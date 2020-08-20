    # Performance Tools: Network



- Determine the speed and duplex settings of the Ethernet devices in the system (mii-tool, ethtool).
- Determine the amount of network traffic flowing over each Ethernet interface (ifconfig, sar, gkrellm, iptraf, netstat, etherape).
- Determine the types of IP traffic flowing in to and out of the system (gkrellm, iptraf, netstat, etherape).
- Determine the amount of each type of IP traffic flowing in to and out of the system (gkrellm, iptraf, etherape).
- Determine which applications are generating IP traffic (netstat).
- how to use the Linux network performance tools to monitor the network traffic flowing through a system all the way from the low-level network interfaces to high-level applications

- Network Traffic in the Link Layer


- At the physical layer, frames flow over the physical network; 
        - The Linux kernel collects a number of different statistics about the number and types of frames:

        - Transmitted/received — If the frame successfully flowed in to or out of the machine, it is counted as a transmitted or received frame.
        - Errors    — Frames with errors (possibly because of a bad network cable or duplex mismatch).
        - Dropped   — Frames that were discarded (most likely because of low amounts of memory or buffers).
        - Overruns  — Frames that may have been discarded by the network card because the kernel or network card was overwhelmed with frames. 
                    This should not normally happen.
        - Frame     — These frames were dropped as a result of problems on the physical level. 
                    This could be the result of cyclic redundancy check (CRC) errors or other low-level problems.
        - Multicast — These frames are not directly addressed to the current system, but rather have been broadcast to a series of nodes simultaneously.

        - Several of the Linux network performance tools can display the number of frames of each type that have passed through each network device. 
        - These tools often require a device name, so it is important to understand how Linux names network devices to understand which name represents which device. 
        - Ethernet devices are named ethN, 
                - where eth0 is the first device, 
                - eth1 is the second devicen.
        - PPP devices are named pppN in the same manner as Ethernet devices. 
        - lo - The loopback device, which is used to network with the local machine

- Protocol-Level Network Traffic

    For TCP or UDP traffic, Linux uses the socket/port abstraction to connect two machines. When connecting to a remote machine, the local application uses a network socket to open a port on a remote machine. As mentioned previously, most common network services have an agreed-upon port number, so a given application will be able to connect to the correct port on the remote machine. For example, port 80 is commonly used for HTTP. When loading a Web page, browsers connect to port 80 on remote machines. The Web server of the remote machine listens for connections on port 80, and when a connection occurs, the Web server sets up the connection for transfer of the Web page.The Linux network performance tools can track the amount of data that flows over a particular network port. Because port numbers are unique for each service, it is possible to determine the amount of network traffic flowing to a particular service.

- Network I/O Performance Tools
    - mii-tool (Media-Independent Interface Tool)
            mii-tool [-v] [device]
        - mii-tool prints the Ethernet settings for the given device. 
        - If no devices are specified, mii-tool displays information about all the available Ethernet devices.
        -  If the -v option is used, mii-tool displays verbose statistics about the offered and negotiated network capabilities

            $ mii-tool -v eth0
    
- ethtool - 
        - provides similar capabilities to mii-tool for configuration and 
        - display of statistics for Ethernet devices. 
        - ethtool is the more powerful tool and contains more configuration options and device statistics.
        - ethtool provide information about an improperly configured network device.
        - configuration of eth0 on the system. 
            - Although the device supports many different speed and link settings, 
              it is currently connected to a full-duplex 1,000Mbps link

         $ ethtool eth0

- ifconfig (Interface Configure)
          
        - The primary job of ifconfig is to set up and configure the network interfaces in a Linux box
        - It also provides rudimentary performance statistics about all the network devices in the system.
        - If no device is specified, ifconfig shows statistics about all the active network devices.
        - provides a reasonable number of statistics that you can use to determine the health and 
          performance of each of the network devices in the system

        - The statistics provided by ifconfig represent the cumulative amount since system boot. 
        - If you bring down a network device and then bring it back up, the statistics do not reset. 
        - If you run ifconfig at regular intervals, you can eyeball the rate of change in the various statistics. 
        - You can automate this by using the watch command or a shell script 

            - ifconfig [device]

        - Performance-Specific ifconfig Statistics

            - RX packets - # of packets that this device has received.
            - TX packets - # of packets that this device has transmitted.
            - errors     - # of errors when transmitting or receiving.
            - dropped    - # of dropped packets when transmitting or receiving.
            - overruns   - # of times the network device did not have enough buffer space to send or receive a packet.
            - frame      - # of low-level Ethernet frame errors.
            - carrier    - # of packets discarded because of link media failure (such as a faulty cable).
 - ip 
        - ip enables you to configure many different aspect of Linux networking, 
          but it can also display performance statistics about each network device.
        - ip provides system totals for statistics since the system has booted
        - ip is a very versatile tool for Linux network configuration, and 
          although its main function is the configuration of the network, 
          you can use it to extract low-level device statistics as well.

            $ ip -s [-s] link
            $ ip -s link
            

        - It prints statistics about all the network devices in the system, including the loopback (lo) and 
        - simple Internet transition (sit0) device. The sit0 device allows IPv6 packets to be encapsulated in IPv4 packets and
          exists to ease the transition between IPv4 and IPv6. 
        - If the extra -s is provided to ip, it provides a more detailed list of low-level Ethernet statistics


          - bytes     The total number of bytes sent or received.
          - packets   The total number of packets sent or received.
          - errors    The number of errors that occurred when transmitting or receiving.
          - dropped   The number of packets that were not sent or received as a result of a lack of resources on the network card.
          - overruns  The number of times the network did not have enough buffer space to send or receive more packets.
          - mcast     The number of multicast packets that have been received.
          - carrier   The number of packets discarded because of link media failure (such as a faulty cable).
          - collsns   This is the number of collisions that the device experienced when transmitting. 
                      These occur when two devices are trying to use the network at the exact same time.  

- sar
        - It can monitor many different things, archive statistics, and even display information in a format that is usable by other tools. 
        - sar does not always provide as much detail as the area-specific performance tools, 
          but it provides a good overview.
        - Network performance statistics are no different.
        - sar provides information about the link-level performance of the network, as do ip and ifconfig; 
        - it also  provides some rudimentary statistics about the number of sockets opened by the transport layer.

            $ sar [-n DEV | EDEV | SOCK | FULL ] [DEVICE] [interval] [count]

            $ sar -n DEV 1 2
            $ sar -n SOCK 1 2


        - Shows statistics about the number of packets and bytes sent and received by each device.
                $ sar  -n DEV 
       - Shows information about the transmit and receive errors for each device.
                $ sar -n EDEV
       - Shows information about the total number of sockets (TCP, UDP, and RAW) in use.
                $ sar -n SOCK
       - Shows all the network statistics.
                $ sar -n FULL
       - The length of time between samples.
                $ sar interval
       - The total number of samples to take.
                $ sar count

                rxpck/s  The rate of packets received.
                txpck/s  The rate of packets sent.
                rxbyt/s  The rate of bytes received.
                txbyt/s  The rate of bytes sent.
                rxcmp/s  The rate of compressed packets received.
                txcmp/s  The rate of compressed packets sent.
                rxmcst/s The rate of multicast packets received.
                rxerr/s  The rate of receive errors.
                txerr/s  The rate of transmit errors.
                coll/s   The rate of Ethernet collisions when transmitting.
                rxdrop/s The rate of received frames dropped due to Linux kernel buffer shortages.
                txdrop/s The rate of transmitted frames dropped due to Linux kernel buffer shortages.
                txcarr/s The rate of transmitted frames dropped due to carrier errors.
                rxfram/s The rate of received frames dropped due to frame-alignment errors.
                rxfifo/s The rate of received frames dropped due to FIFO errors.
                txfifo/s The rate of transmitted frames dropped due to FIFO errors.
                totsck   The total number of sockets in use.
                tcpsck   The total number of TCP sockets in use.
                udpsck   The total number of UDP sockets in use.
                rawsck   The total number of RAW sockets in use.ip-fragThe total number of IP fragments.



- netstat
        - netstat is a basic network-performance tool that is present on nearly every Linux machine with networking. 
        - we can use it to extract information about the number and types of network sockets currently being used and interface-specific statistics
         regarding the number of UDP or TCP packets flowing to and from the current system.
        - It also enables you to trace the owner of a socket back to a particular process or PID, 
          which can prove useful when trying to determine the application responsible for network traffic.
        - netstat provides a great number of network performance statistics about sockets and
          interfaces in a running Linux system. 
        - It is the only network-performance tool that maps the sockets used back to the PID of the process that is using it 

          $ netstat [-p] [-c] [–interfaces=<name>] [-s] [-t] [-u] [-w]


        - If netstat is called without any parameters, it shows information about system-wide socket usage and 
          displays information about both Internet and UNIX domain sockets. 
          (UNIX domain sockets are used for interprocess communication on the local machine, but do not indicate network traffic.) 

        - To retrieve all the statistics that netstat is capable of displaying, you must run it as root
            $ netstat -t -c


        - print the TCP socket information, and display the program that is responsible for this socket
            $ netstat -t -p

        - provide statistics about the UDP traffic that the system has received since boot.
            $ netstat -s -u

        - provide information about the amount of network traffic flowing through the eth0 interface.
            $ netstat –interfaces=eth0