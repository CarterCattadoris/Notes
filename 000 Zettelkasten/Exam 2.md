202510281041
Status: #idea
Tags:[[CSE 381]]

**Given**

- Physical address: **32 bits**
    
- Total cache size: **64 KiB**
    
- Block size: **32 B**
    
- Mapping: **Direct-mapped (1-way)**

offset = $\log_{2}{(32B)} = 5B$

\# blocks = $\frac{64KiB}{32B} = \frac{65536}{32} = 2048$

index bits = $\log_2{(2048)} = 11$

tag bits = 32 - index bits - offset = 32 - 11 - 5 = 16

Hit rate: The fraction of memory accesses found in a level of the memory hierarchy.
Miss rate: The fraction of memory accesses not found in a level of the memory hierarchy.

Hit time: The time required to access a level of the memory hierarchy, including the time needed to determine whether the access is a hit or a miss.

Miss penalty: The time required to fetch a block into a level of the memory hierarchy from the lower level, including the time to access the block, transmit it from one level to the other, insert it in the level that experienced the miss, and then pass the block to the requestor.

Flash memory is a type of _electrically erasable programmable read-only memory_ (EEPROM).

