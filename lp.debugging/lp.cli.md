
## Linux Performance troubleshooting Commands

- [Linux perf debugging tools](https://lzone.de/cheat-sheet/Debugging)

```

- lsof 
        - “list open files” to help you to find all the opened files and processes 
           along with the one who opened them. 
        - The lsof utility can be convenient to use in some scenarios.

        - To list, all the files opened by particular PID

                $ lsof –p PID

         - Count number of files & processes
                $ lsof -p 34743 | wc -l
         - Check the currently opened log file
                $ lsof –p | grep log
          - Find out port number used by the daemon
                $ lsof -i -P |grep 4375

- pidstat
        - pidstat can be used to monitor tasks managed by the Linux kernel. 
        - Troubleshooting I/O related issues can be the ease with this command.
        - List I/O statistics of all the PID
            $ pidstat –d    
        - To displace I/O stats for particular PID
            $ pidstat –p 4356 –d

        - If we need real-time troubleshooting for some process, 
          then you can monitor the I/O in an interval. 
            -  example is to monitor every 5 seconds.
                $ pidstat -p 3335 -d 5
- top
        - used to display system summary information and current utilization.
        - show yous CPU utilization, process details, a number of tasks, memory utilization, a number of zombie processes, etc.
                $ top –u username

- ps
        - stands for process status and widely used a command to get a snapshot of the running process

- tcpdump
        - tcpdump to capture the network packets on a network interface.
            - captured the traffic flow on eth0 interface.
                - $ tcpdump -i eth0 -w /tmp/capture
            - To capture network traffic between source and destination IP
                - tcpdump src $IP and dst host $IP
            - Capture network traffic for destination port 443
                - tcpdump dst port 443
            - Read the captured file
                - tcpdump –r filename

- iostat
        - iostat stands for input-output statistics and often used to diagnose performance issue with storage devices. 
        - we can monitor CPU, Device & Network file system utilization report with iostat
                $ iostat -d
        - Display CPU statistics
                $ iostat -c
- ldd
        - ldd stands for list dynamic dependencies to show shared libraries needed by the library.
        - The ldd command can be handy to diagnose the application startup problem.

- netstat 
        - netstat (Network Statistics) is a popular command to print network connections, 
        - interface statistics and to troubleshoot various network related issue.
        - To show stats of all protocols
                $ netstat –s
        - To show kernel routing table
                $ netstat -r 

 - free
        - If your Linux server is running out of memory or just want to find out how much memory available out of available memory
            $ free -m

 - sar (System Activity Report) 
        - will be helpful to collect a number of a report including CPU, Memory and device load.
        -  executing sar command will show you system utilization for the entire day.
        - By default, it stores utilization report in 10 minutes.
        - Show CPU report for 3 times every 3 seconds
            $ sar 3 2 
        - Show Memory usage report
            $ sar -r
        - Show network report
            $ sar –n ALL
    
    - ipcs
        - ipcs (InterProcess Communication System) provides a report on the semaphore, shared memory & message queue.
        - To list the message queue
                $ ipcs –q
        - To list the semaphores
                $ ipcs –s
        - To list the shared memory
                $ ipcs –m
        - To display current usage status of IPC
                $ ipcs -u