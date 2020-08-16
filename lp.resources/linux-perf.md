
## Optimizing Linux Performance :
```

- Superior application performance is more crucial than ever—and in today's complex production environments, 
  it's tougher to ensure, too. 
- If you use Linux, you have extraordinary advantages: complete source code access, plus an exceptional 
  array of optimization tools. 
- But the tools are scattered across the Internet. Many are poorly documented. And few experts know how to use them
  together to solve real problems. Now, one of those experts has written the definitive Linux tuning primer for every professional: 
  Optimizing Linux® Performance.

Linux optimization tools,showing how they fit into a proven methodology for perfecting overall application performance. 
shows developers how to pinpoint exact lines of source code that are impacting performance. 
so they can implement solutions more quickly. 

How to:

    - Identify bottlenecks even if you're not familiar with the underlying system
    - Find and choose the right performance tools for any problem
    - Recognize the meaning of the events you're measuring
    - Optimize system CPU, user CPU, memory, network I/O, and disk I/O—and understand their interrelationships
    - Fix CPU-bound, latency-sensitive, and I/O-bound applications, through case studies you can easily 
      adapt to your own environment
    - Install and use oprofile, the advanced systemwide profiler for Linux systems


1. Performance Hunting Tips
            1.1. General Tips
                    1.1.1. Take Copious Notes (Save Everything)
                    1.1.2. Automate Redundant Tasks
                    1.1.3. Choose Low-Overhead Tools If Possible
                    1.1.4. Use Multiple Tools to Understand the Problem
                    1.1.5. Trust Your Tools
                    1.1.6. Use the Experience of Others (Cautiously)

            1.2. Outline of a Performance Investigation
                    1.2.1. Finding a Metric, Baseline, and Target
                           Establish a Metric
                           Establish a Baseline
                           Establish a Target
                    1.2.2. Track Down the Approximate Problem
                    1.2.3. See Whether the Problem Has Already Been Solved
                    1.2.4. The Case Begins (Start to Investigate)
            

2. Performance Tools: System CPU
                    2.1. CPU Performance Statistics
                            2.1.1. Run Queue Statistics
                            2.1.2. Context Switches
                            2.1.3. Interrupts
                            2.1.4. CPU Utilization
                    2.2. Linux Performance Tools: CPU
                         vmstat (Virtual Memory Statistics)
                         CPU Performance-Related Options
                            2.2.3. top (v. 3.x.x)
                            2.2.3.1. CPU Performance-Related Options
                            2.2.4. procinfo (Display Info from the /proc File System)
                        2.2.5. gnome-system-monitor
                        2.2.6. mpstat (Multiprocessor Stat)
                        2.2.7. sar (System Activity Reporter)
                        2.2.8. oprofile
                    
3. Performance Tools: System Memory
                        3.1. Memory Performance Statistics
                        3.1.1. Memory Subsystem and Performance
                        3.1.2. Memory Subsystem (Virtual Memory)
                                3.1.2.1. Swap (Not Enough Physical Memory)
                                3.1.2.2. Buffers and Cache (Too Much Physical Memory)
                                3.1.2.3. Active Versus Inactive Memory
                                3.1.2.4. High Versus Low Memory
                                3.1.2.5. Kernel Usage of Memory (Slabs)
                        3.2. Linux Performance Tools: CPU and Memory
                            3.2.1. vmstat (Virtual Memory Statistics) II
                                3.2.1.1. System-Wide Memory-Related Options
                                    3.2.2. top (2.x and 3.x)
                                3.2.2.1. Memory Performance-Related Options
                                    3.2.3. procinfo II
                                    3.2.4. gnome-system-monitor (II)
                                    3.2.5. free
                                    3.2.6. slabtop
                                    3.2.7. sar (II)
                                    3.2.8. /proc/meminfo
                            

4. Performance Tools: Process-Specific CPU
                        4.1. Process Performance Statistics
                                4.1.1. Kernel Time Versus User Time
                                4.1.2. Library Time Versus Application Time
                                4.1.3. Subdividing Application Time
                        4.2. The Tools
                                4.2.1. time
                                4.2.2. strace
                                4.2.3. ltrace
                                4.2.4. ps (Process Status)
                                4.2.5. ld.so (Dynamic Loader)
                                4.2.6. gprof
                                4.2.7. oprofile (II)
                                4.2.8. Languages: Static (C and C++) Versus Dynamic (Java and Mono)


5. Performance Tools: Process-Specific Memory
                        5.1. Linux Memory Subsystem
                        5.2. Memory Performance Tools
                                5.2.1. ps
                                5.2.2. /proc/<PID>
                                5.2.3. memprof
                                5.2.4. valgrind (cachegrind)
                                5.2.5. kcachegrind
                                5.2.6. oprofile (III)
                                5.2.7. ipcs
                                5.2.8. Dynamic Languages (Java, Mono)


6. Performance Tools: Disk I/O
                        6.1. Introduction to Disk I/O
                        6.2. Disk I/O Performance Tools
                        6.2.1. vmstat (ii)
                              6.2.1.1. Disk I/O Performance-Related Options and Outputs
                        6.2.2. iostat
                        6.2.3. sar
                        6.2.4. lsof (List Open Files)
        
7. Performance Tools: Network
                        7.1. Introduction to Network I/O
                                7.1.1. Network Traffic in the Link Layer
                                7.1.2. Protocol-Level Network Traffic
                        7.2. Network Performance Tools
                                7.2.1. mii-tool (Media-Independent Interface Tool)
                                7.2.2. ethtool
                                7.2.3. ifconfig (Interface Configure)
                                7.2.4. ip
                                7.2.5. sar
                                7.2.6. gkrellm
                                7.2.7. iptraf
                                7.2.8. netstat
                                7.2.9. etherape
                            

8. Utility Tools: Performance Tool Helpers
                        8.1. Performance Tool Helpers
                                8.1.1. Automating and Recording Commands
                                8.1.2. Graphing and Analyzing Performance Statistics
                                8.1.3. Investigating the Libraries That an Application Uses
                                8.1.4. Creating and Debugging Applications
                        8.2. Tools
                                8.2.1. bash
                                8.2.2. tee
                                8.2.3. script
                                8.2.4. watch
                                8.2.5. gnumeric
                                8.2.6. ldd
                                8.2.7. objdump
                                8.2.8. GNU Debugger (gdb)
                                8.2.9. gcc (GNU Compiler Collection)
                                        8.2.9.1. Performance-Related Options

9. Using Performance Tools to Find Problems
                        9.1. Not Always a Silver Bullet
                        9.2. Starting the Hunt
                        9.3. Optimizing an Application
                                 Is Memory Usage a Problem?
                                 Is Startup Time a Problem?
                                 Is the Loader Introducing a Delay?
                                 Is CPU Usage (or Length of Time to Complete) a Problem?
                                 Is the Application’s Disk Usage a Problem?
                                 Is the Application’s Network Usage a Problem?
                        9.4. Optimizing a System
                                    9.4.1. Is the System CPU-Bound?
                                        9.4.2. Is a Single Processor CPU-Bound?
                                        9.4.3. Are One or More Processes Using Most of the System CPU?
                                        9.4.4. Are One or More Processes Using Most of an Individual CPU?
                                        9.4.5. Is the Kernel Servicing Many Interrupts?
                                        9.4.6. Where Is Time Spent in the Kernel?
                                        9.4.7. Is the Amount of Swap Space Being Used Increasing?
                                        9.4.8. Is the System I/O-Bound?
                                        9.4.9. Is the System Using Disk I/O?
                                        9.4.10. Is the System Using Network I/O?
                        9.5. Optimizing Process CPU Usage
                                        9.5.1. Is the Process Spending Time in User or Kernel Space?
                                        9.5.2. Which System Calls Is the Process Making, and How Long Do They Take to Complete?
                                        9.5.3. In Which Functions Does the Process Spend Time?
                                        9.5.4. What Is the Call Tree to the Hot Functions?
                                        9.5.5. Do Cache Misses Correspond to the Hot Functions or Source Lines?
                        9.6. Optimizing Memory Usage
                                    9.6.1. Is the Kernel Memory Usage Increasing?
                                    9.6.2. What Type of Memory Is the Kernel Using?
                                    9.6.3. Is a Particular Process’s Resident Set Size Increasing?
                                    9.6.4. Is Shared Memory Usage Increasing?
                                    9.6.5. Which Processes Are Using the Shared Memory?
                                    9.6.6. What Type of Memory Is the Process Using?
                                    9.6.7. What Functions Are Using All of the Stack?
                                    9.6.8. What Functions Have the Biggest Text Size?
                                    9.6.9. How Big Are the Libraries That the Process Uses?
                                    9.6.10. What Functions Are Allocating Heap Memory?
                        9.7. Optimizing Disk I/O Usage
                                    9.7.1. Is the System Stressing a Particular Disk?
                                    9.7.2. Which Application Is Accessing the Disk?
                                    9.7.3. Which Files Are Accessed by the Application?
                        9.8. Optimizing Network I/O Usage
                                    9.8.1. Is Any Network Device Sending/Receiving Near the Theoretical Limit?
                                    9.8.2. Is Any Network Device Generating a Large Number of Errors?
                                    9.8.3. What Type of Traffic Is Running on That Device?
                                    9.8.4. Is a Particular Process Responsible for That Traffic?
                                    9.8.5. What Remote System Is Sending the Traffic?
                                    9.8.6. Which Application Socket Is Responsible for the Traffic?
                        
10. Performance Hunt 1: A CPU-Bound Application (GIMP)
                        10.1. CPU-Bound Application
                        10.2. Identify a Problem
                        10.3. Find a Baseline/Set a Goal
                        10.4. Configure the Application for the Performance Hunt
                        10.5. Install and Configure Performance Tools
                        10.6. Run Application and Performance Tools
                        10.7. Analyze the Results
                        10.8. Jump to the Web
                        10.9. Increase the Image Cache
                        10.10. Hitting a (Tiled) Wall
                        10.11. Solving the Problem
                        10.12. Verify Correctness?

11. Performance Hunt 2: A Latency-Sensitive Application (nautilus)
                        11.1. A Latency-Sensitive Application
                        11.2. Identify a Problem
                        11.3. Find a Baseline/Set a Goal
                        11.4. Configure the Application for the Performance Hunt
                        11.5. Install and Configure Performance Tools
                        11.6. Run Application and Performance Tools
                        11.7. Compile and Examine the Source
                        11.8. Using gdb to Generate Call Traces
                        11.9. Finding the Time Differences
                        11.10. Trying a Possible Solution

12. Performance Hunt 3: The System-Wide Slowdown (prelink)
                        12.1. Investigating a System-Wide Slowdown
                        12.2. Identify a Problem
                        12.3. Find a Baseline/Set a Goal
                        12.4. Configure the Application for the Performance Hunt
                        12.5. Install and Configure Performance Tools
                        12.6. Run Application and Performance Tools
                        12.7. Simulating a Solution
                        12.8. Reporting the Problem
                        12.9. Testing the Solution

13. Performance Tools: What’s Next?
                        13.1. The State of Linux Tools
                        13.2. What Tools Does Linux Still Need?
                        13.2.1. Hole 1: Performance Statistics Are Scattered
                        13.2.2. Hole 2: No Reliable and Complete Call Tree
                        13.2.3. Hole 3: I/O Attribution
                        13.3. Performance Tuning on Linux
                        
