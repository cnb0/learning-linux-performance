
# Performance Tools: Disk I/O
```
 - gauge disk I/O subsystem usage

 - These tools can show which disks or partitions are being used, how much I/O each disk is processing, 
 - how long I/O requests issued to these disks are waiting to be processed.
 - we should be able to Determine the amount of total amount and type (read/write) 
   of disk I/O on a system (vmstat).
 
 - determine which devices are servicing most of the disk I/O (vmstat, iostat, sar).
 - determine how effectively a particular disk is fielding I/O requests (iostat).
 - determine which processes are using a given set of files (lsof).

 - Linux disk I/O performance tools used to extract information about system-wide (vmstat), 
   device-specific (vmstat, iostat, sar), and 
   file-specific (lsof) disk I/O usage. 
-  different types of I/O statistics and 
   extract these statistics from Linux using the I/O performance tools


 vmstat disk I/O Statistics

 $ vmstat -D
 $ vmstat -d 1 3
 $ vmstat -p hde3 1 3


 $ iostat -d 1 2
 $ iostat -x -dk 1 5 /dev/hda2


- sar is used to collect information about the I/O of the devices on the system. 
- sar lists the devices by their major and minor number rather than their names


 $ sar -d [ interval [ count ] ]
 $ sar -d 1 3

- lsof (List Open Files)
    - lsof provides a way to determine which processes have a particular file open. 
    - In addition to tracking down the user of a single file, 
      lsof can display the processes using the files in a particular directory. 
    - It can also recursively search through an entire directory tree and
      list the processes using files in that directory tree. 
      
      lsof can prove helpful when narrowing down which applications are generating I/O

      lsof [-r delay] [+D directory] [+d directory] [file]

    - lsof displays which processes are using a given file

      - lsof -r 2 +D /usr/bin/

    - lsof to determine which processes are accessing files on a particular partition
    - After you list all PIDs accessing the files, you can then attach to each of the PIDs with strace and 
       figure out which one is doing a significant amount of I/O. Although this method works, 
       it is really a Band-Aid solution,
       because the number of processes accessing a partition could be large and 
       it is time-consuming to attach and analyze the system calls of each process. 
       This may also miss short-lived processes, and may unacceptably slow down processes 
       when they are being traced.
       This is an area where the Linux kernel could be improved. 
    - The ability to quickly track which processes are generating I/O would allow for much 
       quicker diagnosis of I/O performance-related problems.
