Project 5 Cache Simulator

Project Description:

Cache memories are hard to understand!  One way to understand them is to 
actually build a cache.  We do not have time to do this in this class.  
However, writing a simulator for a cache can also make caches easier to 
understand.  So in this project, you will design a cache simulator and 
use it to see the effect of various cache design parameters on performance.

You will start by designing a data structure that will hold all meta data 
for a cache. This data structure will be dynamically allocated by a function 
called allocate_cache. The function will take in parameters: C, B, S, WP where 
the cache allocated has 2^C bytes of total data storage, having 2^B-byte blocks, 
and with sets of 2^S blocks per set (note that S=0 is a direct-mapped cache, 
and S = C - B is a fully associative cache). The cache implements one of two 
write policies (WP): write through (WTWNA/WTNA) or write back (WBWA) (sometimes 
called copy back). In the case of write back there will be a dirty bit per tag. 
There is a valid bit for each tag entry that specifies whether or not this entry 
in the cache has been accessed. When the simulator starts, all valid bits are 
set to false (0).) The size of an address is 32 bits. Note: The cache data 
structure may contain the values of C, B, S, and WP if you find it necessary.

The allocate_cache function will return a pointer to the cache data structure.

You will then implement functions called student_read and student_write. This 
function will take in as parameters: the address, a pointer to a statistics 
storage structure, and a pointer to a cache data structure. The functions will 
return a number indicating whether the result was a hit or a miss.

Note: When simulating caches you don't have to actually store any actual data. 
The simulation just operates on the cache meta data.

We will supply you with "trace" files which contain data recorded from actual 
runs of benchmark programs. These files will be in this format:

r|w <hex address>
r|w <hex address>
...

Example:

r ffe04540
r ffe04544
w 0eff2340
r ffe04548 

A main function which will call the allocate_cache function and then will enter 
the main simulation loop where it will read from one of the supplied trace files 
and call the cache access functions has been provided.

The statistics you need to record are:

   1   number of accesses to the cache
   2   number of reads
   3   number of read misses
   3.5 number of read hits
   4   number of writes
   5   number of write misses (note that write misses will be equal to zero if WP = WTNA)
   5.5 number of write hits
   6.  total number of bytes transferred to and from memory.
   7.  total number of misses (when WP = WTNA, writes that are not in the cache do not count as misses)
   8.  cache read hit rate, which equals (number of read hits)/(number of reads to the cache)
   8.5 overall cache hit rate, (total hits)/(total accesses)
   9.  total number of bits of cache storage, including all data storage, tag storage, valid and dirty bits.

In addition, report the following for the overall memory system:

The Actual memory access time (AAT) assuming:

    * a miss penalty of 50 ns, and
    * a hit time of 2+0.2*S ns (where there are 2^S blocks per set).

The average access time equation is:

AAT = Hit time + Read miss rate x Miss penalty 

For this project you will only be required to simulate single caches. That is 
main will read a line from a trace file, call the cache access functions and 
tabulate the appropriate statistics. When you have this working you may choose 
to simulate multi-level caches. Your cache data structure (L1) will have another 
cache structure stored in it (L2) then your simulation will read a line from the 
trace file, call cache access on the L1 and if the result is a miss you will 
call cache access again only this time on the L2 cache data structure. In the 
case of multi-level caches you should produce statistics by cache and a total 
for the system. If you choose to implement a multi-level cache, you will need to 
modify the statistics printing function. These modifications should be done in 
such a way as to allow the output to stay the same in the case of a single level 

Analysis

First, validate that your cache is working with trace files and 
results supplied by the TA's.
(running diff on the output should cause no lines returned)

Second, design a single level cache system for each provided trace subject to 
the following goals (running all traces in the trace directory) 
 

   1. You have a total budget of 48KB for the entire cache system's storage 
      (including all data storage, tag storage, dirty and valid bits).
   2. The cache should have the lowest possible AAT.

You may vary any parameter (C, B, S, WP).  

Optionally, design a two-level cache system where you have 48KB for the L1 
system's storage (including all data storage, tag storage, dirty and valid bits) 
and you have 512 Kb for the L2 system's storage (including all data storage, tag 
storage, dirty and valid bits)

In the case of a two level cache:

    Hit time for level 1 is 2+0.2*S ns (where there are 2^S blocks per set).
    
    Hit time for level 2 is 6+0.25*S ns (where there are 2^S blocks per set).
    
    Miss penalty for Level 1 is the AAT for the level 2.
    
    Miss penalty for Level 2 is 150 ns.
    
Validation Requirement

Sample simulation outputs will be provided on the website by the TAs. You must 
run your simulator and debug it until it matches 100% all the statistics in the 
validation outputs posted on the website. You are required to hand in this 
validated output with your project.

What to hand in via T-Square:

   1. Output from your simulation showing it matches 100% all the statistics in 
      the validation outputs posted on the website, for each validation run.
   2. The design results of the experiments for each trace file. During demos 
      you will be required to supply persuasive arguments of the choices that 
      were made. (An argument may be as simple as an explanation of the search 
      procedure used to find the designs and a statement about why the procedure 
      is complete.)  
   3. The commented source code for everything you write.
   4. You must turn in your project a tarball called lastname_firstname.tar.gz.
   Replace firstname and lastname with your actual first name and last name...
   
NOTE: This is a simulation. You do not actually store any data in your caches. 
Just the meta data that would be used to correctly operate your cache.   
