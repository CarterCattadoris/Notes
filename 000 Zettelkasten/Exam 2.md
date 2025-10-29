202510281041
Status: #idea
Tags:[[CSE 381]]

**Given**

- Physical address: **32 bits**
    
- Total cache size: **64 KiB**
    
- Block size: **32 B**
    
- Mapping: **Direct-mapped (1-way)**

offset = $\log_{2}{(32B)} = 5B$
- offset = number of words/bytes per block (word/byte offset)

\# blocks = $\frac{64KiB}{32B} = \frac{65536}{32} = 2048$

index bits = $\log_2{(2048)} = 11$
- index bits = number of lines in direct mapped

tag bits = 32 - index bits - offset = 32 - 11 - 5 = 16
- remaining bits 

direct mapped cache mapping: Block address modulo num blocks in cache

Hit rate: The fraction of memory accesses found in a level of the memory hierarchy.
Miss rate: The fraction of memory accesses not found in a level of the memory hierarchy.

Hit time: The time required to access a level of the memory hierarchy, including the time needed to determine whether the access is a hit or a miss.

Miss penalty: The time required to fetch a block into a level of the memory hierarchy from the lower level, including the time to access the block, transmit it from one level to the other, insert it in the level that experienced the miss, and then pass the block to the requestor.

Flash memory is a type of _electrically erasable programmable read-only memory_ (EEPROM).

**L1 cache ONLY**
AMAT = time for a hit + miss rate x miss penalty

**L1 + L2**
AMAT = HT1 + MR1(HT2 + MR2 * MP2)

Fully associative cache: A cache structure in which a block can be placed in any location in the cache.

Set-associative cache: A cache that has a fixed number of locations (at least two) where each block can be placed.

set associative cache mapping: block number modulo number of sets in cache


**Miss Types**
Compulsory miss

capacity miss

conflict miss