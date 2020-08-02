
# CPU 

 - Processor: the physical chip that plugs into a socket on the system or processor board and 
              contains one or more CPUs implemented as cores or hardware threads.
 
 - Core: 
            - an independent CPU instance on a multicore processor. 
            - The use of cores is a way to scale processors, called chip-level multiprocessing (CMP). 
 
 - Hardware thread: 
            - a CPU architecture that supports executing multiple threads in parallel
              on a single core (including Intel’s Hyper-Threading Technology), where each thread is an independent 
 
 - CPU instance.
            - One name for this scaling approach is multithreading. 
 
 - CPU instruction: 
            - a single CPU operation, from its instruction set. 
            - There are instructions for arithmetic operations, memory I/O, and control logic. 
 
 - vCpu/Logical CPU: 
            - also called a virtual processor,1 an operating system CPU instance (a schedulable CPU entity). 
            - This may be implemented by the processor as a hardware thread 
              (in which case it may also be called a virtual core), a core, or a single-core processor.

 - Scheduler:
            - the kernel subsystem that assigns threads to run on CPUs.

 - Image Run queue: 
            - a queue of runnable threads that are waiting to be serviced by CPUs. 


- CPU Memory CachesProcessors provide various hardware caches for improving memory I/O performance

- CPU Run Queues
           - The number of software threads that are queued and ready to
             run is an important performance metric indicating CPU saturation
              

 - Concepts CPU performance, 
        - the CPU clock rate 
                - The clock is a digital signal that drives all processor logic. 
                - Each CPU instruction may take one or more cycles of the clock (called CPU cycles) to execute. 
                - CPUs execute at a particular clock rate; 
                        - a 5 GHz CPU performs 5 billion clock cycles per second.

        - CPU Instruction :
                - CPUs execute instructions chosen from their instruction set. 
                - An instruction includes the following steps, each processed by a component of the CPU called a functional unit:
                    - Instruction fetch
                    - Instruction decode
                    - Execute
                    - Memory access
                    - Register write-back

        - Instruction Pipeline
                    - The instruction pipeline is a CPU architecture that can execute multiple instructions in parallel

        -  Utilization
                    - CPU utilization is measured by the time a CPU instance is busy performing work during an interval,
                       expressed as a percentage. 
                    - It can be measured as the time a CPU is not running the kernel idle thread but is instead running 
                      user-level application threads or other kernel threads, or processing interrupt
                    - performance does not degrade steeply under high utilization, as the kernel supports priorities, preemption, 
                      and time sharing

        - User-Time/Kernel-Time
                    - The CPU time spent executing user-level application code is called user-time, and kernel-level code is kernel-time. 
                    - Kernel-time includes time during system calls, kernel threads, and interrupts. 
                    - When measured across the entire system, the user-time/kernel-time ratio indicates the type of workload performed.

        -  Saturation
                    - A CPU at 100% utilization is saturated, and 
                    - threads will encounter scheduler latency as they wait to run on-CPU, decreasing overall performance. 
                    - This latency is the time spent waiting on the CPU run queue or other structure used to manage threads.

        - Preemption
                    - Allows a higher-priority thread to preempt the currently running thread and begin its own execution instead 
                    - This eliminates the run-queue latency for higher-priority work, improving its performance
                    
        - Priority Inversion
                    - Priority inversion occurs when a lower-priority thread holds a resource and 
                      blocks a higher-priority thread from running. 
                    - This reduces the performance of the higher-priority work, as it is blocked waiting.
