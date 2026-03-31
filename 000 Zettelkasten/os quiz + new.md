# OS Quiz Study Sheet

---

## PART A: MEMORY MANAGEMENT & NON-CONTIGUOUS MEMORY

---

### 1. Memory Hierarchy & Principle of Locality

**Memory hierarchy (fastest → slowest, smallest → largest):** Registers → L1/L2 Cache → Main Memory (RAM) → Hard Disk (SSD/HDD)

**Principle of Locality** — the key assumption behind caches, TLBs, and page replacement:

- **Temporal locality:** If a memory location was accessed recently, it's likely to be accessed again soon.
- **Spatial locality:** If a memory location was accessed, nearby locations are likely to be accessed soon.
- Writing small subroutines and tight loops improves locality and speeds up memory access through the hierarchy.

**Three goals of memory management:**

1. **Protection** — prevent processes from accessing each other's memory.
2. **Utilization** — maximize how many programs fit in memory; allow programs larger than physical RAM.
3. **Speed** — support fast instruction/data access using the hierarchy.

---

### 2. Taxonomy of Memory Management Schemes

There are four combinations:

||Contiguous|Non-Contiguous|
|---|---|---|
|**Load entire program**|Case 1: Base+Limit registers|Case 3: (uncommon)|
|**Load parts on demand**|Case 2: Overlays|Case 4: **Paging + Virtual Memory** ← modern|

**Case 1 — Contiguous with Base & Limit Registers:**

- Program loaded into one contiguous block. MMU checks every address: `base ≤ address < base + limit`.
- Problem: **external fragmentation** — small free gaps between processes that can't be used.
- Fix: **memory compaction** — expensive, suspends all user programs to shuffle memory.

**Case 2 — Overlays (Game Consoles):**

- Program is bigger than RAM; _programmer_ manually divides program into stages/parts loaded one at a time.
- Not transparent — the application programmer must manage the division.

---

### 3. Non-Contiguous Memory: Paging

**Core idea:** Divide the program's address space into fixed-size **pages**; divide physical memory into same-size **page frames**. Pages can be loaded into _any_ available frame (non-contiguously).

**Key definitions:**

- **Page:** fixed-size chunk of a process's virtual address space (e.g. 4KB).
- **Page frame:** same-size chunk of physical memory.
- **Page table:** per-process mapping of virtual page # → physical frame #. Kept by the OS.

**Address translation (virtual → physical):**

- Virtual address = `[page number | offset]`
- Number of offset bits = log₂(page size). The remaining upper bits = page number.
- Example: 32-bit CPU, 4KB page → 12 bits offset, 20 bits page number → 2²⁰ = 1,048,576 pages.

**Calculating pages needed:** ⌈process size / page size⌉. Example: 145KB process, 8KB pages → ⌈145/8⌉ = 19 pages.

---

### 4. Virtual Memory Systems

- Pages are stored in the hard disk's **swap area** (virtual memory area).
- Only _needed_ pages are brought into RAM. Programs can be larger than physical memory.
- Main memory acts as a **cache** for the hard disk.

**Page fault:** When the CPU references a page not currently in RAM.

1. If a free frame exists → bring page in from disk.
2. If no free frame → run a **page replacement algorithm** to pick a victim, then bring the desired page in.
3. The faulting process is **blocked** (put in I/O wait queue) until the page arrives. This is an **involuntary I/O**.
4. When the disk I/O completes, an interrupt fires. The exception handler backs up the PC to re-execute the faulted instruction. The process re-enters the ready queue.

---

### 5. Performance Issues in Paging

**Speed problem — address translation overhead:**

- Every memory access now requires an extra access to the page table. Paging can _double_ access time.
- Solution: **TLB (Translation Lookaside Buffer)** — a small, fast hardware cache storing recent `<virtual page, physical frame>` pairs. If TLB hit → bypass page table lookup entirely. Typical size ~1024 entries.
- If TLB hit ratio is high, paging speed is comparable to non-paging systems.

**Space problem — page table size:**

- For a 64-bit CPU with 4KB pages: 2⁵² entries × 8 bytes = 32,768 TB per page table. Impossible.
- **Solution 1: Multi-level paging** — divide the huge page table into smaller sub-tables. Only keep the needed ones in memory (locality principle). E.g. split 52 bits into four 13-bit groups → each sub-table has 8,192 entries = 64KB.
- **Solution 2: Inverted Page Table (IPT)** — one system-wide table with entries = (physical memory size / page size). Each entry stores `<process ID, page #>`. Uses hashing for fast lookup. Much smaller (e.g. 16GB RAM / 4KB = 4M entries × 8 bytes = 32MB total).

**TLB hit-ratio calculation example:** If TLB hit ratio = 0.3 and page table is always in memory (no page faults):

- TLB hit (30%): 1 memory access (for data).
- TLB miss (70%): 1 access for page table + 1 for data = 2 accesses.
- Average per reference = 0.3(1) + 0.7(2) = 1.7 memory accesses.
- Per 100 references → 170 memory accesses.

---

### 6. Segmentation with Paging

**Problem with pure paging:** All four segments (text, static data, dynamic data/heap, stack) share one virtual address space. The heap and stack can collide if they grow toward each other.

**Solution:** Each segment gets its _own_ virtual address space. Then each segment is divided into pages.

**Address translation:** Use the most-significant bits to identify the segment, then the page number, then offset. Example: 32-bit CPU, 1KB pages, 8 bits for segment → segment bits identify which segment's page table to consult, then proceed as normal paging.

**Pure paging vs. Segmentation with paging:**

- Pure paging: one linear virtual address space for all segments.
- Seg+paging: each segment has its own address space and can grow/shrink independently.

---

### 7. Page Replacement Algorithms

All attempt to predict which page is _least likely_ to be needed soon. Key questions for each algorithm: what info is tracked, when is it updated, and how is the victim chosen?

**Random:** Pick a random frame. Fast, no overhead, no past info needed. Works OK when frame count is small (e.g. L1/L2 cache).

**FIFO (First-In First-Out):** Replace the oldest page in memory. Simple (sorted linked list). Problem: old pages may still be heavily used → **thrashing** (excessive page faults, OS spends most time handling faults instead of running user programs).

**NRU (Not Recently Used):** Uses 2 bits per page table entry:

- **R (Referenced):** set on any access; cleared at every clock interrupt.
- **D (Dirty):** set when page is modified (written to).
- Victim priority: (R=0,D=0) → (R=0,D=1) → (R=1,D=0) → (R=1,D=1).
- A dirty victim must be written back to disk before replacement (extra overhead).

**LRU (Least Recently Used):** Track usage count or maintain a linked list updated on every reference. Very accurate but expensive — requires updating data structures on _every_ memory access.

**NFU (Not Frequently Used):** Approximation of LRU. Uses a counter per page + reference bit. At each clock interrupt, if R bit is set, increment counter by 1, then clear R. Cheaper than LRU but less precise. Problem: both LRU and NFU don't "forget" — a page used heavily in the past but no longer needed stays favored.

**Two-Handed Clock:** Proactive — keeps free frames available _before_ faults occur.

- Circular linked list of all pages in memory. Two hands rotate clockwise.
- **First hand:** clears the R bit of the page it points to.
- **Second hand:** if R bit is still 0, evict the page.
- If a page is referenced between the two hands, its R bit gets set → it survives.
- The **angle** between hands controls aggressiveness: wide angle = more lenient (more time for pages to get re-referenced); overlapping hands = evict everything.

---

### 8. Other Virtual Memory Concerns

**Page Daemon:** A system process that runs the two-handed clock periodically to keep a pool of free frames ready. Reduces reactive page faults.

**Pre-paging vs. Demand paging:**

- Demand paging: only bring pages in when a page fault specifically requests them.
- Pre-paging: predictively bring pages that will likely be needed soon. Reduces fault frequency.

**Thrashing:** When page fault frequency is too high; the OS is constantly swapping pages and user programs barely get CPU time. Fix: suspend non-critical processes (swap them out) and give more frames to remaining ones.

**Disk Map:** Tracks where each page lives on the hard disk's swap area so the OS can find it on a fault.

**Involuntary I/O:** A page fault triggers a disk read that the programmer never intended. After the I/O completes, the PC is backed up to retry the faulted instruction (unlike a normal I/O where execution continues forward).

**Page size tradeoffs:**

- Smaller pages → less internal fragmentation, finer granularity, but larger page tables and more TLB misses.
- Larger pages → smaller page tables, fewer faults, but more wasted space (internal fragmentation).

---

---

