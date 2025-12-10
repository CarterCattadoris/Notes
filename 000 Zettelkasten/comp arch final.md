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

