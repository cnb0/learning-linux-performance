
# Network 


 - netstat -s: Look for a high rate of retransmits and out-of-order packets. What constitutes a “high” retransmit rate depends on the clients: 
               an Internet-facing system with unreliable remote clients should have a higher retransmit
              rate than an internal system with clients in the same data center. 
 - netstat -i: Check interface error counters (specific counters depend on the OS version).
 - ifconfig : Check “errors,” “dropped,” “overruns.” 
 - Throughput: Check the rate of bytes transmitted and received—on Linux, via ip(8); 
               High throughput may hit line rate for the negotiated speed and be limited.
 - It could also cause contention and delays between network users on the system. 
 - tcpdump/snoop: While these can be expensive in terms of the CPU cost,
                  using them for short periods may be enough to see who is using the network and identify unnecessary work that can be eliminated. 
- perf: for selected packet inspection between the application and the wire, including examining kernel state.


 - USE Method
        - The USE method is for quickly identifying bottlenecks and errors across all components. 
        - For each network interface, and in each direction—transmit (TX) and receive (RX)—check for

     - Utilization: 
                - the time the interface was busy sending or receiving frames 
     - Saturation: 
                - the degree of extra queueing, buffering, or blocking due to a fully utilized interface 
     - Errors:
             - for receive: bad checksum, frame too short (less than the data link header) or too long, 
               collisions (unlikely with switched networks); for transmit: late collisions (bad wiring)