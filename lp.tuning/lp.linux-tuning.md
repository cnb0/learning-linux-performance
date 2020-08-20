
## System Performance is Observability , Methodologies, Benchmarking, profiling , tracing, tuning 

- Workload characterization
- USE Method 
- Resource Analysis
- Workload analysis
- CPU profile method
- off-CPU analysis
- static performance tuning


### Linux OS Tuning
        - CPU 
        - Virtual memory
        - File system
        - Storage I/O
        - networking
        - hypervisor 

-  Ubuntu server out of box is not optimized to make full use of available hardware. 
   This means “out-of-box” setup might fail under high load.
-  So we need to tweak system configuration for maximum concurrancy.

### USE Method  - Start with questions then find the right tools
    - for every resource check 
    - Utilization
        - CPU - time busy
    - Saturation
         - run queue length or latency 
    - Errors
         - ECC errors

### Workload characterization
    - Analyze workload charateristics , not resulting performance 
         - for Example CPUs
                - Who
                    - which pids, programs, users
                - Why
                    - codepaths, contexts
                - What
                    - CPU instructions, cycles
                - How
                    - changing over time

    
### benchmarking - an experimental analysis activity 
    - For any benchmark ask why not 10x


### Linux perf Analysis - Quick check on system performance

    - load avgs
            $ uptime
    - kernel errors
            $ dmesg -T | tail
    - overall stats by time
            $ vmstat 1
    - CPU balance
            $ mpstat -p ALL 1
    - process usage
            $ pidstat 1
    - disk  I/O
            $ iostat -xz 1
    - memory usage
            $ free -m
    - network i/O
            $ sar -n DEV 1
    - TCp stats
            $ sar -n TCP,ETCP 1
    - Check overview
            $ top
            $ htop
      
```
- perf counters - performance monitoring counters

- List & reloading changes -  /etc/sysctl.conf
            $ sysctl --all
            $ sysctl --load
          

            - Show all system parameters with their values (default or changed)
                $ sysctl -A 
            - Show values of parameters modified by you
                $ sysctl -p

- CPU 
        - disable ubuntu apport (crash reporter)
            $ schedtool -B PID

- Process Scheduler ( CFS scheduler ) 
         - kernel parameter that determines how long a migrated process has to be running before the 
           kernel will consider migrating it again to another core. 
         - The sysctl name is sched_migration_cost_ns, default value 50000 (that's ns so 0.5 ms):
                    
                    $ cat /proc/sys/kernel/sched_migration_cost_ns
                    $ sysctl -w kernel.sched_migration_cost_ns=5000000

         - parameter that can dramatically impact forking servers is sched_autogroup_enabled.
           This setting groups tasks by TTY, to improve perceived responsiveness on an interactive system.
           On a server with a long running forking daemon, this will tend to keep child processes 
           from migrating away as soon as they should. It can be disabled like so:

                    $ sysctl -w kernel.sched_autogroup_enabled=0
                    
            - Various PostgreSQL users have reported gains up to 30% on highly concurrent workloads on multi-core systems

# sysctl -w kernel.sched_autogroup_enabled=0

- Virtual memory 
            - do less swapping
                $ echo 10 > /proc/sys/vm/swappiness
                $ sysctl -w vm.swappiness=10
                          vm.dirty_ratio = 60
                          vm.dirty_background_ratio = 2
             - Raise the vm map count value
                        $ sudo sysctl -w "vm.max_map_count=2048000"
             - Raise the vm map count value 
                        $ sudo bash -c "echo 0 > /proc/sys/vm/overcommit_memory"

- Improve system memory management 
                - echo madvise > /sys/kernel/mm/transparent_hugepage/enabled
                - disable Transparent Huge Pages
                         $ sudo bash -c "echo madvise > /sys/kernel/mm/transparent_hugepage/enabled"
                         $ sudo bash -c "echo madvise > /sys/kernel/mm/transparent_hugepage/defrag"
                - kernel.numa_balancing = 0

- FileSystem
                - Increase size of file handles and inode cache
                - When you're serving a lot of traffic it is usually the case that the traffic 
                   you're serving is coming from a large number of local files.
                     $  cat /proc/sys/fs/file-max
                     $  sysctl -w fs.file-max = 2097152
                        fs.file-max = 2097152

                        - vm.dirty_ratio  = 80
                        - vm.dirty_background_ratio = 5
                        - vm.dirty_expire_centisecs = 12000
                        - mount -o defaults, noatime,discard,nobarrier

                -  disable the "atime" option on your filesystems.
                    - With this disabled that the last time a file was accessed won't be constantly updated every time you read a file, 
                     since this information isn't generally useful inand causes extra disk hits, its typically disabled.


To do this, just edit /etc/fstab and add "notime" as a mount option for the filesystem



- Storage I/O 
                - /sys/block/*/queue/rq_affinity   1 
                - /sys/block/*/queue/scheduler     kyber
                - /sys/block/*/queue/nr_requests   256
                - /sys/block/*/queue/read_ahead_kb 128
                - mdadm --chunk=64 
        
- Misc
                - net.core.bpf_jit_enable = 1
                - sysctl -w kernel.perf_event_max_stack = 1000
                    plus use AWS Nitro

- Hypervisor 
                - echo tsc > /sys/devices/../current_clocksource

```