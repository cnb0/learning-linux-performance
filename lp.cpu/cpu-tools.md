```
1. Tools Method
        - The tools method is a process of iterating over available tools, 
          examining key metrics they provide. While this is a simple methodology, 
        - it can overlook issues for which the tools provide poor or no visibility, 
        - it can be time-consuming to perform.
        
        - For CPUs, the tools method can involve checking the following: 

            - uptime: Check load averages to see if CPU load is increasing or decreasing over time. 
                    A load average over the number of CPUs in the system usually indicates saturation. 

            - vmstat: Run vmstat per second, and check the idle columns to see how much headroom there is.
                    Less than 10% can be a problem. mpstat: Check for individual hot (busy) CPUs,
                    identifying a possible thread scalability problem. 

            - top/prstat: See which processes and users are the top CPU consumers. 

            - pidstat/prstat: Break down the top CPU consumers into user- and system-time. 

            - perf/dtrace/stap/oprofile: Profile CPU usage stack traces for either user- or kernel-time, 
              to identify why the CPUs are in use. 

            - perf/cpustat: Measure CPI.If an issue is found, examine all fields from the available 
                            tools to learn more context. 


2.  USE Method
        - The USE method is for identifying bottlenecks and errors across all components, early in a 
          performance investigation, before deeper and more time-consuming strategies are followed.
        
        - For each CPU, check for
                - Utilization: 
                        - The time the CPU was busy (not in the idle thread) 
                - Saturation: 
                        - The degree to which runnable threads are queued waiting their turn on-CPU 
                - Errors: 
                        - CPU errors, including correctable errors

3. Workload Characterization
            Basic attributes for characterizing CPU workload are 
                - Load averages (utilization + saturation) 
                - User-time to system-time ratio 
                - Syscall rate 
                - Voluntary context switch rate 
                - Interrupt rate
                - What is the CPU utilization system-wide? Per CPU? 
                - How parallel is the CPU load? Is it single-threaded? How many threads? 
                - Which applications or users are using the CPUs? How much? 
                - Which kernel threads are using the CPUs? How much?
                - What is the CPU usage of interrupts? 
                - What is the CPU interconnect utilization? 
                - Why are the CPUs being used (user- and kernel-level call paths)? 
                - What types of stall cycles are encountered?
4. Profiling
            - Profiling builds a picture of the target for study. 
            - CPU usage can be profiled by sampling the state of the CPUs at timed intervals, 
              following these steps:
                    - Select the type of profile data to capture, and the rate.
                    - Begin sampling at a timed interval.
                    - Wait while the activity of interest occurs.
                    - End sampling and collect sample data.
                    - Process the data.

            - The types of CPU profile data are based on the following factors: 
                    - User level, kernel level, or 
                    - both Function and offset (program-counter-based),function only, 
                      partial stack trace, or full stack trace
            - Selecting full stack traces for both user and kernel level captures the complete profile of CPU usage

5. Performance Monitoring
        Performance monitoring can identify active issues and patterns of behavior over time.
         Key metrics for CPUs are 
            - Utilization: percent busy
            - Saturation: 
               - either run-queue length, inferred from load average, or 
               - as a measure of thread scheduler latency

6. Static Performance Tuning
        - Static performance tuning focuses on issues of the configured environment.
        - For CPU performance, examine the following aspects of the static configuration: 
            - How many CPUs are available for use? Are they cores? Hardware threads? 
            - Is the CPU architecture single- or multiprocessor? 
            - What is the size of the CPU caches? Are they shared? 
            - What is the CPU clock speed? Is it dynamic (e.g., Intel Turbo Boost and SpeedStep)? 
            - Are those dynamic features enabled in the BIOS? 
            - What other CPU-related features are enabled or disabled in the BIOS? 
            - Are there performance issues (bugs) with this processor model? 
            - Are they listed in the processor errata sheet? 
            - Are there performance issues (bugs) with this BIOS firmware version? 
            - Are there software-imposed CPU usage limits (resource controls) present? What are they?
        
      - The answers to these questions may reveal previously overlooked configuration choices.
        - The last question is especially true for cloud computing environments, where 
          CPU usage is commonly limited.

7. Priority Tuning
        - Unix has always provided a nice() system call for adjusting process priority, 
          which sets a nice-ness value. 
        - Positive nice values result in lower process priority (nicer), and 
        - negative values—which can be set only by the superuser (root)—result in higher priority

8. Resource Controls
        - The operating system may provide fine-grained controls for allocating CPU cycles to 
          processes or groups of processes. 
        - These may include fixed limits for CPU utilization and shares for a more flexible approach—allowing
          idle CPU cycles to be consumed based on a share value

9. CPU Binding

        -  to tune CPU performance involves binding processes and threads to individual CPUs, or collections of CPUs. 
        -  This can increase CPU cache warmth for the process, improving its memory I/O performance. 
             - For NUMA systems it also improves memory locality, also improving performance.
        - Process binding: 
                - configuring a process to run only on a single CPU, or only on one CPU from a defined set. 
        - Exclusive CPU sets:
                - partitioning a set of CPUs that can be used only by the process(es) assigned to them. 
                - This can improve CPU cache further, as when the process is idle other processes cannot use the CPUs, 
                  leaving the caches warm.
          
          On Linux-based systems, the exclusive CPU sets approach can be implemented using cpusets
