
## Static Performance Tuning and application/process monitoring

```

- Objectives :
        - Latency: a low application response time 
        - Throughput: a high application operation rate or data transfer rate Resource 
        - utilization: efficiency for a given application workload

        - using metrics that may be derived from business or quality-of-service requirements. 
        - Examples are
             - An average application request latency of 5 ms 
             - 95% of requests at a latency of 100 ms or less 
             - Elimination of latency outliers: zero requests beyond 1,000 ms 
             - A maximum throughput of at least 10,000 application requests per second per server 
             - Average disk utilization under 50% for 10,000 application requests per second

- Static performance tuning focuses on issues of the configured environment. 
  For application performance, examine the following aspects of the static configuration:

        - What version of the application is running? Are there newer versions? Do their release notes mention performance improvements?
        - What known performance issues are there with the application? Is there a bug database that can be searched?
        - How is the application configured?
        - If it was configured or tuned differently from the defaults, what was the reason? (Was it based on measurements and analysis, or guesswork?)
        - Does the application employ a cache of objects? How is it sized?
        - Does the application run concurrently? How is that configured (e.g., thread pool sizing)?
        - Is the application running in a special mode? (For example, debug mode may have been enabled and be reducing performance.)
        - What system libraries does the application use? What versions are they?
        - What memory allocator does the application use?
        - Is the application configured to use large pages for its heap?
        - Is the application compiled? What version of the compiler? What compiler options and optimizations? 64-bit?
        - Has the application encountered an error, and is it now running in a degraded mode?
        - Are there system-imposed limits or resource controls for CPU, memory, file system, disk, or network usage? 
         (These are common with cloud computing.)

               Answering these questions may reveal configuration choices that have been overlooked.


-  CPU bound process-specific performance tools to figure out how the process is behaving

        - Determine whether an application’s runtime is spent in the kernel or application.
        - Determine what library and system calls an application is making and how long they are taking.
        - Profile an application to figure out what source lines and functions are taking the longest time to complete.
        - track the CPU performance bottlenecks of individual processes. 
        - determine how an application was spending its time by attributing the time spent to the Linux kernel, system libraries, or
          even to the application itself. 
        - which calls were made to the kernel and system libraries and how long each took to complete. 
        - profile an application and determine the particular line of source code that was spending a large amount of time. 
        - application that hogs the CPU and use these tools to find the exact functions that are spending all the time.

                        - Process Performance Statistics
                                - Kernel Time Versus User Time
                                - Library Time Versus Application Time
                                - Subdividing Application Time

                                $ time --verbose gcalctool
                                $ strace -c gimp
                                $ ltrace -c /usr/X11R6/bin/xeyes
                                $ ps -o etime,time,pcpu,cmd 10882
                                $ gprof  --brief -p ./burn_gprof
                                        - gcc -gp -g3 -o app app.c
                                - oprofile
                                        $ opgprof application
                                        $ opannotate --source /tmp/burn
                                -  For Java  
                                        -Xrunhprof

- Memory bound process-   diagnose an application’s interaction with the memory subsystem as managed by the Linux kernel and the CPU


        - Determine how much memory an application is using (ps, /proc).
        - Determine which functions of an application are allocating memory (memprof).
        - Profile the memory usage of an application using both software simulation (kcachegrind, cachegrind) 
                - effectiveness of the processor and system cache and memory subsystem
        - Hardware performance counters (oprofile).
        - Determine which processes are creating and using shared memory (ipcs)- monitor shared memory usage 
        - Effectively the application is using the memory subsystem when accessing these allocations
          tools can track every allocation of memory


         
                        $   ps –o vsz,rss,tsiz,dsiz,majflt,minflt,cmd 10882
                        $ cat /proc/<PID>/status
                        $ cat /proc/<PID>/maps
                        $ memprof ./app
                        $ valgrind --skin=cachegrind application
                                $ cg_annotate --25571 --auto=yes
                        $ kcachegrind cachegrind.out.pid
                        - oprofile
                                $ op_help
                                $ opreport -l ./app_name
                        $ ipcs -u
                        $ ipcs -p



```

