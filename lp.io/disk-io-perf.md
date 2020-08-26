## Linux and Unix Test Disk I/O Performance With dd Command
```
- dd command on a Linux to test I/O performance of my hard disk drive? 
- How do I check the performance of a hard drive including the read and write speed on a Linux operating systems? 
- How can I use the dd command under Linux I/O performance test?

- simple sequential I/O performance test:

dd command :
          - It is used to monitor the writing performance of a disk device on a Linux and Unix-like system.
hdparm command : 
          - It is used to get/set hard disk parameters including test the reading and caching performance 
                 of a disk device on a Linux based system.

- Use dd command to monitor the reading and writing performance of a disk device:
  - Use the dd command to measure server throughput (write speed) 
        - $ dd if=/dev/zero of=/tmp/test1.img bs=1G count=1 oflag=dsync
  - Use the dd command to measure server latency 
        - $ dd if=/dev/zero of=/tmp/test2.img bs=512 count=1000 oflag=dsync


        - $ dd if=/dev/input.file  of=/path/to/output.file  bs=block-size  count=number-of-blocks  oflag=dsync
           ## GNU dd syntax ##
           ##########################################################
           ##***[Adjust bs and count as per your needs and setup]**##
           ##########################################################
           dd if=/dev/zero of=/tmp/test1.img bs=1G count=1 oflag=dsync
           dd if=/dev/zero of=/tmp/test2.img bs=64M count=1 oflag=dsync
           dd if=/dev/zero of=/tmp/test3.img bs=1M count=256 conv=fdatasync
           dd if=/dev/zero of=/tmp/test4.img bs=8k count=10k
           dd if=/dev/zero of=/tmp/test4.img bs=512 count=1000 oflag=dsync
           ## OR alternate syntax for GNU/dd ##
           dd if=/dev/zero of=/tmp/testALT.img bs=1G count=1 conv=fdatasync
           
- Finding server latency time 
   - 512 bytes were written one thousand times to get RAID10 server latency time:
       $ dd if=/dev/zero of=/tmp/test2.img bs=512 count=1000 oflag=dsync
       
- But why the server throughput and latency time are so low?
   - Low values does not mean you are using slow hardware. 
     The value can be low because of the HARDWARE RAID10 controller’s cache.
     
     
- Use dd command on Linux to test read speed
    To get accurate read test data, first discard caches before testing by running the following commands:
        $ flush
        $ echo 3 | sudo tee /proc/sys/vm/drop_caches
        $ time dd if=/path/to/bigfile of=/dev/null bs=8k
        
- Use hdparm command to see buffered and cached disk read speed
      - run the following commands 2 or 3 times Perform timings of device reads 
        for benchmark and comparison purposes:

      ### Buffered disk read test for /dev/sda ##
     - hdparm -t /dev/sda1
     - hdparm -t /dev/sda
        - To perform timings of cache reads for benchmark and comparison purposes 
          again run the following command 2-3 times (note the -T option):

        -  ## Cache read benchmark for /dev/sda ###
          $ hdparm -T /dev/sda1
          ## OR ##
          $ hdparm -T /dev/sda
          
          OR combine both tests:
          $ hdparm -Tt /dev/sda  
  
  
 -  Which method and command do you recommend to use to test disk I/O performance?
     - dd command on all Unix-like systems (time sh -c "dd if=/dev/zero of=/tmp/testfile bs=100k count=1k && sync"
     - If you are using GNU/Linux use the dd command (dd if=/dev/zero of=/tmp/testALT.img bs=1G count=1 conv=fdatasync)
     - Make sure you adjust count and bs arguments as per your setup to get a good set of result.
     - The GUI method is recommended only for Linux/Unix laptop users running Gnome 2 or 3 desktop.
     -  For detailed I/O performance benchmarking use the fio command
     -  IOzone. It is a filesystem benchmark tool. The benchmark generates and measures a variety of file operations.
