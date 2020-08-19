# Linux performance monitoring process and tools

```
- Automate the display and collection of periodic performance data (bash, watch).
- Record all commands and output displayed during a performance investigation (tee, script).
- Import, analyze, and graph performance data (gnumeric).
- Determine the libraries that an application is using (ldd).
- Determine which functions are part of which libraries (objdump).
- Investigate runtime characteristics of an application (gdb).
- Create performance tool/debugging-friendly applications (gcc).

- Automating and Recording Commands
- Graphing and Analyzing Performance Statistics
- Investigating the Libraries That an Application Uses
- Creating and Debugging Applications

- linux loadavg
    - Linux load averages are "system load averages" that show the running thread (task)
      demand on the system as an average number of running plus waiting thread
      
        $ uptime
            16:48:24 up  4:11,  1 user,  load average: 25.25, 23.40, 23.46
            top - 16:48:42 up  4:12,  1 user,  load average: 25.25, 23.14, 23.37
        $ cat /proc/loadavg 
            25.72 23.19 23.35 42/3411 43603

            - If the averages are 0.0, then your system is idle.
            - If the 1 minute average is higher than the 5 or 15 minute averages, 
              then load is increasing.
            - If the 1 minute average is lower than the 5 or 15 minute averages, 
              then load is decreasing.
            - If they are higher than your CPU count, then you might have a 
              performance problem (it depends).

       - As a set of three, you can tell if load is increasing or decreasing
       - They can be also useful when a single value of demand is desired, 
         such as for a cloud auto scaling rule.
       - But to understand them in more detail is difficult without the aid of other metrics.
       - A single value of 23 - 25, by itself, doesn't mean anything, but might 
        mean something if the 
         CPU count is known, and if it's known to be a CPU-bound workload.

- On Linux, load averages are or "system load averages", for the system as a whole, 
  measuring the number of threads that are working and waiting to work 
  (CPU, disk, uninterruptible locks). 
  Put differently, it measures the number of threads that aren't completely idle. 
  Advantage: includes demand for different resources.


# Better Metrics

- When Linux load averages increase, you know you have higher demand for resources 
  (CPUs, disks, and some locks)

        - per-CPU utilization: eg, using mpstat -P ALL 1
        - per-process CPU utilization: eg, top, pidstat 1, etc.
        - per-thread run queue (scheduler) latency: eg, in /proc/PID/schedstats, delaystats, perf sched
        - CPU run queue latency: eg, in /proc/schedstat, perf sched, my runqlat bcc tool.
        - CPU run queue length: eg, using vmstat 1 and the 'r' column, or my runqlen bcc tool.

- Finding out system bottlenecks
- Disk (storage) bottlenecks
- CPU and memory bottlenecks
- Network bottleneck

            - Process activity monitoring command
                    $ top
            - Virtual memory statistics
                    $ vmstat -m  # Display Memory Utilization Slabinfo
            - Get Information About Active / Inactive Memory Pages
                    $ vmstat -a 
            - Find out who is logged on and what they are doing
                    $ w <user_name>
            - Tell how long the Linux system has been running
                    $ uptime
            - Displays the Linux processes
                    $ ps -Al
                    $ ps -alF

                - Display Threads ( LWP and NLWP)
                    $ ps -AlFH

                - Watch Threads After Processes
                    $ ps -AlLm

                - Print All Process On The Server
                    $ ps aux

                - Print A Process Tree?
                    $ ps -ejH
                    $ ps axjf
                    $ pstree

                - Get Security Information of Linux Process
                    $ ps -eo euser,ruser,suser,fuser,f,comm,label
                    $ ps axZ
                    $ ps -eM
                - Let Us Print Every Process Running As User
                    $  ps -U vivek -u vivek u
                - Configure ps Command Output In a User-Defined Format
                    $ ps -eo pid,tid,class,rtprio,ni,pri,psr,pcpu,stat,wchan:14,comm
                    $ ps axo stat,euid,ruid,tty,tpgid,sess,pgrp,ppid,pid,pcpu,comm
                    $ ps -eopid,tt,user,fname,tmout,f,wchan

                - Try To Display Only The Process IDs of Lighttpd
                    $ ps -C lighttpd -o pid=
                    $ pgrep lighttpd
                    $ pgrep -u vivek php-cgi
                
                 - Print The Name of PID 54566
                           $ ps -p 54566 -o comm=
                 - Top 10 Memory Consuming Process
                            $ ps -auxf | sort -nr -k 4 | head -10
                 - Show Us Top 10 CPU Consuming Process
                            $ ps -auxf | sort -nr -k 3 | head -10
            - free – Show Linux server memory usage

- /proc/ file system – Various Linux kernel statistics
        cat /proc/cpuinfo
        cat /proc/meminfo
        cat /proc/zoneinfo
        cat /proc/mounts

- iostat – Montor Linux average CPU load and disk activity

- sar – Monitor, collect and report Linux system activity
    - sar command used to collect, report, and save system activity information. 
      To see network counter,
           $ sar -n DEV | more

    - You can also display real time usage using sar:
            $ sar 4 5
- mpstat – Monitor multiprocessor usage on Linux
        mpstat command displays activities for each available processor, 
         processor 0 being the first one. 
            - to display average CPU utilization per processor:
                $ mpstat -P ALL
- pmap – Montor process memory usage on Linux
            - pmap command report memory map of a process. 
            - Use this command to find out causes of memory bottlenecks.
                # pmap -d PID
- netstat – Linux network and statistics monitoring tool
           - netstat command displays network connections, routing tables, 
             interface statistics, masquerade connections, and multicast memberships.
                $ netstat -tulpn
                $ netstat -nat
-  iptraf – Get real-time network statistics on Linux
            - Network traffic statistics by TCP connection
            - IP traffic statistics by network interface
            - Network traffic statistics by protocol
            - Network traffic statistics by TCP/UDP port and by packet size
            - Network traffic statistics by Layer2 address

- tcpdump – Detailed network traffic analysis

        - tcpdump command is simple command that dump traffic on a network. 
            - good understanding of TCP/IP protocol to utilize this tool.
             For.e.g to display traffic info about DNS, enter:
                $ tcpdump -i eth1 'udp port 53'

                - Print all HTTP session to 192.168.1.5:
                    $ tcpdump -ni eth0 'dst 192.168.1.5 and tcp and port http'
-  iotop – Linux I/O monitor
        - iotop command monitor, I/O usage information, using the Linux kernel. 
        - It shows a table of current I/O usage sorted by processes or threads on the server.
            $ sudo iotop
-  htop – interactive process viewer
-  atop – Advanced Linux system & process monitor
    - atop is a very powerful and an interactive monitor to view the load on a Linux system.
       It displays the most critical hardware resources from a performance point of view. 
       You can quickly see CPU, memory, disk and network performance. 
     - It shows which processes are responsible for the indicated load concerning CPU and 
       memory load on a process level.

- ac and lastcomm –
        You must monitor process and login activity on your Linux server. The psacct or acct package
         contains several utilities for monitoring process activities, including:
        - ac command : Show statistics about users’ connect time
        - lastcomm command : Show info about about previously executed commands
        - accton command : Turns process accounting on or off
        - sa command : Summarizes accounting information

- nethogs- Find out PIDs that using most bandwidth on Linux
        - NetHogs is a small but handy net top tool. 
        - It groups bandwidth by process name such as Firefox, wget and so on. 
         - If there is a sudden burst of network traffic, start NetHogs. You will see which 
           PID is causing bandwidth surge.
            $ sudo nethogs

-  iftop – Show bandwidth usage on an interface by host
        - iftop command listens to network traffic on a given interface name such as eth0.
             It displays a table of current bandwidth usage by pairs of hosts.
                $ sudo iftop
-  vnstat – A console-based network traffic monitor
        - vnstat is easy to use console-based network traffic monitor for Linux.
             It keeps a log of hourly, daily and monthly network traffic for the selected interface(s).
               $ vnstat
- nmon – Linux systems administrator, tuner, benchmark tool
           - nmon is a Linux sysadmin’s ultimate tool for the tunning purpose.
             It can show CPU, memory, network, disks, file systems, NFS, top process resources and 
             partition information from the cli.
                $ nmon

- Nagios – Linux server/network monitoring
- Cacti – Web-based Linux monitoring tool


```
