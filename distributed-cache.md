# Distributed Cache

What are Distributed CACHES and how do they manage DATA CONSISTENCY?
-----------------------------------------------------------------------------------------------------------

In Memory Caching
-
- Save memory cost - For commonly accessed data
- Avoid Re-computation - For frequent computation like finding average age
- Reduce DB Load - Hit cache before querying DB

Drawbacks of Cache
-
- Hardware (SSD) much more expensive than DB
- As we store more data on cache, search time increases (counter productive)

Design
-
- Database (Infinite information) vs Cache (Relevant information)

Cache Policy
-
- Least Recently Used (LRU) - Top entires are recent entries, remove least recently used entries in cache

Issue with caches
-
- Extra calls - When we couldn’t find entry in cache, we query from database.
- Threshing - Input and output cache without ever using results
- Consistency - When update DB, we must maintain consistency between cache and DB

Where to place the cache
-
- Close to server (in memory)
    - Benefit - Fast
    - Issue - Maintaining consistency between memory of different servers, especially for sensitive data such as password
- Close to DB (global cache, i.e. Redis)
    - Benefit - Accurate, Able to scale independently

Write-through vs Write-back
-
Write-through
  
	 data is simultaneously updated to cache and memory. This process is simpler and more reliable. This is used when there are no frequent writes to the cache(The number of write operations is less). 
	It helps in data recovery (In case of a power outage or system failure). A data write will experience latency (delay) as we have to write to two locations (both Memory and Cache). It Solves the inconsistency problem. But it questions the advantage of having a cache in write operation (As the whole point of using a cache was to avoid multiple access to the main memory). 
	
Write-back

	The data is updated only in the cache and updated into the memory at a later time. Data is updated in the memory only when the cache line is ready to be replaced (cache line replacement is done using Belady’s Anomaly, Least Recently Used Algorithm, FIFO, LIFO, and others depending on the application). 
	Write Back is also known as Write Deferred. 
	Dirty Bit: Each Block in the cache needs a bit to indicate if the data present in the cache was modified(Dirty) or not modified(Clean). If it is clean there is no need to write it into the memory. It is designed to reduce write operation to a memory. If Cache fails or if the System fails or power outages the modified data will be lost. Because it’s nearly impossible to restore data from cache if lost. 
	If write occurs to a location that is not present in the Cache(Write Miss), we use two options, Write Allocation and Write Around. 

Write Allocation:

	In Write Allocation data is loaded from the memory into cache and then updated. Write allocation works with both Write back and Write through. But it is generally used with Write Back because it is unnecessary to bring data from the memory to cache and then updating the data in both cache and main memory. Thus Write Through is often used with No write Allocate. 

Write Around:

	Here data is Directly written/updated to the main memory without disturbing the cache. It is better to use this when the data is not immediately used again.
	
	
