


## Linux Network Commands Used In Network Troubleshooting

```
- Check network connectivity using the ping command
      $ ping google.com  
      $ ping -c 3 google.com
    - This command measures the average response. If there is no response, then maybe there is one of the following:
        - There is a physical problem on the network itself.
        - The location might be incorrect or non-functional.
        - The target is blocking the ping requests.
        - There is a problem with the routing table.
        - Distance to the target
        - The connection speed
        - The hop count

- dig - Get DNS records and host commands
      - To verify DNS mappings, host addresses, MX records, and all other DNS records for a 
        better understanding of DNS topography
           $ dig google.com
           $ dig google.com MX
           $ dig google.com ANY
           $ dig –x 8.8.8.8
           $ host –a google.com
           $ host 8.8.8.8

- traceroute - diagnose network latency  
      - To show the pathway to your target and where the delay comes from
      - Providing the names and the identity of every device on the path.
      - Reporting network latency and identify at which device the latency comes from.
      - The output will provide the specified host, the size of the packet, the IP address, and the number of hops
      - The traceroute command sends a UDP packet,  TCP, and ICMP.

       $ traceroute google.com
        - ICMP
            $ sudo traceroute -I google.com  
        - TCP
            $ sudo traceroute -T google.com 

- mtr command (realtime tracing)  -  it displays realtime data
            $ mtr google.com
        - sends ten packets to each hop found on its way
            $ mtr --report google.com

- ss- Checking connection performance 

    - The socket statistics command ss is a replacement for netstat, 
      it’s faster than netstat and gives more information.
    - The ss command gets its information directly from the kernel 
      instead of relying on /proc directory like netstat command.

         $ ss 
    - outputs all TCP, UDP, and UNIX socket connections and pipes
    -  -t to show TCP sockets or -u to show UDP or -x to show UNIX sockets
        $ ss -ta
    - To list all established TCP sockets for IPV4
         $ ss -t4 state established

    - To list all closed TCP states
        $  ss -t4 state closed

    - to show all connected ports from a specific IP
            $ ss dst 1.2.3.4
            $ $ ss dst 1.2.3.4:22



- iftop - for traffic monitoring
         
          $ sudo iftop -I <interface>
          - To show ports
          $ sudo iftop -P

- arp 

    - Systems keep a table of IP addresses and their corresponding MAC addresses; 
      this is the ARP lookup table. 
    - If you try to connect to an IP address, your router will check for your MAC address. 
      If your system caches it, the ARP table is not used.

      $arp 

- tcpdump - Packet analysis  
    - to capture the traffic that is passing through your network interface
      
      $ tcpdump -i <network_device>
      $ tcpdump -i <network_device> tcp
      $ tcpdump -i <network_device> port 80
      $ tcpdump -c 20 -i <network_device>
      - specify the IP to capture from using the src option or going to using the dst option
            $ tcpdump -c 20 -i <network_device> src XXX.XXX.XXX.XXX
      -  save the traffic captured from tcpdump to a file and read it later with -w option
            $ tcpdump -w /path/ -i <network_device>
            $ tcpdump -r /path
