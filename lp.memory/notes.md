

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

