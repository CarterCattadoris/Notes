
# VLSI Design Study Guide

## 1. Combinational Circuit Design

### Logical Effort
**Purpose:** Method to make design decisions about circuit topology, number of stages, and transistor sizing.

**Key Concepts:**
- **Delay Model:** d = f + p (effort delay + parasitic delay)
- **Logical Effort (g):** Ratio of input capacitance of a gate to an inverter delivering the same output current
  - Inverter: g = 1 (by definition)
  - NAND2: g = 4/3
  - NAND3: g = 5/3
  - NAND4: g = 6/3 = 2
  - NOR2: g = 5/3
  - NOR3: g = 7/3
  - NOR4: g = 9/3 = 3
  - General: NAND(n) = (n+2)/3, NOR(n) = (2n+1)/3
  - Tristate/mux: g = 2
  - XOR/XNOR: g = 4
- **Electrical Effort (h):** h = Cout/Cin (fanout ratio)
- **Parasitic Delay (p):** Intrinsic delay of gate driving no load
  - Inverter: p = 1
  - NAND/NOR (n inputs): p = n
  - Tristate/mux: p = 2n
- **Stage Effort (f):** f = g × h

**Path Optimization:**
- Best number of stages: N = log₄(F)
- Optimal stage effort: f̂ = F^(1/N)
- Minimum delay: D = NF^(1/N) + P
- Delay is smallest when each stage bears the same effort
- Paths are fastest when effort delays are ~4

**Methodology:**
1. Compute path effort (F = GBH)
   - G = product of logical efforts
   - B = branching effort
   - H = electrical effort (path)
2. Estimate best number of stages: N = log₄(F)
3. Sketch path with N stages
4. Estimate least delay: D = NF^(1/N) + P
5. Determine best stage effort: f̂ = F^(1/N)
6. Find gate sizes: Cin = (gi × Cout)/f̂

**Key Insights:**
- NANDs are faster than NORs in CMOS
- Path delay ≈ log₄(F) FO4 inverter delays
- Inverters and NAND2 best for driving large capacitances

**FO4 Delay Reference:**
- 180nm process: ~60 ps
- General: f/3 ns in f μm process (or f/3 ps in f nm process)

### Computing Logical Effort
**Method:** Count transistor widths
- For NAND2: Input capacitance = 4 (two inputs, each sees 2+2)
  - g = 4/3 (compared to inverter with input capacitance 3)
- For each input of a multi-input gate!

### Skewed Gates
**Purpose:** Optimize for input-dependent delays
- **HI-skew:** Favor rising output (larger PMOS)
- **LO-skew:** Favor falling output (larger NMOS)
- **Unskewed:** Balanced transistors

### Asymmetric Gates
**Purpose:** Favor one input over another
- Use smaller transistor on critical input (less capacitance)
- Boost size of non-critical inputs
- Maintain total resistance constant

### Device Sizing
- **Standard cell designs:** Gate sizing (INV-A, INV-B, INV-C with different drive strengths)
- **Custom designs:** Transistor-level sizing for critical paths
- Use wider transistors on critical paths
- Consider eliminating output inverters in layout

### Limitations of Logical Effort
- Neglects input rise time effects
- Iteration required for designs with interconnect
- Chicken-and-egg problem (need path to compute G)
- Maximum speed only, not minimum area/power

---

## 2. Clocking and Sequential Elements

### Latches vs. Flip-Flops
**Latch:** Level-sensitive (transparent when clock is high/low)
- Data passes through when clock is active

**Flip-Flop:** Edge-triggered (built from back-to-back latches)
- Master-slave configuration
- Captures data on clock edge only

### Timing Parameters
- **tpcq:** Latch/Flop propagation delay (clk to Q)
- **tccq:** Latch/Flop contamination delay (clk to Q)
- **tpdq:** Latch D-Q propagation delay
- **tcdq:** Latch D-Q contamination delay
- **tsetup:** Setup time (data must be stable before clock edge)
- **thold:** Hold time (data must be stable after clock edge)
- **tpd:** Logic propagation delay
- **tcd:** Logic contamination delay

### Timing Constraints
**Setup Time Constraint (Max-Delay):**
- Ensures data arrives in time before next clock edge
- Tclk ≥ tpcq + tpd + tsetup

**Hold Time Constraint (Min-Delay):**
- Ensures data doesn't change too quickly after clock edge
- tcd ≥ thold - tccq

### Sequencing Elements

**Static Latches:**
- Tristate feedback: Static but backdriving risk
- Buffered input: Reduces noise susceptibility, non-inverting
- Buffered output: No backdriving, widely used in standard cells
  - Very robust (most important)
  - Rather large
  - Rather slow (1.5-2 FO4 delays)
  - High clock loading
- Essential for DSM (Deep Sub-Micron) applications

**Flip-Flops:**
- Very easy to use, supported by all tools
- No time borrowing capability

**2-Phase Transparent Latches:**
- Lots of skew tolerance and time borrowing
- Supported by most tools
- Can cause timing loops

**Pulsed Latches:**
- Fast, some skew tolerance & borrow
- Hold time risk

### Safe Flip-Flops
- Use non-overlapping clocks
- Very slow (non-overlap adds to setup time)
- **But no hold times**
- In industry: use better timing analyzer, add buffers to slow signals if hold time at risk

### Shift Registers
- Store and delay data
- Simple design: cascade of registers
- **Critical: Watch your hold times!**

### Clock Distribution
**Clock Skew:** Variations in clock arrival time at different elements

**Clock Jitter:** Variations in clock period

**Minimizing Skew:**
- Use H-tree or matched-tree distribution structures
- Balance clock paths
- On small chips: just a wire (possibly with inverter for clk')
- On practical chips: RC delay causes significant skew
- Use repeaters to buffer clock and equalize delay
  - Amplifies and reshapes clock signal
  - Reduces but does not eliminate skew
- Route data and clock in opposite directions (eliminates races, costs performance)
- Align arrival times of data and clock signals (longer routing, higher complexity)

**Note:** A race occurs when timing of signals causes incorrect data capture

**Gated Clocks:**
- Help reduce dynamic power consumption
- Make jitter worse

**Clock Shielding:**
- Route power lines (VDD or GND) next to clock lines
- Minimizes/eliminates coupling with neighboring signal nets

### Time Borrowing (2-Phase Latches)
- Allows borrowing time between pipeline stages
- Provides skew tolerance
- Can compensate for imbalanced logic delays

---

## 3. Adders

### Propagate, Generate, Kill (PGK)
**Basic Definitions:**
- **Generate (G):** Cout = 1 independent of Cin → G = A · B
- **Propagate (P):** Cout = Cin → P = A ⊕ B
- **Kill (K):** Cout = 0 independent of Cin → K = ~A · ~B (i.e., ~K = A + B)

**Key Equations:**
- Sum: S = A ⊕ B ⊕ Cin = P ⊕ Cin
- Carry: Cout = A·B + A·Cin + B·Cin = G + P·Cin

**Group Operations:**
- Propagate and generate can be computed for groups spanning i:j
- Allows hierarchical adder designs

### Adder Architectures

**Ripple Carry Adder:**
- Simplest design: cascade full adders
- Critical path from Cin to Cout through all stages
- Slow for large bit-widths (delay proportional to N)
- Design full adder to have fast carry delay

**Carry-Lookahead Adder:**
- Computes group generate/propagate (Gi:0) for many bits in parallel
- Uses higher-valency cells with more than two inputs
- Much faster than ripple carry
- More complex hardware

**Carry-Skip Adder:**
- Ripple carry is slow through all N stages
- Allows carry to skip over groups of n bits
- Decision based on n-bit propagate signal
- Compromise between ripple carry and carry-lookahead
- Moderate complexity and speed

**Carry-Select Adder:**
- Compute sums for both Cin = 0 and Cin = 1 in parallel
- Select correct result when carry arrives
- Faster but uses more area

**Carry-Increment Adder:**
- Factor initial PG and final XOR out of carry-select
- Optimization of carry-select approach

### Carry Propagate Adders (CPA)
- N-bit adder where each sum bit depends on all previous carries
- Challenge: compute all carries quickly
- Critical path determines overall adder speed

### Layout Considerations
- Clever layout circumvents usual line of diffusion
- Use wide transistors on critical path
- Eliminate output inverters where possible
- Consider transistor placement for minimal diffusion capacitance

---

## 4. Datapath Design

### Multipliers

**Array Multiplier:**
- Uses Carry-Save Adders (CSA) in array
- Final Carry-Propagate Adder (CPA) at bottom
- Critical path goes through array and final CPA
- Combinational design (no clock required)

**Shift-Add Multiplier:**
- Sequential design (datapath + control)
- Components:
  - 64-bit Multiplicand register (with shift left)
  - 64-bit ALU
  - 64-bit Product register (with write)
  - 32-bit Multiplier register (with shift right)
- Examines multiplier bits one at a time
- Conditionally adds and shifts

**Carry-Save vs Carry-Propagate:**
- Carry-save: faster intermediate stages (3:2 compression)
- Carry-propagate: needed for final result

### Shifters

**Funnel Shifter:**
- Selects N-bit field Y from 2N-bit input
- Can shift by k bits (0 ≤ k < N)
- Can perform all six shift types:
  - Logical left/right
  - Arithmetic left/right
  - Rotate left/right

**Logarithmic Barrel Shifter:**
- Multiple stages of multiplexers
- Each stage shifts by power of 2 (1, 2, 4, 8, ...)
- Total shift = sum of stage shifts

**Evolution of Barrel Shifter:**
1. Right shift only (basic)
2. Right/Left shift (add preshift stage or control logic)
3. Right/Left Shift & Rotate (add mask and sign control)

**32-bit Logarithmic Barrel Shifter:**
- Datapath never wider than 32 bits
- First stage preshifts by 1 to handle left shifts
- Stages for: 1, 2, 4, 8, 16 bit shifts
- 5 control bits select total shift amount

**Simplified Funnel Shifter:**
- Alternative implementation
- Reduces complexity compared to full funnel shifter

**ARM Barrel Shifter (Application Example):**
- Used for second operand in ALU operations
- Register with optional shift operation
- Shift value can be:
  - 5-bit unsigned integer
  - Specified in bottom byte of another register
- Immediate value: 8-bit number rotated right through even number of positions
- Assembler calculates rotate from constant

---

## 5. Interconnects in CMOS Design

### Key Principles
**"Chips are mostly made of wires called interconnect"**
- In stick diagrams, wires set size
- Transistors are little things under the wires
- Many layers of wires

**Wires are as important as transistors for:**
- Speed
- Power
- Noise

### Wire Layers
Alternating layers run orthogonally:
- **HVH:** M1 Horizontal, M2 Vertical, M3 Horizontal, M4 Vertical
- **VHV:** M1 Vertical, M2 Horizontal, M3 Vertical, M4 Horizontal

### Diffusion & Polysilicon
**Diffusion:**
- Very high capacitance (~2 fF/μm, comparable to gate capacitance)
- High resistance
- **Avoid using diffusion runners for wires!**

**Polysilicon:**
- Lower capacitance but high resistance
- Use for transistor gates
- Only for very short wires between gates

### Wire Characteristics
**Capacitance:**
- Ctotal = Ctop + Cbot + 2Cadj
- Capacitance to neighbors and layers above/below
- Wire has capacitance per unit length

**Resistance:**
- Wire has resistance per unit length
- Example: R = 2.5 kΩ·μm for gates

### RC Delay
**Critical Concept:** RC delay is proportional to L²
- R and C are proportional to wire length L
- For long wires, delay becomes unacceptably large
- Example: 10× inverter driving 2× inverter through 5mm wire can have tpd = 1.1 ns

**Repeaters (Buffers):**
- Break long wires into N shorter segments
- Drive each segment with inverter or buffer
- Reduces delay from L² to approximately linear
- Design questions:
  - How many repeaters should we use?
  - How large should each one be?
- Equivalent circuit considerations:
  - Wire length l with capacitance Cw·l and resistance Rw·l
  - Inverter width W (nMOS = W, pMOS = 2W)
  - Gate capacitance C'·W and resistance R/W

### Crosstalk
**Definition:** Capacitive coupling between adjacent wires

**Cause:** A capacitor does not like to change voltage instantaneously. Wire has high capacitance to neighbor. When neighbor switches, the wire tends to switch too.

**Effects:**
- Noise on non-switching wires
- Increased delay on switching wires
- Called capacitive coupling

### Noise Implications
- Static CMOS eventually settles even with large noise spikes
  - But glitches cause extra delay
  - Also cause extra power from false transitions
- **Dynamic logic never recovers from glitches**
- Memories and other sensitive circuits can produce wrong answers
- Important to stay within noise margins

### Contribution of Wires (They Are Not Free!)
- **Delay:** Function of R, L, C, via resistance, local vs. global
- **Power:** Charging/discharging C (CV²f)
- **Noise:** Attackers/victims impact functionality and delay
- **Power supply IR drops and ground bounce:** Affects timing, leads to timing failures
- **Reliability:** Electromigration, self-heat, maximum current
- **Cost:** Number of layers vs. area/performance targets, yield

---

## 6. CMOS Gate Design

### Logical Effort of Common Gates

| Gate Type | 1 | 2 | 3 | 4 | n |
|-----------|---|---|---|---|---|
| Inverter | 1 | - | - | - | - |
| NAND | - | 4/3 | 5/3 | 6/3 | (n+2)/3 |
| NOR | - | 5/3 | 7/3 | 9/3 | (2n+1)/3 |
| Tristate/mux | 2 | 2 | 2 | 2 | 2 |
| XOR, XNOR | 4, 4 | 6, 12, 6 | 8, 16, 16, 8 | - | - |

### Parasitic Delay of Common Gates
(In multiples of pinv ≈ 1)

| Gate Type | 1 | 2 | 3 | 4 | n |
|-----------|---|---|---|---|---|
| Inverter | 1 | - | - | - | - |
| NAND | - | 2 | 3 | 4 | n |
| NOR | - | 2 | 3 | 4 | n |
| Tristate/mux | 2 | 4 | 6 | 8 | 2n |
| XOR, XNOR | - | 4 | 6 | 8 | - |

### Key Insights
- **NANDs are faster than NORs in CMOS**
- Inverter has best (lowest) logical effort
- Logical effort increases with number of inputs
- NOR gates have higher logical effort than NAND gates

### Skewed Gates Catalog
Gates can be designed with different pull-up (gu) and pull-down (gd) strengths:
- **HI-skew:** Favors rising output (stronger PMOS)
- **LO-skew:** Favors falling output (stronger NMOS)
- **Unskewed:** Balanced design

Average logical effort: gavg = (gu + gd)/2

---

## 7. Layout Considerations

### Critical Layout Principles
- Clever layout circumvents usual line of diffusion
- Use wide transistors on critical path
- Eliminate output inverters where possible

### Example: Efficient Layout
- Shared diffusion contacts between adjacent transistors
- Minimize diffusion area (reduces capacitance)
- Optimize transistor placement for signal flow
- Consider routing layers carefully

### Transistor Sizing in Layout
- nMOS vs pMOS sizing affects layout area
- Typical ratio: pMOS = 2× nMOS width (for equal drive strength)
- Critical paths may use wider transistors

---

## 8. Key Formulas & Relationships

### Logical Effort
- d = f + p = gh + p
- f̂ = F^(1/N)
- D = NF^(1/N) + P
- N = log₄(F)
- F = GBH (path effort = logical × branching × electrical)
- Cin = (gi × Cout)/f̂

### Timing
- Tclk ≥ tpcq + tpd + tsetup (setup constraint)
- tcd ≥ thold - tccq (hold constraint)

### Adders
- S = A ⊕ B ⊕ Cin = P ⊕ Cin
- Cout = G + P·Cin
- G = A·B (generate)
- P = A⊕B (propagate)
- K = ~A·~B (kill)

### Interconnect
- RC delay ∝ L²
- Ctotal = Ctop + Cbot + 2Cadj
- Repeaters reduce delay from L² to linear

---

## 9. Important Design Principles

1. **Speed-Power-Area Tradeoffs:** Most design decisions involve balancing these three metrics

2. **Critical Path Optimization:** 
   - Identify critical paths
   - Size transistors appropriately using logical effort
   - Minimize stages of logic (but not always fewer = faster!)
   - Consider using asymmetric gates for input-critical paths

3. **Clock Domain Management:**
   - Minimize skew with balanced distribution trees
   - Handle hold time violations with buffers
   - Consider time borrowing with 2-phase latches
   - Shield clock lines from noise

4. **Layout Matters:**
   - Diffusion is expensive (high C and R)
   - Wire planning is critical for long interconnects
   - Use repeaters for long wires
   - Clever layout can improve performance significantly

5. **Gate Selection:**
   - NANDs preferred over NORs
   - Inverters best for driving large loads
   - Consider skewed gates for specific applications

6. **Noise Management:**
   - Crosstalk between wires
   - Power supply noise (IR drops, ground bounce)
   - Clock jitter
   - Static vs dynamic logic considerations

7. **Tools & Methodologies:**
   - Logical effort for back-of-envelope calculations
   - Timing analysis for constraint verification
   - Spreadsheet comparisons for design alternatives

---

## 10. Common Design Mistakes to Avoid

- Using diffusion for routing (too much capacitance and resistance)
- Ignoring hold time constraints (especially in shift registers)
- Oversizing all transistors (wastes area and power)
- Undersizing critical path transistors
- Not considering wire delay in long interconnects
- Poor clock distribution causing excessive skew
- Assuming fewer stages always means faster paths
- Not checking for timing races in opposite-direction routing
- Ignoring crosstalk effects on delay and noise
- Forgetting that dynamic logic doesn't recover from glitches

---

## 11. Design Comparison Example: 4-bit Decoder

When comparing multiple designs, use spreadsheet analysis:

| Design | N stages | G | P | D (delay) |
|--------|----------|---|---|-----------|
| NAND4-INV | 2 | 2 | 5 | 29.8 |
| NAND2-NOR2 | 2 | 20/9 | 4 | 30.1 |
| INV-NAND4-INV | 3 | 2 | 6 | 22.1 |
| NAND4-INV-INV-INV | 4 | 2 | 7 | 21.1 |
| NAND2-NOR2-INV-INV | 4 | 20/9 | 6 | 20.5 |
| NAND2-INV-NAND2-INV | 4 | 16/9 | 6 | 19.7 |

**Key Insight:** More stages can be faster when properly optimized!

---

## Study Tips

1. **Master logical effort calculations** - Practice by hand with different gate combinations
2. **Work timing constraint problems** - Vary clock periods and see effects on setup/hold
3. **Understand adder tradeoffs** - Know when to use ripple, carry-lookahead, or carry-skip
4. **Practice wire delay calculations** - Include repeater analysis
5. **Draw circuit diagrams** - Helps understand signal flow and critical paths
6. **Compare design alternatives** - Use spreadsheets like the decoder example
7. **Know the formulas** - Especially logical effort, timing, and RC delay relationships
8. **Understand physical implications** - Connect circuit design to layout concerns
