
## Static Performance Tuning

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
        - Are there system-imposed limits or resource controls for CPU, memory, file system, disk, or network usage? (These are common with cloud computing.)

Answering these questions may reveal configuration choices that have been overlooked.