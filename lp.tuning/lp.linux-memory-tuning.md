
## Tune the Linux kernel for memory performance

```

- The linux kernel attempts to optimize RAM utilization, in that it occupies 
  unused RAM with caches. This is done on the basis that unused RAM is wasted RAM.

- Over time the kernel will fill the RAM with cache.
- As more memory is required by the applications/buffers, 
  the kernel goes through the cache memory pages and 
  finds a block large enough to fit the requested malloc. 
  It then frees that memory and allocates it to the calling application.

- Under some circumstances, this can affect the general performance of the system as 
  cache de-allocation is time-consuming in comparison with access to unused RAM.
  Higher latency could therefore sometimes be observed.

- This latency will purely be based on the fact that RAM is being used to its full speed potential. 
  As such, no other symptoms may occur apart from general overall and potentially sporadic latency increases. 
  The equivalent would be similar to symptoms that may be observed if the hard disks are 
  not keeping up with reads and writes. 

- As such this may show network-based latency instead.

- The kernel memory cache contains the following:

        - dirty cache  
                 - Data blocks not yet committed to the file systems which support caching (e.g. ext4). 
                 - This can be emptied by issuing the sync command athough this may imply a periodic performance penalty. 
                   This is not advised for normal usage unless it is extremely important to commit data to hard drive 
                   (for example when expecting a failure).
        - clean cache 
                - Data blocks which are on the hard drive but are also retained in memory for fast access. 
                  Dropping the clean cache can result in a performance deficit as all data will read from disk, 
                  whereas beforehand, the frequently used data would be fetched directly from RAM.
        - inode cache 
                - Cache of the inode location information. 
                   This can be dropped as with clean cache but with the attendant performance penalty.
        - slab cache 
                - This type of cache stores objects allocated via malloc by applications so that they 
                  may be re-malloc again in the future with object data already populated, 
                  resulting in speed gain during memory allocations.


- While not much can be done with dirty cache, the other cached objects can be cleared. 
        - This has potentially 2 outcomes. 
                - Latency in high-malloc applications, storing data in memory, will be reduced. 
                - disk access may slow down, as all data will have to be read from disk.

- Clearing slab cache on a server can potentially introduce a temporary speed penalty (spike). 
        - For this reason, it is not advised to clear caches. 
        - Instead, it is preferred to inform the system that a certain amount of RAM should never be occupied by cache.
        - If necessary, clearing the cache can be performed as follows:

                - clear page cache (above type clean cache and inode cache)
                        $ echo 1 > /proc/sys/vm/drop_caches

                - clear slab cache 
                        $ echo 2 > /proc/sys/vm/drop_caches

                - clear page and slab cache (types 2,3,4)
                        $ echo 3 > /proc/sys/vm/drop_caches


        - Most of the space will be occupied by page cache, not slab cache.
        - It is recommended that when clearing cache, to only drop the page cache (echo 1).


- Fine-tuning these parameters is dependant upon the current utilization. 
        - if application requires least 1.1GB free in min_free_kbytes, if the available system memory allows. 
            - This means that caches will still operate sufficiently, while leaving a margin for applications to allocate into.
                $ echo 3145728 > /proc/sys/vm/min_free_kbytes

        - You should leave no more than 3% of spare memory to min_free_kbytes in order to avoid the kernel 
        spending too much time unnecessarily reclaiming memory. 
        This would equal anywhere between 1.1GB and 3% of total RAM on such systems.

        - Caution should be exercised when setting this parameter, both too low and too 
            high values can have an adverse effect upon system performance. 
            Setting min_free_kbytes too low prevents the system from reclaiming memory. 
            This can result in system hangs and OOM kills of processes.
         - Setting this parameter to a value that is too high (5-10% of total system memory) 
           will cause the system to run out of memory immediately. 
         - Linux is designed to use all available RAM to cache file system data. 
           Setting a high min_free_kbytes value results in the system spending too much time reclaiming memory.
         - As standard keep min_free_kbytes at 1-3% of the total memory on the system,

- It is advised to either reduce swappiness to 0 or not use swap. 
    - For low-latency operations, using swap to any extent will drastically slow down performance.
    - To set the swappiness to 0 to reduce potential latency:
        $ echo 0 > /proc/sys/vm/swappiness


```
