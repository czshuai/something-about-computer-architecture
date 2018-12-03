# Ten Advanced Optimizations of Cache Performance
### First Optimization: Small and Simple First-Level Caches to Reduce Hit Time and Power
The critical timing path in a cache hit is the three-step process:
1. Addressing the tag memory using the index portion of the address.
2. Comparing the read tag value to the address.
3. Setting the multiplexor to choose the correct data item if the cache is set associative.

The size of the L1 caches has recently increased either slightly or not at all due to the ***clock rate impact*** arising from a larger L1 cache. So designers have opted for more associativity rather than larger caches.   
   
***Access time(hit time) and energy consumption*** are the consideration in choosing both the cache size and associativity.
   
In recent design, there are three other factors that have led to the ues of higher associativity in first-level caches.
- Many processors take at least two clocks to access the cache and thus the impact of a longer hit time may not be critical.
- To keep the TLB out of the critical path, almost all L1 caches should be virtually indexed.
- With the introduction of multithreading, conflict misses can increase, making higher associativity more attractive.

---
### Second Optimization: Way Prediction to Reduce Hit Time
In ***way prediction***, extra bits are kept in the cache to predict the way, or block within the set of the next cache access. The approach ***reduces conflict misses*** and yet ***maintains the hit speed of direct-mapped cache***.    
   
***Way selection***, an extended form of way prediction, can be used to reduce power consumption by using the way prediction bits to decide which cache block to actually access (the way prediction bits are essentially extra address bits).

---
### Third Optimization: Pipelined Cache Access to Increase Cache Bandwith
This optimization is simply to pipeline cache access so that ***the effective latency of a first-level cache hit can be multiple clock cycles***, giving fast clock cycle time and high bandwidth but slow hits.

---
### Fourth Optimization: Nonblocking Caches to Increase Cache Bandwith
A ***nonblocking cache or lockup-free cache*** escalates the potential benefits of such a scheme by allowing the data cache to continue to supply cache hits during a miss. ("hit under miss" optimization)   
   
A subtle and complex option is that the cache may further lower the effecitive miss penalty if it can ***overlap multiple misses***. ("hit under multiple miss" or "miss under miss" optimization)   
   
Deciding how many outstanding misses to support depends on a variety of factors:
- The temporal and spatial locality in the miss stream.
- The bandwidth of the responding memory or cache.
- To allow more outstanding misses at the lowest level of the cache requires supporting at least that many misses at a higher level
- The latency of the memory system.

---
### Fifth Optimization: Multibanked Caches to Increase Cache Bandwidth
Rather than treat the cache as a simple monolithic block, we can divide it into independent banks that can support simultaneous accesses.    
   
***Sequential interleaving***， a simple mapping of addresses to banks that work well is to spread the addresses of the block sequentially across the banks.

---
### Sixth Optimization: Critical Word First and Early Restart to Reduce Miss Penalty
Don't wait for the full block to be loaded before sending the requested word and restarting the processor.Here are two specific strategies:
- ***Critical word first***: Request the missed word first from memory and send it to the processor as soon as it arrives; let the processor continue execution while filling the rest of the words in the block.
- ***Early restart***: Fetch the words in normal order, but as soon as the requested word of the block arrives send it to the processor and let the processor continue execution.

The benefits of these two strategies depend on the size of the block and the likelihood of another access to the portion of the block that has not yet been fetched.

---  
### Seventh Optimization: Merging Write Buffer to Reduce Miss Penalty
Write-through caches rely on write buffers, as all stores must be sent to the next lower level of the hierarchy.   
    
If the buffer contains other modified blocks, the addresses can be checked to see if the address of the new data matches the address of a valid write buffer entry.If so, the new data are combined with that entry.***Write merging*** is the name of this optimization.

---
### Eighth Optimization: Compiler Optimizations to Reduce Miss Rata
#### Loop Interchange 
Simply exchanging the nesting of the loops can make the code access the data in the order in which they are stored.
```
/* Before */
for (j = 0; j < 100; j = j + 1)
    for (i = 0; i < 5000; i = i + 1)
        x[i][j] = 2 * x[i][j];
```
```
/* After */
for (i = 0; i < 5000; i = i + 1)
    for (j = 0; j < 100; j = j + 1)
        x[i][j] = 2 * x[i][j];
```
#### Blocking
Instead of operating on entire rows or columns of an array, blocked algorithms operate on submatrices or blocks.
```
/* Before */
for (i = 0; i < N; i = i + 1)
    for (j = 0; j < N; j = j + 1) {
        r = 0;
        for (k = 0; k < N; k = k + 1)
            r = r + y[i][k] * z[k][j];
        x[i][j] = r;
    };
```
```
/* After */
for (jj = 0; jj < N; jj = jj + B)
for (kk = 0; kk < N; kk = kk + B)
for (i = 0; i < N; i = i + 1)
    for (j = jj; j < min(jj + B, N); j = j + 1) {
            r = 0;
            for (k = kk; k < min(kk + B, N); k = k + 1)
                r = r + y[i][k] * z[k][j];
            x[i][j] = x[i][j] + r;
    };
```
B is called the ***blocking factor***.

---
### Ninth Optimization: Hardware Prefetching of Instructions and Data to Reduce Miss Penalty or Miss Rate
This approach is to ***prefetch items before the processor requests them***. Both instructions and data can be prefetched, either directly into the caches or into an external buffer that can be more quickly accessed than main memory.
   
Prefetching relies on ***utilizing memory bandwidth*** that otherwise would be unused.

---
### Tenth Optimization: Compiler-Controlled Prefetching to Reduce Miss Penalty or Miss Rate
An alternative to hardware prefetching is for the compiler to insert prefetch instructions to request data before the processor needs it. There are two flavors of prefetch:
- ***Register prefetch*** will load the value into a register.
- ***Cache prefetch*** loads data only into the cache and not the register.

***non-faulting cache prefetches***.






