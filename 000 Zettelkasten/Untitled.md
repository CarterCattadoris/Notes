
# Quick Study Guide: Combinational Circuit Design (Essential Concepts Only)
 
## The One Formula You Must Know
 
Everything in this topic comes down to **d = gh + p**. This tells you the delay of a gate. The delay has two parts: the effort delay (gh) which depends on the load you're driving, and the parasitic delay (p) which is always there regardless of load.
 
Think of g (logical effort) as "how bad is this gate compared to an inverter?" An inverter has g equals one. A two-input NAND has g equals four-thirds, and a two-input NOR has g equals five-thirds. This immediately tells you that NAND gates are faster than NOR gates in CMOS, which is why you'll see more NANDs in real designs.
 
The h value (electrical effort) is just how much capacitance you're driving divided by your input capacitance. If you're driving something four times bigger than yourself, your h equals four.
 
## Gate Logical Efforts (Memorize These)
 
For NAND gates, use g equals (n+2)/3 where n is the number of inputs. So a two-input NAND is 4/3, three-input is 5/3, four-input is 6/3 which is 2.
 
For NOR gates, use g equals (2n+1)/3. So a two-input NOR is 5/3, three-input is 7/3, four-input is 9/3 which is 3.
 
An inverter is always g equals 1.
 
## Parasitic Delays (Memorize These)
 
Inverter has p equals 1. Both NAND and NOR gates have p equal to the number of inputs. A two-input NAND has p equals 2, a three-input NAND has p equals 3, and so on.
 
## Multiple Gates in a Path
 
When you have several gates in a row, multiply all the individual g values to get the path logical effort G. The path electrical effort H is just the final output capacitance divided by the very first input capacitance.
 
If the path has branches (capacitance going somewhere else besides the main path), you need branching effort B. For each branching point, calculate b equals (capacitance on path plus capacitance off path) divided by (capacitance on path). Multiply all the b values together to get B.
 
The total path effort is F equals GBH. This one number tells you how hard your path is working.
 
## Optimal Staging
 
Here's the key insight: paths are fastest when each stage has an effort around 4. If your path effort F is 64, you need about log-base-4 of 64 equals 3 stages. Each stage should have effort around 4, and the total delay will be roughly 3 times 4 plus parasitic delays equals 12 plus maybe 6 for parasitics equals 18 time units.
 
The general formula is N approximately equals log₄(F) for the number of stages, and the delay is D equals N times F to the power of (1/N) plus P, where P is the sum of all parasitic delays.
 
## Sizing Gates
 
Once you know you want each stage to have effort f equals 4, you work backward from the output. For each gate, its input capacitance should be C_in equals g times C_out divided by f. Start at the output where you know C_out, calculate that gate's C_in, then move to the previous gate where that C_in becomes the new C_out, and repeat.
 
## Problem-Solving Steps
 
First, identify your path and mark the starting and ending capacitances. Second, calculate G by multiplying all the g values. Third, calculate H from the capacitance ratio. Fourth, check for branches and calculate B if needed. Fifth, multiply to get F equals GBH. Sixth, find N using log₄(F) and round to a whole number. Seventh, calculate the target stage effort as F to the power of (1/N). Eighth, size gates working backward. Finally, add up all delays to get total delay.
 
## Quick Reference Card
 
**Gate efforts:** Inverter g=1, NAND2 g=4/3, NAND3 g=5/3, NAND4 g=2, NOR2 g=5/3, NOR3 g=7/3, NOR4 g=3
 
**Parasitic delays:** Inverter p=1, NANDn p=n, NORn p=n
 
**Path effort:** F = GBH where G = product of all g values, H = C_out/C_in, B = product of all branching factors
 
**Optimal stages:** N ≈ log₄(F), use stage effort f ≈ 4
 
**Gate sizing:** C_in = g·C_out/f, work backward from output
 
**Total delay:** D = N·f + P where P is sum of parasitic delays
 
## Most Likely Exam Problems
 
You'll probably see a problem where you have a chain of gates with given input and output capacitances, and you need to find the optimal number of stages and size each gate. Use the steps above. You might also see a problem asking which gate type is faster for a given function—remember NAND beats NOR. Or you might need to calculate delay for a given circuit—just apply d equals gh plus p to each stage and add them up.
 
# Quick Study Guide: Clocking and Sequential Elements
 
Let me give you the essential concepts you need to pass this exam tomorrow. I'll focus on what actually shows up on tests.
 
## Core Concept: Why Clocking Matters
 
Synchronous systems need clocks to determine when data is valid. The clock creates timing boundaries so your chip knows "cycle 1" from "cycle 2." Think of it like a heartbeat for your digital circuit - it coordinates everything.
 
The challenge is that distributing the clock signal across a chip takes time due to wire resistance and capacitance. This creates two problems you must understand: **clock skew** (different parts of the chip receive the clock at different times) and **clock jitter** (the clock edge itself varies in time).
 
## Essential Definitions
 
**Clock Skew** is the spatial difference in clock arrival times. If flip-flop A gets the clock 20 picoseconds before flip-flop B, you have 20ps of skew. Skew can be positive or negative depending on which flip-flop receives the clock first.
 
**Clock Jitter** is temporal variation in the clock period itself. Even at one location, the clock edges don't arrive at perfectly regular intervals.
 
**Critical distinction**: Skew affects both setup and hold time analysis. Jitter primarily affects setup time because if jitter tracks together at both flip-flops, the relative timing doesn't change for hold analysis.
 
## Clock Distribution - Quick Summary
 
Your exam might ask you to compare distribution methods. Here's what you need to know:
 
**H-Trees** use matched path lengths in a fractal pattern. They have low wire capacitance but can have high delay. Skew is low when designed well.
 
**Grids** use wide metal wires that short the clock together everywhere. They have high wire capacitance but low delay and low local skew. The grid averages out differences.
 
**Hybrid networks** (used in most modern chips) combine H-trees with grids to get the benefits of both.
 
The key tradeoff table you should memorize:
 
Grid: High wire cap, Low delay, Low-Medium skew H-Tree: Low wire cap, High delay, Low skew  

Pulsed: Very high wire cap, High delay, Low skew
 
## Latches vs Flip-Flops - The Key Difference
 
**A latch is level-sensitive**. When the clock is high (for a positive latch), the output follows the input continuously. When the clock goes low, it holds the last value. The latch is "transparent" when the clock is active.
 
**A flip-flop is edge-triggered**. The output only changes at the clock edge (rising or falling). A flip-flop is actually two latches back-to-back with opposite clock phases.
 
This difference is fundamental to everything else, so make sure you understand it.
 
## Timing Parameters You Must Know
 
For any timing problem, you need these definitions:
 
**t_pcq** is propagation delay from clock to output (maximum time) **t_ccq** is contamination delay from clock to output (minimum time) **t_setup** is how long before the clock edge data must be stable **t_hold** is how long after the clock edge data must stay stable **t_pd** is logic propagation delay (maximum) **t_cd** is logic contamination delay (minimum)
 
The key insight is that setup time uses **maximum** delays (worst case) while hold time uses **minimum** delays (best case).
 
## Critical Timing Equations
 
These are the formulas that will appear on your exam. Learn them cold.
 
**Setup Time for Flip-Flops:** T_cycle ≥ t_pcq + t_pd + t_setup + t_skew
 
This tells you the minimum clock period. The logic delay t_pd must fit within the cycle time minus the sequencing overhead (t_pcq + t_setup + t_skew).
 
**Hold Time for Flip-Flops:** t_cd + t_ccq ≥ t_hold + t_skew
 
This is independent of clock period. The minimum logic delay plus the minimum clock-to-Q delay must exceed the hold time plus skew.
 
**Key insight about skew**: Positive skew (capturing flip-flop gets clock later) helps hold time but hurts setup time. Negative skew does the opposite.
 
**For Two-Phase Latches** (less common but important): Setup: t_pd ≤ T_c - 2t_pdq Hold: t_cd ≥ t_hold - t_ccq - t_nonoverlap + t_skew (in each half cycle)
 
**Time borrowing with latches:** t_borrow ≤ T_c/2 - (t_setup + t_nonoverlap + t_skew)
 
Latches allow time borrowing because they're transparent for part of the cycle. A slow path can borrow time from a fast path as long as the total delay over the full cycle is acceptable.
 
## Problem-Solving Strategy for Setup Time
 
When you see a setup time problem, follow these steps:
 
First, identify what the problem is asking - usually maximum frequency or minimum clock period.
 
Second, write the setup equation: T_c ≥ t_pcq + t_pd + t_setup + t_skew
 
Third, plug in the values carefully. Make sure you use maximum delays and get the sign of skew correct.
 
Fourth, solve for T_c (minimum) and if asked, calculate f_max = 1/T_c.
 
**Common mistake**: Students forget to include skew or use the wrong sign. If the problem says the capturing flip-flop receives the clock 30ps later, that's positive skew which makes the problem worse.
 
## Problem-Solving Strategy for Hold Time
 
Hold time problems ask whether there's a violation and how to fix it.
 
First, write the hold constraint: t_cd + t_ccq ≥ t_hold + t_skew
 
Second, use **minimum** delays. This is the opposite of setup time analysis.
 
Third, check if the inequality is satisfied. If the left side is smaller, you have a violation.
 
Fourth, if violated, calculate how much delay to add: (t_hold + t_skew) - (t_cd + t_ccq)
 
**Critical point**: You cannot fix hold time by slowing the clock. Hold time is independent of clock frequency. The only fix is adding delay buffers.
 
**Another critical point**: Positive skew now hurts hold time (opposite of setup). If the capturing flip-flop gets the clock later, data has less time to remain stable.
 
## Metastability - What You Need to Know
 
When you violate setup or hold time, a flip-flop can enter a metastable state where its output is stuck between 0 and 1. This is catastrophic because the output might oscillate or produce invalid voltage levels.
 
The probability of metastability is given by the MTBF formula:
 
MTBF = e^(t_MET/C2) / (C1 × f_CLK × f_DATA)
 
where t_MET is the time available for the flip-flop to resolve the metastable state.
 
**Key insight**: MTBF increases exponentially with t_MET. Adding synchronizer stages dramatically improves MTBF because each stage adds a full clock period to t_MET.
 
For asynchronous signals entering your clock domain, always use at least two (preferably three) synchronizer flip-flops in series with no logic between them. This gives metastability time to resolve.
 
## Quick Tips for Tomorrow
 
**On setup time questions**: Use maximum delays, include skew with correct sign, solve for minimum clock period.
 
**On hold time questions**: Use minimum delays, remember you can't fix it by slowing the clock, calculate required buffer delay if violated.
 
**On skew questions**: Remember positive skew helps hold but hurts setup. Know that skew comes from different wire lengths, process variations, and power supply noise.
 
**On latch questions**: Remember time borrowing is the key advantage. Total delay over full cycle matters more than individual path delays.
 
**On metastability questions**: More synchronizer stages means exponentially better MTBF. Calculate t_MET as the sum of available time at each stage.
 
**Most common exam mistake**: Mixing up maximum and minimum delays. Setup uses max, hold uses min. Write this down at the top of your exam.
 
**Second most common mistake**: Getting the sign of clock skew wrong. Draw a timing diagram if you're unsure which flip-flop gets the clock first.
 
## Practice Problem Pattern
 
If you see: "Flip-flops have t_pcq=80ps, t_setup=60ps, t_hold=40ps, t_ccq=30ps. Logic has t_pd=500ps, t_cd=100ps. Clock skew is +20ps. Find minimum clock period and check hold time."
 
**Setup**: T_c ≥ 80 + 500 + 60 + 20 = 660ps minimum
 
**Hold**: Check if 100 + 30 ≥ 40 + 20 130 ≥ 60 ✓ (no violation)
 
This pattern covers probably 60% of exam questions on this topic.
 
Focus on understanding these core concepts and practicing the formula applications. You'll do fine tomorrow. The key is staying organized and being careful with signs and which delays to use (max vs min). Good luck!
 
# ADDER DESIGN - Quick Exam Study Guide
 
## ESSENTIAL FORMULAS TO MEMORIZE
 
**Half Adder:**
 
- Sum: S = A ⊕ B

- Carry: Cout = A • B
 
**Full Adder:**
 
- Sum: S = A ⊕ B ⊕ Cin (or S = P ⊕ Cin where P = A ⊕ B)

- Carry: Cout = MAJ(A,B,C) = A•B + A•Cin + B•Cin = G + P•Cin
 
**Propagate/Generate (PG) Logic:**
 
- Generate: G = A • B (forces carry out to be 1)

- Propagate: P = A ⊕ B (passes carry through)

- Kill: K = ~A • ~B (forces carry out to be 0)

- Cout = G + P•Cin
 
**Group PG (for ranges i:j):**
 
- Gi:j = Gi:k + Pi:k • Gk-1:j

- Pi:j = Pi:k • Pk-1:j

- Base case: Gi:i = Ai • Bi, Pi:i = Ai ⊕ Bi
 
**Delay Formulas:**
 
- Ripple Carry: t = tpg + (N-1)•tAO + txor

- Carry-Skip: t = tpg + [2(n-1) + (k-1)]•tAO + txor (for k groups of n bits)

- Carry-Increment: t = tpg + [(n-1) + (k-1)]•tAO + txor
 
## KEY CONCEPTS SIMPLY EXPLAINED
 
**The Core Problem:** Addition requires propagating carry bits from right to left. The LSB carry affects every bit to its left, creating a sequential dependency that limits speed.
 
**Three Design Approaches:**
 
1. **Ripple Carry** - Let the carry ripple through sequentially. Slowest but smallest area. Delay grows linearly O(N).

2. **Carry-Skip/Select** - Divide into groups. Skip over or select pre-computed results for entire groups. Reduces delay to O(√N) with proper group sizing.

3. **Carry-Lookahead/Tree** - Compute all carries in parallel using PG logic. Fastest but largest area. Delay grows logarithmically O(log N).
 
**Understanding PG Logic:** Think of each bit position as either generating a carry (both inputs 1), propagating a carry (exactly one input 1), or killing a carry (both inputs 0). By combining these across multiple bits, you can compute carries without waiting for previous stages.
 
## ADDER ARCHITECTURES - WHAT YOU MUST KNOW
 
**Ripple Carry:**
 
- Chain full adders sequentially

- Critical path: Cin through N stages to Cout

- Use inverting full adders alternately to eliminate inverters on carry path

- Simplest but slowest for large N
 
**Carry-Skip:**
 
- Divide N bits into groups of n bits each

- Each group has a multiplexer: if all bits propagate (Pi:j = 1), skip directly to next group

- Variable group size (larger in middle, smaller at ends) optimizes delay

- Manchester design uses dynamic logic with pass gates
 
**Carry-Select:**
 
- Pre-compute results for both Cin = 0 and Cin = 1

- When actual carry arrives, use multiplexer to select correct result

- Doubles hardware but cuts delay

- Can use variable group sizes for optimization
 
**Carry-Lookahead (CLA):**
 
- Use higher-valency cells (3+ inputs) to compute group PG values

- All carries computed in parallel rather than sequentially

- Trade wiring complexity for speed
 
**Tree Adders (Prefix Trees):**
 
- Apply PG combination recursively in tree structure

- Three key metrics: logic levels (l), fanout (f), wiring tracks (t)

- All known trees satisfy: l + f + t = L - 1 (where L = log₂ N)
 
**The Three Extremes:**
 
- Kogge-Stone (0,0,3): Minimum logic levels, maximum wiring

- Sklansky (0,3,0): Minimum logic levels, maximum fanout

- Brent-Kung (3,0,0): Minimum wiring/fanout, maximum logic levels
 
**The Compromises:**
 
- Han-Carlson: Hybrid of Kogge-Stone + Brent-Kung

- Knowles: Reduces wiring vs Kogge-Stone

- Ladner-Fischer: Reduces fanout vs Sklansky
 
## PROBLEM-SOLVING APPROACH
 
**For delay calculations:**
 
1. Identify the critical path (usually Cin to Cout)

2. Count levels of logic gates along that path

3. Use the formula: t = tpg + (stages)•tAO + txor
 
**For PG diagram problems:**
 
4. First row: compute individual G and P for each bit

5. Each subsequent row: combine adjacent groups using Gi:j formulas

6. Black cells compute both G and P; gray cells compute only G

7. Final result: G(N-1):0 is the final carry out
 
**For choosing an adder:**
 
- Need minimum area? → Ripple carry

- Need minimum delay? → Tree adder (Kogge-Stone if wiring isn't constrained)

- Balanced design? → Carry-skip with variable groups or Han-Carlson tree

- Low fanout required? → Brent-Kung
 
## QUICK REFERENCE VALUES
 
**For 16-bit adders:**
 
- Ripple: ~16 gate delays

- Carry-skip (4-bit groups): ~10 gate delays

- Tree adders: ~4 logic levels (log₂ 16 = 4)
 
**Tree Adder Taxonomy (l, f, t) for 16-bit:**
 
- Brent-Kung: (3, 0, 0) = 7 logic levels, fanout 2, minimal wiring

- Sklansky: (0, 3, 0) = 4 logic levels, fanout 9, minimal wiring

- Kogge-Stone: (0, 0, 3) = 4 logic levels, fanout 2, 8× wiring
 
**Critical Insight:** For N-bit addition, the theoretical minimum is log₂ N levels of logic. Everything else is about managing the tradeoffs between area (transistor count), wiring (routing resources), and fanout (gate loading).
 
## EXAM TIPS
 
When you see a PG diagram, trace one path from bottom to top to understand the carry computation. When comparing adders, think: "What's the bottleneck?" For ripple it's sequential carry propagation. For trees it's logic depth. For carry-skip it's the longest path (either through a group or skipping across groups).
 
The most testable concept is the PG recursion formula - make sure you can apply Gi:j = Gi:k + Pi:k • Gk-1:j to combine groups. Also be ready to calculate delays given gate delays (tpg, tAO, txor).
 
# VLSI Datapath Design - Exam Study Guide
 
## 1. COMPARATORS - Essential Formulas & Logic
 
**Core Building Blocks:**
 
The 1's detector uses an N-input AND gate that outputs 1 only when all input bits equal 1. The 0's detector uses an N-input NOR gate (inverters feeding into AND) that outputs 1 only when all input bits equal 0.
 
For equality comparison (A = B), you check if each bit position matches using XNOR gates (the "equality gate"), then AND all the results together. If all bit positions match, the output is 1.
 
**Magnitude Comparison (Critical for Exams):**
 
To determine if A < B for unsigned numbers, compute B - A, which equals B + ~A + 1. The carry-out becomes your sign bit. When the carry-out is 1, you know A ≤ B (or equivalently, A < B when combined with a zero check).
 
For signed number comparison, you need four flags: C (carry-out), Z (zero - all result bits are 0), N (negative - MSB of result), and V (overflow - inputs had different signs and output sign doesn't match B). The signed comparison formulas are:
 
- A < B when (N ⊕ V) + Z

- A > B when (N ⊕ V)

- A ≤ B when (N ⊕ V)

- A ≥ B when (N ⊕ V) + Z
 
## 2. SHIFTERS - Types & Applications
 
**Logical Shifts** fill with zeros. LSL (left) and LSR (right) both shift in 0's and capture the bit shifted out in the carry flag. Left shift by k positions multiplies by 2^k, while right shift divides by 2^k.
 
**Arithmetic Shifts** preserve sign for two's complement. ASR shifts right while copying the sign bit (MSB) into each new position. This performs signed division by powers of two. ASL is identical to LSL.
 
**Rotate Operations** wrap bits around. ROR moves bits right with wraparound, while ROL moves left with wraparound. RRX is special: it's a 33-bit rotate through the carry flag, rotating one position only.
 
**ARM Barrel Shifter Application:** You can multiply by constants efficiently using shifts combined with ADD/SUB. For example, to multiply R5 by 9, use `ADD R9, R5, R5, LSL #3` which computes R5 + (R5 × 8) = R5 × 9 in a single cycle.
 
**Funnel Shifter Implementation:** This versatile design can perform all six shift types by selecting an N-bit field from a 2N-bit input. The offset determines shift amount (k for right shifts, k̄ for left shifts). For right shifts, the upper portion contains appropriate fill bits (0 for logical, sign for arithmetic, original bits for rotate).
 
## 3. MULTI-INPUT ADDERS - Carry-Save Technique
 
**Problem:** Adding k N-bit numbers naively requires k-1 serial adders, which is slow.
 
**Solution:** Carry-Save Adders (CSA) process additions in a tree structure. Each full adder takes three inputs and produces two outputs: a sum bit and a carry bit (weighted twice as much). This is the key insight - keep results in redundant carry-save form until the final stage.
 
**Process:** Use k-2 stages of CSAs to combine k inputs down to two values (a sum vector and carry vector), then use one final Carry-Propagate Adder (CPA) to compute the actual result.
 
**Speed Advantage:** Each CSA stage has constant delay regardless of bit width (no carry propagation). Only the final CPA has O(log N) or O(N) delay depending on implementation.
 
## 4. ARRAY MULTIPLIERS - Structure
 
**Basic Concept:** An M×N bit multiplication generates N partial products (each M bits wide), shifted by position. The product is M+N bits.
 
**Array Structure:** Arrange full adders in a diagonal array. Each row processes one partial product. The first row uses half-adders (HA) for 2-input addition, subsequent rows use full-adders (FA) for 3-input addition. Partial products flow diagonally; carries propagate horizontally and downward.
 
**Rectangular Array:** Squeeze the diagonal structure into a rectangle to optimize floor planning. The final row is a carry-propagate adder to generate the output.
 
**Carry-Save Array:** Replace ripple-carry chains between rows with carry-save logic to speed up operation. Only the final vector-merging adder propagates carries.
 
## 5. SHIFT-ADD MULTIPLIERS - Sequential Approach
 
**Version 1 (Inefficient):** 64-bit multiplicand register shifts left each cycle, 64-bit ALU, 64-bit product register, 32-bit multiplier register shifts right. Wastes hardware since multiplicand upper half is always zero initially.
 
**Version 2 (Better):** 32-bit multiplicand (fixed), 32-bit ALU, 64-bit product register shifts right, 32-bit multiplier register shifts right. The product register gradually fills from left as partial products accumulate.
 
**Version 3 (Optimal):** Combine the multiplier register with the product register. Test bit 0 of product, add multiplicand to upper half if bit is 1, then shift entire product right. This eliminates one register.
 
**Algorithm (32 iterations):**
 
1. Test Product[0]

2. If Product[0] = 1, add Multiplicand to upper half of Product

3. Shift Product right 1 bit

4. Repeat until 32 iterations complete
 
## 6. BOOTH ENCODING - Faster Multiplication
 
**Motivation:** Reduce partial products from N to N/r by examining r bits at once (radix-2^r encoding). For r=2 (radix-4), you'd need multiples 0, Y, 2Y, 3Y. Since 3Y requires an adder, use a clever trick: instead of 3Y, use -Y and add 4Y to the next partial product.
 
**Modified Radix-4 Booth Table (Memorize This):** Looking at bits x(2i+1), x(2i), x(2i-1):
 
- 000 → 0

- 001 → +Y (SINGLE)

- 010 → +Y (SINGLE)

- 011 → +2Y (DOUBLE)

- 100 → -2Y (DOUBLE, NEG)

- 101 → -Y (SINGLE, NEG)

- 110 → -Y (SINGLE, NEG)

- 111 → 0
 
**Sign Extension Simplification:** Negative partial products need sign extension. Rather than extending many 1's, observe that all 1's equals a single 1 in the proper column plus inverse of the sign bit. Precompute these values and add them once rather than extending each partial product.
 
**Hardware:** Booth encoder generates three control signals (SINGLE, DOUBLE, NEG) per partial product. Booth selector uses these to choose 0, Y, 2Y, -Y, or -2Y efficiently using multiplexers and conditional negation.
 
---
 
## Exam Problem-Solving Strategy
 
**For Comparator Questions:** Draw the circuit showing XNOR gates for equality, or the subtractor with flag generation for magnitude comparison. Remember that unsigned uses carry-out directly, signed uses the (N⊕V) formula.
 
**For Shifter Questions:** If asked to implement a multiply-by-constant, factor it as sums/differences of powers of 2. For example, ×7 = ×8 - ×1, so use `RSB R9, R5, R5, LSL #3`.
 
**For Multiplier Design Questions:** Count the critical path (number of FA delays) for array multipliers. For Booth encoding, practice the bit pattern recognition. Remember that radix-4 Booth cuts partial products in half (from N to N/2).
 
**For Bit-Serial Questions:** Understand that these trade speed for area - only one bit processed per clock but much simpler hardware.
 
The most commonly tested concepts are: magnitude comparator flag logic for signed numbers, Booth encoding table, and the evolution from shift-add multiplier version 1 to version 3. Master these three and you'll handle most exam questions successfully.
 
# CMOS Interconnects Study Guide - Quick Exam Reference
 
## Essential Formulas to Memorize
 
**Wire Resistance:**
 
- R = ρl/(tw) = R□ × (l/w)

- R□ = ρ/t (sheet resistance in Ω/□)

- Count squares: R = R□ × number of squares
 
**Wire Capacitance:**
 
- Total capacitance: C_total = C_top + C_bot + 2C_adj

- C = εA/d (parallel plate approximation)

- ε = kε₀ where ε₀ = 8.85 × 10⁻¹⁴ F/cm
 
**Miller Coupling Factor (MCF) for Crosstalk:**
 
- Neighbor constant: C_eff = C_gnd + C_adj, MCF = 1

- Neighbor switching with wire: C_eff = C_gnd, MCF = 0

- Neighbor switching opposite: C_eff = C_gnd + 2C_adj, MCF = 2
 
**Crosstalk Noise:**
 
- Floating victim: ΔV_victim = [C_adj/(C_gnd-v + C_adj)] × ΔV_aggressor

- Driven victim: ΔV_victim = [C_adj/(C_gnd-v + C_adj)] × [1/(1+k)] × ΔV_aggressor where k = (τ_aggressor/τ_victim) × (R_aggressor/R_victim) × [(C_gnd-a + C_adj)/(C_gnd-v + C_adj)]
 
**Repeater Optimization:**
 
- Optimal number: N = l√(R_w C_w)/(2RC')

- Optimal width: W = √(RC_w)/(R_w C')

- Typical result: 60-80 ps/mm in 180 nm process
 
## Key Reference Values
 
**Metal Resistivity (bulk):**
 
- Copper: 1.7 μΩ·cm (35-40% better than aluminum)

- Aluminum: 2.8 μΩ·cm

- Silver: 1.6 μΩ·cm (best but not used)
 
**Sheet Resistance (180 nm process):**
 
- Metal1: 0.08 Ω/□

- Metal2-3: 0.05 Ω/□

- Metal4-6: 0.02-0.03 Ω/□

- Polysilicon (silicided): 3-10 Ω/□

- Polysilicon (no silicide): 50-400 Ω/□

- Diffusion (silicided): 3-10 Ω/□
 
**Capacitance Values:**
 
- Typical wire: ~0.2 fF/μm

- Gate capacitance: ~2 fF/μm

- Diffusion capacitance: ~2 fF/μm (very high!)
 
**Dielectric Constants:**
 
- SiO₂: k = 3.9

- Low-k dielectrics: k ≈ 3 or less
 
## Core Concepts Explained Simply
 
**Why Interconnects Matter:** Modern chips are mostly wires with small transistors underneath. Wires affect speed, power consumption, noise, and reliability just as much as transistors do.
 
**Metal Layers Strategy:** Processes use multiple metal layers with different thicknesses. Lower layers (M1-M3) are thin and tightly packed for local connections. Upper layers (M4-M6) are thick with wider spacing for global wires, power, and clock distribution. This reduces resistance for long wires.
 
**Aspect Ratio:** The ratio of wire thickness to width (AR = t/w). Deep submicron processes keep AR less than 2 to maintain reasonable sheet resistance. When wires have high aspect ratios, coupling to neighboring wires dominates over ground capacitance.
 
**Why Copper Replaced Aluminum:** Copper has lower resistivity, but it diffuses into silicon and damages transistors. Solution: surround copper with a diffusion barrier (adds a thin layer that increases effective resistance slightly but still worth it).
 
**Crosstalk Physics:** When a neighboring wire switches, the capacitance between wires resists voltage changes. If your wire is trying to stay at a constant voltage, the neighbor's transition will pull it up or down temporarily. If both wires switch in opposite directions, the effective capacitance doubles (Miller effect), dramatically increasing delay.
 
**Why Repeaters Work:** Wire delay grows with L² because both R and C increase with length. Breaking a long wire into N segments with buffers between them reduces delay from L² to approximately L. You pay an area and power cost, but gain enormous speed improvement for long wires.
 
## Problem-Solving Approach
 
**For Resistance Problems:**
 
1. Identify the wire dimensions (length l, width w, thickness t)

2. Find the sheet resistance R□ for that metal layer

3. Calculate number of squares: l/w

4. Multiply: R = R□ × (l/w)

5. Don't forget contact/via resistance if present (typically 2-20 Ω each)
 
**For Capacitance Problems:**
 
6. Determine what capacitances exist: C_top, C_bot, C_adj

7. For ground capacitance, consider layers above and below

8. For coupling, check neighbors on same layer

9. Remember: C_total = C_gnd + 2×C_adj (factor of 2 because two neighbors)

10. Use graphs/tables if given for specific geometries
 
**For Crosstalk Delay Problems:**
 
1. Identify which neighbors are switching and in what direction

2. Determine MCF for each neighbor (0, 1, or 2)

3. Calculate effective capacitance: C_eff = C_gnd + MCF×C_adj

4. Worst case is all neighbors switching opposite direction (MCF = 2)

5. Best case is all neighbors switching same direction (MCF = 0)
 
**For Crosstalk Noise Problems:**
 
6. Draw the equivalent circuit with aggressor and victim

7. Identify if victim is floating or driven

8. If driven, estimate resistance ratio (aggressor in saturation is typically 2-4× victim in linear)

9. Apply appropriate formula

10. Check if noise exceeds noise margin
 
**For Repeater Problems:**
 
1. Extract wire parameters: R_w (resistance per length), C_w (capacitance per length)

2. Extract gate parameters: R (resistance of unit inverter), C' (capacitance per unit width)

3. Apply optimization formulas for N and W

4. Remember this gives minimum delay; practical designs may use fewer repeaters
 
## Exam Strategy Tips
 
**Watch for units:** Sheet resistance is Ω/□ (dimensionless square). Length is often in microns. Capacitance might be in fF (femtofarads).
 
**Polysilicon and diffusion are terrible for wires:** They have much higher resistance and comparable capacitance to metal. Only use polysilicon for gates and very short connections.
 
**Use upper metal layers for long wires:** They have lower sheet resistance and are farther from other layers, reducing capacitance.
 
**Shielding reduces crosstalk:** Placing power or ground wires between signals eliminates coupling capacitance. This trades area for noise immunity.
 
**Quick sanity checks:**
 
- Does increasing wire width decrease resistance? (Yes, more area for current)

- Does increasing wire width increase capacitance? (Yes, more area facing neighbors)

- Does spacing wires farther apart reduce crosstalk? (Yes, capacitance decreases with distance)

- Should critical signals be on upper metal layers? (Usually yes, for speed and lower noise)
 
**Common traps:**
 
- Forgetting the factor of 2 in C_total = C_gnd + 2C_adj (two adjacent neighbors)

- Confusing bulk resistivity ρ with sheet resistance R□

- Using the wrong MCF value for crosstalk calculations

- Neglecting contact/via resistance in total path resistance
 
This focused guide covers the essential formulas and concepts you need for exam success. Practice applying the problem-solving approaches to sample problems, and you'll be well-prepared. Good luck tomorrow!
 
#100
 
#claudeai
 
THE COMPARISON QUESTION (Most Important)
Your professor explicitly said he'll show you two adders and ask which is better and why. Here's how to approach this:
What "better" means depends on the metric. When comparing adders, you need to identify the critical path (longest delay path) and count the hardware resources. The critical path in almost all adders runs from the least significant bit's carry-in to the most significant bit's carry-out, because each bit might need to wait for the carry from the previous position.
For a ripple carry adder, the critical path goes through every single full adder stage sequentially. If you have a 16-bit ripple carry adder, the carry signal must propagate through all 16 full adders. So you would say "the critical path has 16 full adder delays."
For a carry-lookahead or tree adder, the critical path is much shorter because carries are computed in parallel using additional logic gates. Instead of 16 sequential stages, you might only have 4 or 5 levels of logic depth (remember, log₂ of 16 is 4).
When counting full adders versus half adders, remember that a half adder is only used in the least significant bit position where there's no carry-in. Every other position needs a full adder because it must handle two input bits plus a carry-in. So a 16-bit adder would typically have 1 half adder and 15 full adders, or sometimes 16 full adders if the designer just uses full adders throughout for consistency.
THE FUNDAMENTAL EXPRESSIONS (Guaranteed to Appear)
Your professor emphasized that you need to know the truth tables and that "carry-out can be written differently." This is crucial. Let me show you the different valid forms:
For a full adder, the carry-out can be expressed as the majority function (at least two of the three inputs must be 1). This gives you several equivalent forms:
Cout = A•B + A•Cin + B•Cin (sum-of-products form from the truth table)
But this can also be factored as:
Cout = A•B + (A ⊕ B)•Cin which is the same as Cout = G + P•Cin in propagate-generate form.
The reason this matters is that the second form shows you can compute the generate term (A•B) and propagate term (A ⊕ B) first, then use those to quickly determine the carry. This factored form is actually faster to implement because it reuses the P term that you've already computed for the sum.
For the sum output, there's really only one form that matters:S = A ⊕ B ⊕ Cin which can also be written as S = P ⊕ Cin where P = A ⊕ B.
 