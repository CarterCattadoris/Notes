# VLSI Practice Final Exam

**Name:** ___________________     **Date:** ___________________

**Instructions:** Show all work for full credit. For design questions, clearly label diagrams and explain your reasoning.

---

## Section I: True/False (10 questions, 2 points each)

**1.** In CMOS logical effort analysis, the logical effort of a gate quantifies how much worse the gate is at producing output current compared to a reference inverter, assuming equal input capacitance. 
TRUE

**2.** In a synchronous digital circuit, clock skew always improves timing margins by providing extra time for data to propagate between flip-flops.
FALSE

**3.** For large operand sizes, a carry-lookahead adder outperforms a ripple carry adder because it computes carry bits in parallel using generate and propagate logic.
TRUE

**4.** In CMOS gates, the effort delay scales with both logical effort and electrical effort, whereas the parasitic delay is a fixed property of gate topology independent of load.
TRUE, f=gh+p

**5.** Flip-flops are edge-triggered storage elements that capture input data only on a specific clock transition, eliminating the transparency issues found in latches.
TRUE

**6.** In logical effort methodology, paths are fastest when the stage effort delays are approximately equal to 4.
explain this

**7.** Subthreshold leakage is the dominant source of static power consumption in modern CMOS transistors below 65nm technology nodes.
TRUE

**8.** In a CMOS array multiplier, each partial product is directly summed using ripple carry adders, allowing for the fastest possible multiplication speed.
FALSE, use carry save

**9.** Dynamic RAM (DRAM) requires periodic refresh operations because data is stored as charge on capacitors that leak over time.
TRUE

**10.** Scan chain design converts a sequential test generation problem into a combinational test generation problem, enabling automatic test pattern generation (ATPG).
TRUE

---

## Section II: Multiple Choice (15 questions, 3 points each)

**11.** What is the logical effort (g) of a 2-input NAND gate?
- A) 1
- **B) 4/3**
- C) 5/3
- D) 2

**12.** In the timing constraint for flip-flops with clock skew, the setup time constraint is:
- A) T_c ≥ t_pd + (t_pcq + t_setup - t_skew)
- **B) T_c ≥ t_pd + (t_pcq + t_setup + t_skew)**
- C) t_cd ≥ t_hold - t_ccq + t_skew
- D) t_cd ≥ t_hold + t_ccq - t_skew

**13.** The optimal number of stages (N) for a multi-stage path with path effort F is:
- A) N = F^(1/2)
- B) N = log_2(F)
- C) N = log_4(F)
- D) N = 4F

**14.** In the RC delay model for CMOS, a unit pMOS transistor has:
- A) Resistance R, capacitance C
- B) Resistance 2R, capacitance C
- C) Resistance R/2, capacitance 2C
- D) Resistance R, capacitance 2C

**15.** Which adder architecture has O(√N) delay complexity?
- A) Ripple carry adder
- B) Carry-lookahead adder
- C) Carry-skip adder
- D) Carry-select adder

**16.** The path delay D in logical effort methodology is calculated as:
- A) D = F + P
- B) D = GBH + P
- C) D = NF^(1/N) + P
- D) D = N·G·H + P

**17.** What causes the body effect in CMOS transistors?
- A) Channel length modulation
- B) Source-to-bulk voltage affecting threshold voltage
- C) Velocity saturation of carriers
- D) Gate oxide tunneling

**18.** In a 6T SRAM cell, the size ratio N1 >> N2 is required for:
- A) Write stability
- B) Read stability
- C) Reduced power consumption
- D) Faster access time

**19.** Clock jitter primarily affects:
- A) Only setup time margins
- B) Only hold time margins
- C) Both setup and hold time margins equally
- D) Cycle time but not race margins

**20.** The electrical effort (h) in logical effort is defined as:
- A) Input capacitance / Output capacitance
- B) Output capacitance / Input capacitance
- C) Logical effort × Path effort
- D) Gate delay / Inverter delay

**21.** Which memory type is volatile and requires the most transistors per bit?
- A) DRAM (1T1C)
- B) SRAM (6T)
- C) Flash memory
- D) ROM

**22.** The branching effort (B) accounts for:
- A) Number of stages in a path
- B) Fan-out and off-path capacitance
- C) Intrinsic gate delay
- D) Wire capacitance only

**23.** In a carry-save multiplier, the critical path includes:
- A) Only the partial product generation
- B) Only the final carry-propagate adder
- C) Partial product generation + final CPA
- D) N stages of ripple carry addition

**24.** Gate leakage in modern CMOS is caused by:
- A) Reverse-biased PN junctions
- B) Subthreshold conduction
- C) Quantum tunneling through thin gate oxide
- D) Hot carrier injection

**25.** The best stage effort (f̂) for minimum delay in logical effort is:
- A) f̂ = 1
- B) f̂ = e ≈ 2.718
- C) f̂ = 4
- D) f̂ = F^(1/N)

---

## Section III: Short Answer (5 questions, 8 points each)

**26.** Explain the difference between propagation delay (t_pd) and contamination delay (t_cd) in combinational logic. Why are both important for timing analysis in sequential circuits?

**27.** A path has logical effort G = 20, electrical effort H = 8, and no branching (B = 1). The parasitic delay P = 12. Calculate:
- a) The path effort F
- b) The optimal number of stages N
- c) The estimated minimum delay D

**28.** Describe three techniques for reducing clock skew in VLSI designs. Explain how each technique helps minimize skew and its trade-offs.

**29.** Compare ripple carry adders and carry-lookahead adders in terms of:
- a) Delay complexity (big-O notation)
- b) Area/transistor count
- c) Power consumption
- d) When each would be preferred

**30.** Explain the concept of "time borrowing" in latch-based designs. How does this differ from flip-flop-based designs? What is the trade-off?

---

## Section IV: Design Problems (3 questions, 15 points each)

### Problem 31: Logical Effort Path Optimization

You need to design a path from an inverter driving a load of 64 units through a chain of gates. The path consists of: INV → NAND2 → NOR2 → Load.

**Given:**
- g_inv = 1, p_inv = 1
- g_nand2 = 4/3, p_nand2 = 2
- g_nor2 = 5/3, p_nor2 = 2
- Input capacitance of inverter = 1 unit
- Load capacitance = 64 units

**a)** Calculate the path logical effort G, electrical effort H, and path effort F.

**b)** Is the number of stages optimal? Calculate the best number of stages.

**c)** Should you add buffers? If so, where and how many?

**d)** Calculate the estimated delay of your optimized path.

---

### Problem 32: Sequential Timing Analysis

Consider a synchronous circuit with the following parameters:
- Clock period T_c = 5 ns
- Clock skew t_skew = 0.3 ns (positive, clock arrives later at receiving flip-flop)
- Flip-flop: t_setup = 0.2 ns, t_hold = 0.15 ns, t_pcq = 0.4 ns, t_ccq = 0.25 ns
- Combinational logic: t_pd = 3.8 ns, t_cd = 1.2 ns

**a)** Verify that the setup time constraint is satisfied. Show your calculation.

**b)** Verify that the hold time constraint is satisfied. Show your calculation.

**c)** What is the maximum clock frequency this circuit can operate at?

**d)** If the clock skew increased to 0.5 ns, which constraint (setup or hold) would be violated first? Explain.

---

### Problem 33: Adder Architecture Design

You are designing a 64-bit adder for a processor.

**a)** Calculate the approximate delay (in number of gate delays) for:
   - A 64-bit ripple carry adder
   - A 64-bit carry-lookahead adder with 4-bit blocks
   - A 64-bit carry-skip adder with 8-bit groups

**b)** Sketch the architecture of a 4-bit carry-select adder showing how it computes the sum for both possible carry-in values.

**c)** For your application, low latency is critical but area is flexible. Which architecture would you choose and why? Consider both first-order delay and practical implementation issues.

**d)** How would your choice change if this were for a low-power IoT device where energy efficiency is paramount?

---

## Bonus Question (5 points)

**34.** In modern CMOS technology (7nm and below), leakage power can exceed dynamic switching power. Describe two circuit-level techniques and two architecture-level techniques to reduce leakage power. Explain the principle behind each technique and any performance trade-offs.

---

**End of Exam**

Good luck! Remember to show all work and explain your reasoning for full credit.