

- Methodology for identifying and resolving every type of Linux-related system or application problem: 
        - errors, crashes, hangs, performance slowdowns, unexpected behavior, and unexpected outputs. 
    
- Increase your efficiency, productivity, and marketability

- If you're involved with deploying or managing Linux in the enterprise 

  help you significantly reduce operation costs, enhance availability, and improve ROI

- Discover proven best practices for diagnosing problems in Linux environments
- Leverage troubleshooting skills you've developed with other platforms
- Learn to identify problems with strace—the most frequently used Linux troubleshooting tool
- Use /proc to uncover crucial information about hardware, kernels, and processes
- Recompile open source applications with debug information
- Debug applications with gdb, including C++ and threaded applications
- Debug kernel crashes and hangs, one step at a time
- Understand the Executable and Linking Format (ELF), and use that knowledge for more effective debugging


```
1. Best Practices and Initial Investigation
                        
                     - Getting Your System(s) Ready for Effective Problem Determination
                     - The Four Phases of Investigation
                         Phase #1: Initial Investigation Using Your Own Skills
                                    Did Anything Change Recently?
                         Phase #2: Searching the Internet Effectively
                                    Google
                                    USENET
                                    Linux Web Resources
                                    Bugzilla Databases
                                    Mailing Lists
                         Phase #3: Begin Deeper Investigation (Good Problem Investigation Practices)
                                     Best Practices for Complex Investigations
                                     Collect the Relevant Information When the Problem Occurs
                                     Use an Investigation Log
                                     Be Detailed (Avoid Qualitative Information)
                                     Challenge Assumptions
                                            Narrow Down the Scope of the Problem
                                            Create a Reproducible Test Case
                                     Work to Prove and/or Disprove Theories
                                     
                        Phase #4: Getting Help or New Ideas
                                    Profile of a Linux Guru
                                    Effectively Asking for Help
                                    Netiquitte
                                    Composing an Effective Message
                                    Giving Back to the Community
                                    USENET
                                    Mailing Lists
                                    Tips on Opening Bug Reports in Bugzilla
                        
                         Use Your Distribution’s Support
                                    Technical Investigation
                                    Symptom Versus Cause
                                      - Error
                                    Crashes
                                     - Traps
                                     - Panics
                                     - Kernel Crashes
                          Hangs (or Very Slow Performance)
                                    - Multi-Process Applications
                                    - Very Busy Systems
                                    - Performance
                                    - Unexpected Behavior/Output
                                    - Troubleshooting Commercial Products


2. strace and System Call Tracing Explained
                        2.1. Introduction
                        2.2. What Is strace?
                        2.2.1. More Information from the Kernel Side
                        2.2.2. When To Use It
                        2.2.3. Simple Example
                        2.2.4. Same Program Built Statically
                        2.3. Important strace Options
                        2.3.1. Following Child Processes
                        2.3.2. Timing System Call Activity
                        2.3.3. Verbose Mode
                        2.3.4. Tracing a Running Process
                        2.4. Effects and Issues of Using strace
                        2.4.1. strace and EINTR
                        2.5. Real Debugging Examples
                        2.5.1. Reducing Start Up Time by Fixing LD_LIBRARY_PATH
                        2.5.2. The PATH Environment Variable
                        2.5.3. stracing inetd or xinetd (the Super Server)
                        2.5.4. Communication Errors
                        2.5.5. Investigating a Hang Using strace
                        2.5.6. Reverse Engineering (How the strace Tool Itself Works)
                        2.6. System Call Tracing Example
                        2.6.1. Sample Code
                        2.6.2. The System Call Tracing Code Explained


3. The /proc Filesystem
                        3.1. Introduction
                        3.2. Process Information
                        3.2.1. /proc/self
                        3.2.2. /proc/<pid> in More Detail
                        3.2.2.1. /proc/<pid>/maps
                        3.2.2.1.1. Code Segment
                        3.2.2.1.2. Data Segment
                        3.2.2.1.3. Heap Segment
                        3.2.2.1.4. Mapped Base / Shared Libraries
                        3.2.2.1.5. Stack Segment
                        3.2.2.1.6. The Kernel Segment
                        3.2.2.1.7. 64-bit /proc/<pid>/maps Differences
                        3.2.3. /proc/<pid>/cmdline
                        3.2.4. /proc/<pid>/environ
                        3.2.5. /proc/<pid>/mem
                        3.2.6. /proc/<pid>/fd
                        3.2.7. /proc/<pid>/mapped_base
                        3.3. Kernel Information and Manipulation
                        3.3.1. /proc/cmdline
                        3.3.2. /proc/config.gz or /proc/sys/config.gz
                        3.3.3. /proc/cpufreq
                        3.3.4. /proc/cpuinfo
                        3.3.5. /proc/devices
                        3.3.6. /proc/kcore
                        3.3.7. /proc/locks
                        3.3.8. /proc/meminfo
                        3.3.9. /proc/mm
                        3.3.10. /proc/modules
                        3.3.11. /proc/net
                        3.3.12. /proc/partitions
                        3.3.13. /proc/pci
                        3.3.14. /proc/slabinfo
                        3.4. System Information and Manipulation
                        3.4.1. /proc/sys/fs
                        3.4.1.1. dir-notify-enable
                        3.4.1.2. file-nr
                        3.4.1.3. file-max
                        3.4.1.4. aio-max-nr, aix-max-pinned, aix-max-size, aio-nr, and aio-pinned
                        3.4.1.5. overflowgid and overflowuid
                        3.4.2. /proc/sys/kernel
                        3.4.2.1. core_pattern
                        3.4.2.2. msgmax, msgmnb, and msgmni
                        3.4.2.3. panic and panic_on_oops
                        3.4.2.4. printk
                        3.4.2.5. sem
                        3.4.2.6. shmall, shmmax, and shmmni
                        3.4.2.7. sysrq
                        3.4.2.7.1. showPc Output:
                        3.4.2.7.2. showMem Output:
                        3.4.2.7.3. showTasks Output:
                        3.4.2.8. tainted
                        3.4.3. /proc/sys/vm


4. Compiling
                        4.1. Introduction
                        4.2. The GNU Compiler Collection
                        4.2.1. A Brief History of GCC
                        4.2.2. GCC Version Compatibility
                        4.3. Other Compilers
                        4.4. Compiling the Linux Kernel
                        4.4.1. Obtaining the Kernel Source
                        4.4.2. Architecture Specific Source
                        4.4.3. Working with Kernel Source Compile Errors
                        4.4.3.1. A Real Kernel Compile Error Example
                        4.4.4. General Compilation Problems
                        4.4.4.1. Environment/Setup Errors or Differences
                        4.4.4.2. Compiler Version Differences or Bugs
                        4.4.4.3. User Error
                        4.4.4.4. Code Error
                        4.5. Assembly Listings
                        4.5.1. Purpose of Assembly Listings
                        4.5.2. Generating Assembly Listings
                        4.5.3. Reading and Understanding an Assembly Listing
                        4.6. Compiler Optimizations
                        4.7. Conclusion

5. The Stack
                        5.1. Introduction
                        5.2. A Real-World Analogy
                        5.3. Stacks in x86 and x86-64 Architectures
                        5.4. What Is a Stack Frame?
                        5.5. How Does the Stack Work?
                        5.5.1. The BP and SP Registers
                        5.5.1.1. Special Case: gcc’s -fomit-frame-pointer Compile Option
                        5.5.2. Function Calling Conventions
                        5.5.2.1. x86 Architecture
                        5.5.2.1.1. Return Value
                        5.5.2.2. x86-64 Architecture
                        5.5.2.2.1. Return Value
                        5.6. Referencing and Modifying Data on the Stack
                        5.7. Viewing the Raw Stack in a Debugger
                        5.8. Examining the Raw Stack in Detail
                        5.8.1. Homegrown Stack Traceback Function
                        5.8.1.1. Using GLIBC’s backtrace()
                        5.8.1.1.1. The -rdynamic Switch
                        5.8.1.2. Manually “Walking the Stack”
                        5.8.1.2.1. Modifying for x86-64
                        5.8.1.3. Stack Corruption
                        5.8.1.4. SIGILL Signals
                        5.8.1.4.1. Signals and the Stack


6. The GNU Debugger (GDB)
                        6.1. Introduction
                        6.2. When To Use a Debugger
                        6.3. Command Line Editing
                        6.4. Controlling a Process with GDB
                        6.4.1. Running a Program Off the Command Line with GDB
                        6.4.2. Attaching to a Running Process
                        6.4.3. Use a Core File
                        6.4.3.1. Changing Core File Name and Location
                        6.4.3.2. Saving the State of a GDB Session
                        6.5. Examining Data, Memory, and Registers
                        6.5.1. Memory Map
                        6.5.2. Stack
                        6.5.2.1. Navigating Stack Frames
                        6.5.2.2. Obtaining and Understanding Frame Information
                        6.5.3. Examining Memory and Variables
                        6.5.3.1. Variables and Scope and Type
                        6.5.3.2. Print Formatting
                        6.5.3.3. Determining the Type of Variable
                        6.5.3.4. Viewing Data in Memory
                        6.5.3.5. Formatting Values in Memory
                        6.5.3.6. Changing Variables
                        6.5.4. Register Dump
                        6.6. Execution
                        6.6.1. The Basic Commands
                        6.6.1.1. Notes on stepi
                        6.6.2. Settings for Execution Control Commands
                        6.6.2.1. Step-mode
                        6.6.2.2. Following fork Calls
                        6.6.2.3. Handling Signals
                        6.6.3. Breakpoints
                        6.6.4. Watchpoints
                        6.6.5. Display Expression on Stop
                        6.6.6. Working with Shared Libraries
                        6.6.6.1. Debugging Functions in Shared Libraries
                        6.7. Source Code
                        6.8. Assembly Language
                        6.9. Tips and Tricks
                        6.9.1. Attaching to a Process—Revisited
                        6.9.1.1. The pause() method
                        6.9.1.2. The “for” or “while” Loop Method
                        6.9.1.3. The xterm method
                        6.9.2. Finding the Address of Variables and Functions
                        6.9.3. Viewing Structures in Executables without Debug Symbols
                        6.9.4. Understanding and Dealing with Endian-ness
                        6.10. Working with C++
                        6.10.1. Global Constructors and Destructors
                        6.10.2. Inline Functions
                        6.10.3. Exceptions
                        6.11. Threads
                        6.11.1. Running Out of Stack Space
                        6.12. Data Display Debugger (DDD)
                        6.12.1. The Data Display Window
                        6.12.1.1. Viewing the Raw Stack
                        6.12.1.2. View Complex Data Structures
                        6.12.2. Source Code Window
                        6.12.3. Machine Language Window
                        6.12.4. GDB Console Window


7. Linux System Crashes and Hangs
                        7.1. Introduction
                        7.2. Gathering Information
                        7.2.1. Syslog Explained
                        7.2.2. Setting up a Serial Console
                        7.2.3. Connecting the Serial Null-Modem Cable
                        7.2.4. Enabling the Serial Console at Startup
                        7.2.5. Using SysRq Kernel Magic
                        7.2.6. Oops Reports
                        7.2.7. Adding a Manual Kernel Trap
                        7.2.8. Examining an Oops Report
                        7.2.8.1. 2.6.x Kernel Oops Dumps
                        7.2.9. Determining the Failing Line of Code
                        7.2.9.1. 2.4.x Kernel Oops Dumps
                        7.2.10. Kernel Oopses and Hardware
                        7.2.11. Setting up cscope to Index Kernel Sources


8. Kernel Debugging with KDB
                    8.1. Introduction
                    8.2. Enabling KDB
                    8.3. Using KDB
                    8.3.1. Activating KDB
                    8.3.2. Resuming Normal Execution
                    8.3.3. Basic Commands


9. ELF: Executable and Linking Format
                    9.1. Introduction
                    9.2. Concepts and Definitions
                    9.2.1. Symbol
                    9.2.1.1. Symbols Names and C Versus C++
                    9.2.2. Object Files, Shared Libraries, Executables, and Core Files
                    9.2.2.1. Object Files
                    9.2.2.2. Shared Libraries
                    9.2.2.3. Exectuables
                    9.2.2.4. Core Files
                    9.2.2.5. Static Libraries
                    9.2.3. Linking
                    9.2.3.1. Linking with Static Libraries
                    9.2.4. Run Time Linking
                    9.2.5. Program Interpreter / Run Time Linker
                    9.3. ELF Header
                    9.4. Overview of Segments and Sections
                    9.5. Segments and the Program Header Table
                    9.5.1. Text and Data Segments
                    9.6. Sections and the Section Header Table
                    9.6.1. String Table Format
                    9.6.2. Symbol Table Format
                    9.6.3. Section Names and Types
                    9.6.3.1. .bss
                    9.6.3.2. .data
                    9.6.3.3. .dynamic
                    9.6.3.4. .dynsym (symbol table)
                    9.6.3.5. .dynstr (string table)
                    9.6.3.6. .fini
                    9.6.3.7. .got (Global Offset Table)
                    9.6.3.8. .hash
                    9.6.3.9. .init
                    9.6.3.10. .interp
                    9.6.3.11. .plt (Procedure Linkage Table)
                    9.6.3.12. .rodata
                    9.6.3.13. .shstrtab
                    9.6.3.14. .strtab (string table)
                    9.6.3.15. .symtab (symbol table)
                    9.6.3.16. .text
                    9.6.3.17. .rel
                    9.7. Relocation and Position Independent Code (PIC)
                    9.7.1. PIC vs. non-PIC
                    9.7.2. Relocation and Position Independent Code
                    9.7.3. Relocation and Linking
                    9.8. Stripping an ELF Object
                    9.9. Program Interpreter
                    9.9.1. Link Map
                    9.10. Symbol Resolution
                    9.11. Use of Weak Symbols for Problem Investigations
                    9.12. Advanced Interception Using Global Offset Table
                    9.13. Source Files
                    9.14. ELF APIs
                    9.15. Other Information


A. The Toolbox
                    A.1. Introduction
                    A.2. Process Information and Debugging
                    A.2.1. Tool: GDB
                    A.2.2. Tool: ps
                    A.2.3. Tool: strace (system call tracer)
                    A.2.4. Tool: /proc filesystem
                    A.2.5. Tool: DDD (Data Display Debugger)
                    A.2.6. Tool: lsof (List Open Files)
                    A.2.7. Tool: ltrace (library call tracer)
                    A.2.8. Tool: time
                    A.2.9. Tool: top
                    A.2.10. Tool: pstree
A.3. Network
                    A.3.1. Tool: traceroute
                    A.3.2. File: /etc/hosts
                    A.3.3. File: /etc/services
                    A.3.4. Tool: netstat
                    A.3.5. Tool: ping
                    A.3.6. Tool: telnet
                    A.3.7. Tool: host/nslookup
                    A.3.8. Tool: ethtool
                    A.3.9. Tool: ethereal
                    A.3.10. File: /etc/nsswitch.conf
                    A.3.11. File: /etc/resolv.conf
A.4. System Information
                    A.4.1. Tool: vmstat
                    A.4.2. Tool: iostat
                    A.4.3. Tool: nfsstat
                    A.4.4. Tool: sar
                    A.4.5. Tool: syslogd
                    A.4.6. Tool: dmesg
                    A.4.7. Tool: mpstat
                    A.4.8. Tool: procinfo
                    A.4.9. Tool: xosview
A.5. Files and Object Files
                    A.5.1. Tool: file
                    A.5.2. Tool: ldd
                    A.5.3. Tool: nm
                    A.5.4. Tool: objdump
                    A.5.5. Tool: od
                    A.5.6. Tool: stat
                    A.5.7. Tool: readelf
                    A.5.8. Tool: strings
A.6. Kernel
                    A.6.1. Tool: KDB
                    A.6.2. Tool: KGDB
                    A.6.3. Tool: ksymoops



```
