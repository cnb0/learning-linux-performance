
# Linux  Systems Performance: Enterprise and the Cloud

 - Large-scale enterprise, cloud, and virtualized computing systems have introduced serious performance challenges. 
 - proven methodologies, tools, and metrics for analyzing and tuning even the most complex environments. 
 - Systems Performance: Enterprise and the Cloud focuses on Linux® and Unix® performance, 
 - while illuminating performance issues that are relevant to all operating systems. 
 - You’ll gain deep insight into how systems work and perform, and 
 - learn methodologies for analyzing and improving system and application performance. 
 - Gregg presents examples from bare-metal systems and virtualized cloud tenants running Linux-based Ubuntu®, Fedora®, CentOS,
   illumos-based Joyent® SmartOS™ and OmniTI OmniOS®. 
 - Modern systems performance, including the “traditional” analysis of CPUs, memory, disks, and networks, 
 - new areas including cloud computing and dynamic tracing. 
 - helps you identify and fix the “unknown unknowns” of complex performance: bottlenecks that emerge from elements and 
   interactions you were not aware of. 
 - The text concludes with a detailed case study, showing how a real cloud customer issue was analyzed from start to finish.

• Modern performance analysis and tuning: terminology, concepts, models, methods, and techniques
• Dynamic tracing techniques and tools, including examples of DTrace, SystemTap, and perf
• Kernel internals: uncovering what the OS is doing
• Using system observability tools, interfaces, and frameworks
• Understanding and monitoring application performance
• Optimizing CPUs: processors, cores, hardware threads, caches, interconnects, and kernel scheduling
• Memory optimization: virtual memory, paging, swapping, memory architectures, busses, address spaces, and allocators
• File system I/O, including caching
• Storage devices/controllers, disk I/O workloads, RAID, and kernel I/O
• Network-related performance issues: protocols, sockets, interfaces, and physical connections
• Performance implications of OS and hardware-based virtualization, and new issues encountered with cloud computing
• Benchmarking: getting accurate results and avoiding common mistakes

- who operates enterprise or cloud environments: system, network, database, and web admins; developers; and other professionals.  


About the Author

1. Introduction
                1.1. Systems Performance
                1.2. Roles
                1.3. Activities
                1.4. Perspectives
                1.5. Performance Is Challenging
                1.6. Latency
                1.7. Dynamic Tracing
                1.8. Cloud Computing
                1.9. Case Studies

2. Methodology
                2.1. Terminology
                2.2. Models
                2.3. Concepts
                2.4. Perspectives
                2.5. Methodology
                2.6. Modeling
                2.7. Capacity Planning
                2.8. Statistics
                2.9. Monitoring
                2.10. Visualizations
                2.11. Exercises
                2.12. References

3. Operating Systems
                3.1. Terminology
                3.2. Background
                3.3. Kernels
                3.4. Exercises
                3.5. References

4. Observability Tools
                4.1. Tool Types
                4.2. Observability Sources
                4.3. DTrace
                4.4. SystemTap
                4.5. perf
                4.6. Observing Observability
                4.7. Exercises
                4.8. References

5. Applications
                5.1. Application Basics
                5.2. Application Performance Techniques
                5.3. Programming Languages
                5.4. Methodology and Analysis
                5.5. Exercises
                5.6. References

6. CPUs
                6.1. Terminology
                6.2. Models
                6.3. Concepts
                6.4. Architecture
                6.5. Methodology
                6.6. Analysis
                6.7. Experimentation
                6.8. Tuning
                6.9. Exercises
                6.10. References

7. Memory
                7.1. Terminology
                7.2. Concepts
                7.3. Architecture
                7.4. Methodology
                7.5. Analysis
                7.6. Tuning
                7.7. Exercises
                7.8. References

8. File Systems
                8.1. Terminology
                8.2. Models
                8.3. Concepts
                8.4. Architecture
                8.5. Methodology
                8.6. Analysis
                8.7. Experimentation
                8.8. Tuning
                8.9. Exercises
                8.10. References

9. Disks
                9.1. Terminology
                9.2. Models
                9.3. Concepts
                9.4. Architecture
                9.5. Methodology
                9.6. Analysis
                9.7. Experimentation
                9.8. Tuning
                9.9. Exercises
                9.10. References

10. Network
                10.1. Terminology
                10.2. Models
                10.3. Concepts
                10.4. Architecture
                10.5. Methodology
                10.6. Analysis
                10.7. Experimentation
                10.8. Tuning
                10.9. Exercises
                10.10. References

11. Cloud Computing
                11.1. Background
                11.2. OS Virtualization
                11.3. Hardware Virtualization
                11.4. Comparisons
                11.5. Exercises
                11.6. References

12. Benchmarking
                12.1. Background
                12.2. Benchmarking Types
                12.3. Methodology
                12.4. Benchmark Questions
                12.5. Exercises
                12.6. References

13. Case Study
                13.1. Case Study: The Red Whale
                13.2. Comments
                13.3. Additional Information
                13.4. References

Appendix A. USE Method: Linux
                Physical Resources
                Software Resources
                Reference

Appendix C. sar Summary
                Linux
                Solaris

Appendix D. DTrace One-Liners
                syscall Provider
                proc Provider
                profile Provider
                sched Provider
                fbt Provider
                pid Provider
                io Provider
                sysinfo Provider
                vminfo Provider
                ip Provider
                tcp provider
                udp provider


Appendix E. DTrace to SystemTap
                Functionality
                Terminology
                Probes
                Built-in Variables
                Functions
                Example 1: Listing syscall Entry Probes
                Example 2: Summarize read() Returned Size
                Example 3: Count syscalls by Process Name
                Example 4: Count syscalls by syscall Name, for Process ID 123
                Example 5: Count syscalls by syscall Name, for “httpd” Processes
                Example 6: Trace File open()s with Process Name and Path Name
                Example 7: Summarize read() Latency for “mysqld” Processes
                Example 8: Trace New Processes with Process Name and Arguments
                Example 9: Sample Kernel Stacks at 100 Hz

Appendix F. Solutions to Selected Exercises
                Chapter 2—Methodology
                Chapter 3—Operating Systems
                Chapter 6—CPUs
                Chapter 7—Memory
                Chapter 8—File Systems
                Chapter 9—Disks
                Chapter 11—Cloud Computing