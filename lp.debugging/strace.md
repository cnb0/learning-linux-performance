 
 ## [strace](https://strace.io/)
 
```
1. attach to an already running process.

     -e trace=%desc     Trace all file descriptor related system calls.
         %file     Trace all system calls which take a file name as an argument.
         %fstat    Trace fstat and fstatat syscall variants.
         %fstatfs  Trace fstatfs, fstatfs64, fstatvfs, osf_fstatfs, and osf_fstatfs64 system calls.
         %ipc      Trace all IPC related system calls.
         %lstat    Trace lstat syscall variants.
         %memory   Trace all memory mapping related system calls.
         %network  Trace all the network related system calls.
         %process  Trace all system calls which involve process management.
         %pure     Trace syscalls that always succeed and have no arguments.
         %signal   Trace all signal related system calls.
         %stat     Trace stat syscall variants.
         %statfs   Trace statfs, statfs64, statvfs, osf_statfs, and osf_statfs64 system calls.
         %%stat    Trace syscalls used for requesting file status.
         %%statfs  Trace syscalls related to file system statistics.


        - The output from strace will correspond to either a system call or signal. 
                - The output from a system call is comprised of three components:

                       Ex: select(1, NULL, NULL, NULL, {83009, 275934}
                        - The system call
                        - Any arguments surrounded by parenthesis
                        - The result of the call following an equal sign
            
        - Attach to an existing process
            $ strace -p 26380
            $ strace df -h            
                
2. Trace only system calls accessing given path.

            $ strace -P /etc/ld.so.cache ls /var/empty


3. Perform a full hexadecimal and ASCII dump of all the data read from/written to file descriptors

            $ strace -ewrite=1 -e trace=sendmsg ./recvmsg > /dev/null

4. Perform a syscall fault injection.
            $ strace -e trace=open -e fault=open cat

5. Count time, calls, and errors for each system call
        $ strace -c ls > /dev/null


6.  Redirecting trace to a file
        - trace any forked child processes, and record all file access to the files.trace file:
            $ strace -f -o files.trace -e trace=file bash

7. Counting number of sys calls


    - System call report/summary
             $ strace -c ifconfig eth0
             $ strace -e open ifconfig eth0
             $ strace -e trace=mprotect,brk ifconfig eth0
             $ strace -e trace=network ifconfig eth0


8 Get timestamps operation and time calls
        - Relative timestamp upon entry to each system call.
                $ strace -r -o strace_r.txt ifconfig eth0 > /dev/null
        - Prefix each line of the trace with the time of day.
                $ strace -t -o strace_t.txt ifconfig eth0 > /dev/null
        - Time printed will include the microseconds.
                $ strace -tt -o strace_tt.txt ifconfig eth0 > /dev/null
        - Time printed will include the microseconds and the leading portion will be printed as the number of seconds since the epoch.
                $ strace -ttt -o strace_ttt.txt ifconfig eth0 > /dev/null
                
9. follow system calls if a process fork, -f option follows child process
        $ strace -f -o strace_acroread.txt acroread > /dev/null

10. Viewing files opened by a process/daemon
        $ strace -f -eopen /usr/sbin/sshd 2>&1 | grep ssh

11. Tracing only network related system calls
        $ strace -e trace=network nc localhost 23

