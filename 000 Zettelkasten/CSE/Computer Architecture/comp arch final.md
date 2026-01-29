Units:
kilo = 10, mega = 20, giga = 30, terra = 40
microsecond = $10^{-6}$  -> 1 MHz cycle
nanosecond = $10^{-9}$ -> 1 GHZ cycle
picosecond = $10^{-12}$

Write through cache: write miss causes write to a lower memory level
Write back cache: write hit doesn't cause a write to lower memory level

Set associativity vs direct mapped:

page tables are NOT on special cache memory, TLBs ARE 

magnetic disks are non volatile

DRAM = optimized for density, SRAM for speed

split L1 cache for data and instructions to avoid structural hazards due to frequently accessing both at the same time

Equations:
$clockrate = \frac{CPI}{hit time}$

**L1 cache ONLY**
AMAT = time for a hit + miss rate x miss penalty

**L1 + L2**
$AMAT = HT1 + MR1(HT2 + MR2 * MP2)$

miss penalty = time/time per cycle
units are in cycles

## cache equations

cache block size: $2^{offset}$, 6 bit offset = $2^6$ = 64 bytes per block
number of blocks: $2^{index}$, 10 bit index = 1024 blocks


## multiple choice

1. snoopy bus: bus based, small scale systems with centralized main memory
2. false: scalar uniprocessor 
3. output data dependance
4. superscalar
5.  simultaneous multithreading
6. warp
7. 20 times
8.  0.6 + 0.6 + 0.3 = 1.5 CPI, 53.3 MIPS = CPI/MHz
9.  1 + 0.2(5 + 0.1 * 30) = 2.6
10. 1000
11. no, you would have the same AMAT more cost
12. 1 GB (2^12 * 2^18 = 2^30 = 1 GB)
13.  4 KiB (2^12)
14. 9.9 (0.6 * 1.1 * 15)
15. 2^6 = 64 per block, 2^10 1024 blocks
16. $\frac{1}{2x10^9} * 10$ = 500ns

--
1. T or F
	1. F
	2. F
	3. T
	4. F
	5. T
	6. T
	7. F
	8. T
	9. F
	10. F
2. decreases stalls when prediction is correct, make the common case fast
3. Write through: writes to cache and main memory at the same time, used for L1 write through to L2. Write back: requires dirty bit because a cache member can be modified without the main memory. L2 penalty to main memory would be brutal with write through so write back is used
4. increase miss rate, lower hit time.
5. you would have faster access to data, after the ID stage instead of EX stage