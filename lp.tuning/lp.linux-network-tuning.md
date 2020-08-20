

# Linux Network Tuning
    

```
-  Ubuntu Linux server out of box is not optimized to make full use of available hardware. 
   This means “out-of-box” setup might fail under high load.
-  So we need to tweak system configuration for maximum concurrancy.

- For servers which are handling large numbers of concurent sessions, 
  there are some TCP options that should probabaly be tweaked.

- List & reloading changes -  /etc/sysctl.conf
            $ sysctl --all
            $ sysctl --load

            - Show all system parameters with their values (default or changed)
                $ sysctl -A 
            - Show values of parameters modified by you
                $ sysctl -p


- GENERAL NETWORK SECURITY OPTIONS

                        - Summary details of each connection status
                                    $ netstat --numeric --tcp | tail --lines +3 | \
                                        awk "{n[\$6]++} END { for(k in n) { print k, n[k]; }}"

                        -  Number of times SYNACKs for passive TCP connection.
                                    net.ipv4.tcp_synack_retries = 2

                        - Protect Against TCP Time-Wait
                                    net.ipv4.tcp_rfc1337 = 1

                        - Decrease the time default value for tcp_fin_timeout connection
                                    net.ipv4.tcp_fin_timeout = 15

                        - Decrease the time default value for connections to keep alive
                                    net.ipv4.tcp_keepalive_time = 300
                                    net.ipv4.tcp_keepalive_probes = 5
                                    net.ipv4.tcp_keepalive_intvl = 15

                        - if a socket is listening and busy a connection-backlog will pile up. 
                          The kernel will keep pending connections in a buffer before failing
                                 - per-socket receive/send buffers
                                        - 16MB per socket - which sounds like a lot, but will virtually never
                                         consume that much.
                                                net.core.rmem_max = 16777216
                                                net.core.wmem_max = 16777216
                                        - Increase the number of outstanding syn requests allowed.
                                           c.f. The use of syncookies.
                                                net.ipv4.tcp_max_syn_backlog = 4096
                                                net.ipv4.tcp_syncookies = 1
                                        - The maximum number of "backlogged sockets".  Default is 128.
                                                net.core.somaxconn = 1024
                               - The trade-off here is that a connecting client will see a slow connection, 
                                 but this is almost certainly better than a Connection Refused error.     

                               - note : Finally if you've changed these limits you will need to restart
                                 the associated daemons. 
                                (For example "service nginx restart".)   

                        - per-socket receive/send buffers for TCP [min default max]
                                    net.ipv4.tcp_rmem = 4096 12582912 16777216
                                    net.ipv4.tcp_wmem = 4096 12582912 16777216
                                    #net.ipv4.tcp_rmem = 4096 87380 16777216
                                    #net.ipv4.tcp_wmem = 4096 65536 16777216
                                    #net.ipv4.tcp_rmem = 4096 16060 262144
                                    #net.ipv4.tcp_wmem = 4096 16384 262144

                        -  port range used by TCP and UDP to choose the local port
                                - With a large number of clients comnunicating with your server it wouldn't be unusual 
                                  to have a 20,000 open sockets or more. 
                                - To increase that range you append the following to the bottom of /etc/sysctl.conf:
                                    # default: net.ipv4.ip_local_port_range = 32768 60999
                                    net.ipv4.ip_local_port_range = 1024 65535

                        - various timewait socket setting tweaks
                                -  increase the recycling time of sockets, avoiding large numbers of them staying in the TIME_WAIT status
                                -  Enables fast recycling of TIME_WAIT sockets.
                                        # (Use with caution according to the kernel documentation!)
                                                  net.ipv4.tcp_tw_recycle = 1
                                                 
                                        # Allow reuse of sockets in TIME_WAIT state for new connections
                                        # only when it is safe from the network stack’s perspective.
                                                   net.ipv4.tcp_tw_reuse = 1
                                                   net.ipv4.tcp_max_tw_buckets = 400000
                                                   net.ipv4.tcp_max_orphans = 60000

                        - time that must elapse before TCP/IP can release an orphaned/closed connection and 
                          reuse its resources
                                            - default: net.ipv4.tcp_fin_timeout = 60
                                            - net.ipv4.tcp_fin_timeout = 30

                        - net.ipv4.tcp_syncookies enabled by default with Ubuntu 12.04LTS+
                                        net.ipv4.tcp_syncookies = 1

                        - remembered connection requests, without an ACK
                            - note: will increase automatically in proportion to available memory
                                        # default: net.ipv4.tcp_max_syn_backlog = 128
                                        net.ipv4.tcp_max_syn_backlog = 4096
                                        #net.ipv4.tcp_max_syn_backlog = 8096

                        - upper limit allowed for a listen() backlog
                        - maximum established sockets (with an ACK) waiting to be accepted by listening process
                                        # default: net.core.somaxconn = 128
                                        net.core.somaxconn = 1024
                                        net.core.somaxconn = 4096
                                        net.core.somaxconn = 8192

                        - give kernel more memory for TCP
                                        #net.ipv4.tcp_mem = 50576 64768 98152
                                        #net.core.netdev_max_backlog = 2500
                                        #net.core.netdev_max_backlog = 5000

                        - note: only need to tweak if ip_conntrack is used - e.g. stateful iptables rules
                                
                                        # default: net.ipv4.netfilter.ip_conntrack_max = 65536
                                        # net.ipv4.netfilter.ip_conntrack_max = 1048576


                        - Three system configuration parameters must be set to 
                                - support a large number of open files and 
                                - TCP connections  with large bursts of messages. 
                                    Changes can be made using the /etc/rc.d/rc.local or /etc/sysctl.conf 
                                    script to preserve changes after reboot.

                        1.  The maximum number of concurrently open files.
                                    $ cat /proc/sys/fs/file-max 
                                    fs.file-max = 1000000

                        2.  Maximum number of remembered connection requests, which are still did 
                            not receive an acknowledgment from connecting client. 
                            The default value is 1024 for systems with more than 128Mb of memory, and 
                            128 for low memory machines.
                                
                                    $ cat /proc/sys/net/ipv4/tcp_max_syn_backlog
                                        net.ipv4.tcp_max_syn_backlog = 3240000

                        3.  Limit of socket listen() backlog, known in userspace as SOMAXCONN. Defaults to 128.  
                                    $ /proc/sys/net/core/somaxconn
                                        net.core.somaxconn = 3240000

                        # Optional tuning 
                        
                        1. Increase system ip port limits to allow for more connections 
                                    $ cat /proc/sys/net/ipv4/ip_local_port_range: 
                                            net.ipv4.ip_local_port_range = 1024 65535

                        2. tcp send window,increasing the tcp send and receive buffers will increase the performance a lot if 
                           (and only if) you have a lot of large files to send.
                                    $ cat /proc/sys/net/ipv4/tcp_wmem and /proc/sys/net/core/wmem_max
                                            net.ipv4.tcp_wmem = 4096 65536 524288
                                            net.core.wmem_max = 1048576

                        3.  tcp receive window,If you have a lot of large file uploads, increasing the receive buffers will help.
                                $ /proc/sys/net/ipv4/tcp_rmem and /proc/sys/net/core/rmem_max
                                            net.ipv4.tcp_rmem = 4096 87380 524288
                                            net.core.rmem_max = 1048576

                        4. some parameter associated with tcp time wait
                                            net.ipv4.tcp_max_tw_buckets = 6000
                                            net.ipv4.tcp_tw_recycle = 1
                                            net.ipv4.tcp_tw_reuse = 1

                        5. some parameters associated with security
                                            net.ipv4.tcp_syncookies = 1
                                            net.ipv4.tcp_max_orphans = 262144


- TUNING NETWORK PERFORMANCE 

            - Default Socket Receive Buffer
                    net.core.rmem_default = 31457280

            - Maximum Socket Receive Buffer
                    net.core.rmem_max = 12582912

            - Default Socket Send Buffer
                    net.core.wmem_default = 31457280

            - Maximum Socket Send Buffer
                    net.core.wmem_max = 12582912

            - Increase number of incoming connections
                    net.core.somaxconn = 4096

            - Increase number of incoming connections backlog
                    net.core.netdev_max_backlog = 65536

            - Increase the maximum amount of option memory buffers
                    net.core.optmem_max = 25165824

            - Increase the maximum total buffer-space allocatable
            - This is measured in units of pages (4096 bytes)
                    net.ipv4.tcp_mem = 65536 131072 262144
                    net.ipv4.udp_mem = 65536 131072 262144

            - Increase the read-buffer space allocatable
                    net.ipv4.tcp_rmem = 8192 87380 16777216
                    net.ipv4.udp_rmem_min = 16384

            - Increase the write-buffer-space allocatable
                    net.ipv4.tcp_wmem = 8192 65536 16777216
                    net.ipv4.udp_wmem_min = 16384

            - Increase the tcp-time-wait buckets pool size to prevent simple DOS attacks
                    net.ipv4.tcp_max_tw_buckets = 1440000
                    net.ipv4.tcp_tw_recycle = 1
                    net.ipv4.tcp_tw_reuse = 1

```
[Linux](https://www.kernel.org/doc/Documentation/networking/ip-sysctl.txt)
[Linux tuning](https://bl.ocks.org/magnetikonline/2760f98f6bf654d5ad79)