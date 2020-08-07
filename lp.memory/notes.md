
- How do I see how much free ram I really have?
         - To see how much ram your applications could use without swapping, run free -m and look at the "available" column:
```
  $ free -m
                total        used        free      shared  buff/cache   available
  Mem:           1504        1491          13           0         855      792
  Swap:          2047           6        2041

  (On installations from before 2016, look at "free" column in the "-/+ buffers/cache" row instead.)

  This is your answer in MiB. If you just naively look at "used" and "free", you'll think your ram is 99% full 
  when it's really just 47%!
```

When should I start to worry about memory ?

- A healthy Linux system with more than enough memory will, after running for a while, show the following expected and harmless behavior:

            free memory is close to 0
            used memory is close to total
            available memory (or "free + buffers/cache") has enough room (let's say, 20%+ of total)
            swap used does not change
            
- Warning signs of a genuine low memory situation that you may want to look into:

            available memory (or "free + buffers/cache") is close to zero
            swap used increases or fluctuates
            dmesg | grep oom-killer shows the OutOfMemory-killer at work


```
Linux memory performance tools include the following: 

- free: report free memory, with buffer cache and page cache .

- dmesg: check for “Out of memory” messages from the OOM killer. 

- valgrind: a performance analysis suite, including memcheck, a wrapper for user-level allocators for memory usage analysis
   - including leak detection. This costs significant overhead; 
   - the manual advises that it can cause the target to run 20 to 30 times slower [3]. 

- swapon: to add and observe physical swap devices or files. iostat: If the swap device is a physical disk or slice,
          device I/O may be observable using iostat(1), which indicates that the system is paging. 

- perf:  this can be used to investigate CPI, MMU/TSB events, and memory bus stall cycles from the CPU performance instrumentation counters. 
         It also provides probes for page faults and several kernel memory (kmem) events. 

- /proc/zoneinfo: statistics for memory zones (NUMA nodes). 

- /proc/buddyinfo: statistics for the kernel buddy allocator for pages.

- prtconf: shows physical memory installed size (which can be filtered from the output using either |grep Mem, or –m on newer versions). 

- prtdiag: shows physical memory layout (on systems that support it). 

- swap: swap statistics: list swap devices (-l), and summarize usage (-s). 

- iostat: If the swap device is a physical disk or slice, device I/O may be observable using iostat(1), 
          which indicates that the system is paging or swapping. 

- cpustat: 
        - this can be used to investigate CPI, MMU/TSB events, and memory bus stall cycles from the CPU performance instrumentation counters. 

- kstat: contains more statistics for understanding kernel memory usage. 

- System-Wide

 - vmstat: virtual and physical memory statistics, system-wide 
 - mpstat: per-CPU usage 
 - iostat: per-disk I/O usage, reported from the block device interface 
 - netstat: network interface statistics, TCP/IP stack statistics, and some per-connection statistics 
 - sar: various statistics; can also archive them for historical reporting
 - tcpdump: network packet tracing (uses libpcap) 
 - blktrace: block I/O tracing (Linux)
 - SystemTap: tracing of kernel internals and the usage of any resource, using static and dynamic tracing 
 - perf: Linux Performance Events, tracing static and dynamic probes
 


 - Per-Process
    ps
    top/htop
    pmap
    strace
    truss
    gdb

- Systemwide profiling
   -  oprofile: Linux system profiling 
   - perf: a Linux performance toolkit, which includes profiling subcommands
   - cachegrind: from the valgrind toolkit, can profile hardware cache usage and be visualized using kcachegrind 
   - Intel VTune Amplifier XE: Linux and Windows profiling, with a graphical interface including source browsing

