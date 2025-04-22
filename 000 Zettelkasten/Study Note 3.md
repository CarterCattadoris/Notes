# Week 11

Let’s go step by step:

---

### ✅ PART 1: Derive Impulse Response Using Laplace and Inverse Laplace (sin only)

#### **System 1: $ H(s) = \dfrac{1}{s^2 + 4s + 1} $**

**Step 1: Input is impulse → $ X(s) = 1 $**

So output in Laplace:
$$
Y(s) = H(s) \cdot X(s) = \frac{1}{s^2 + 4s + 1}
$$

**Step 2: Complete the square**
$$
s^2 + 4s + 1 = (s + 2)^2 - 3
\Rightarrow Y(s) = \frac{1}{(s + 2)^2 - 3}
$$

**Step 3: Convert to standard inverse Laplace**
$$
Y(s) = \frac{1}{(s + 2)^2 - (\sqrt{3})^2}
\Rightarrow Y(t) = \frac{1}{\sqrt{3}} e^{-2t} \sin(\sqrt{3} t) u(t)
$$

---

#### **System 2: $ H(s) = \dfrac{4}{s^2 + 4s + 4} $**

**Step 1:**
$$
Y(s) = \frac{4}{s^2 + 4s + 4} = \frac{4}{(s + 2)^2}
$$

**Step 2: Use inverse Laplace of $ \frac{1}{(s+a)^2} = t e^{-at} $**

So:
$$
Y(t) = 4t e^{-2t} u(t)
$$

---

#### **System 3: $ H(s) = \dfrac{25}{s^2 + 4s + 25} $**

**Step 1:**
$$
s^2 + 4s + 25 = (s + 2)^2 + 21
\Rightarrow Y(s) = \frac{25}{(s + 2)^2 + (\sqrt{21})^2}
$$

**Step 2: Use inverse Laplace**
$$
\mathcal{L}^{-1} \left\{ \frac{\omega}{(s + a)^2 + \omega^2} \right\} = e^{-at} \sin(\omega t)
$$

We match form:
$$
\frac{25}{(s + 2)^2 + (\sqrt{21})^2} = \frac{25}{\sqrt{21}} \cdot \frac{\sqrt{21}}{(s + 2)^2 + 21}
$$

So:
$$
Y(t) = \frac{25}{\sqrt{21}} e^{-2t} \sin(\sqrt{21} t) u(t)
$$

---

### ✅ PART 2: Python Code to Plot Impulse and Step Responses

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import TransferFunction, impulse, step

# Define systems
systems = [
    TransferFunction([1], [1, 4, 1]),   # H1(s)
    TransferFunction([4], [1, 4, 4]),   # H2(s)
    TransferFunction([25], [1, 4, 25])  # H3(s)
]

time = np.linspace(0, 10, 1000)

# Plot impulse responses
plt.figure(figsize=(12, 6))
plt.subplot(2, 1, 1)
for i, sys in enumerate(systems, 1):
    t, y = impulse(sys, T=time)
    plt.plot(t, y, label=f'H{i}(s) impulse')
plt.title('Impulse Responses')
plt.xlabel('Time [s]')
plt.ylabel('Amplitude')
plt.legend()
plt.grid(True)

# Plot step responses
plt.subplot(2, 1, 2)
for i, sys in enumerate(systems, 1):
    t, y = step(sys, T=time)
    plt.plot(t, y, label=f'H{i}(s) step')
plt.title('Step Responses')
plt.xlabel('Time [s]')
plt.ylabel('Amplitude')
plt.legend()
plt.grid(True)

plt.tight_layout()
plt.show()
```

---

### ✅ PART 3: Interpretation of Differences

- **H1(s):** Underdamped system — decaying oscillation with frequency $ \sqrt{3} $.
- **H2(s):** Critically damped — no oscillation, fastest return to equilibrium.
- **H3(s):** Underdamped — oscillates more rapidly with $ \sqrt{21} $, but decays slower due to lower gain factor.

---

### ✅ PART 4: Why Analyze the Roots of Denominator?

The denominator (characteristic polynomial) determines **pole locations**, which directly dictate:

- **Stability:** If any pole has positive real part → unstable.
- **Damping:** Real roots → overdamped or critically damped. Complex → underdamped.
- **Natural frequency & damping ratio:** Control oscillation and decay behavior.

The pole positions in the complex plane **control time-domain behavior** entirely.

Would you like me to generate the actual plots too?

# Week 12

Absolutely—let’s go through each question step by step.

---

### ✅ What is a **State-Space Model** for Linear Time-Invariant (LTI) Systems?

A **state-space model** is a **mathematical framework** used to model and analyze dynamic systems by expressing them as a system of **first-order differential equations**.

A **continuous-time state-space model** has the form:
$$
\begin{aligned}
\dot{x}(t) &= A x(t) + B u(t) \\
y(t) &= C x(t) + D u(t)
\end{aligned}
$$
Where:
- $ x(t) $ is the **state vector** (internal variables of the system)
- $ u(t) $ is the **input**
- $ y(t) $ is the **output**
- $ A, B, C, D $ are matrices that describe the system dynamics

This model is **linear** if all equations are linear, and **time-invariant** if the matrices $A, B, C, D$ do not change over time.

---

### ✅ 3 Real-World Examples of LTI Systems in State-Space Form

#### 1. **Mass-Spring-Damper System**
- 2nd-order system
- States: position $x$, velocity $\dot{x}$
- Input: external force $F(t)$
- Output: position or velocity

#### 2. **Electrical RLC Circuit**
- Components: resistor (R), inductor (L), capacitor (C)
- States: capacitor voltage and inductor current
- Input: voltage source
- Output: current or voltage across components

#### 3. **Aircraft Pitch Dynamics**
- States: pitch angle, pitch rate
- Input: elevator deflection
- Output: pitch angle
- Used for designing autopilots and stability augmentation systems

---

### ✅ Detailed Meaning of the 4 State-Space Matrices

$$
\dot{x}(t) = A x(t) + B u(t) \\
y(t) = C x(t) + D u(t)
$$

| Matrix | Size             | Meaning |
|--------|------------------|---------|
| $A$  | $n \times n$   | **System matrix** – defines how current state affects its derivative (internal dynamics) |
| $B$  | $n \times m$   | **Input matrix** – defines how inputs affect the state |
| $C$  | $p \times n$   | **Output matrix** – maps internal states to outputs |
| $D$  | $p \times m$   | **Feedthrough matrix** – direct mapping from input to output (instantaneous) |

- $n$: number of states
- $m$: number of inputs
- $p$: number of outputs

---

### ✅ If I Have a 3rd-Order ODE System, What Are the Dimensions?

For a **3rd-order differential equation**, you need to define 3 **states** (typically the variable and its first two derivatives). Therefore:

- $x(t)$ is 3×1 → 3 state variables
- So:

| Matrix | Size        |
|--------|-------------|
| $A$  | $3 \times 3$ |
| $B$  | $3 \times 1$ |
| $C$  | $1 \times 3$ |
| $D$  | $1 \times 1$ |

(assuming 1 input and 1 output)

---

### ✅ Advantages of State-Space Models vs Transfer Functions

| Advantage | Description |
|----------|-------------|
| ✅ **Can Model MIMO Systems** | State-space handles **multiple inputs and outputs (MIMO)**; transfer functions are mostly for SISO. |
| ✅ **Models Internal States** | Gives insight into internal dynamics (e.g., position and velocity), not just input-output behavior. |
| ✅ **Handles Initial Conditions** | Can include and simulate arbitrary initial state values directly. |
| ✅ **Easier for Modern Control** | Methods like pole placement, LQR, observer design, and Kalman filters all rely on state-space. |
| ✅ **Well-Suited for Computers** | Easy to discretize and simulate numerically. |

---

Would you like a worked example converting a 3rd-order ODE to state-space form?

# Week 13

Great set of questions! Let’s walk through them clearly and concisely.

---

### ✅ Difference Equations vs Differential Equations

| Concept                 | **Difference Equation**                             | **Differential Equation**                           |
|------------------------|------------------------------------------------------|-----------------------------------------------------|
| Domain                 | **Discrete-time** (e.g., digital systems)            | **Continuous-time** (e.g., analog systems)          |
| Function Notation      | $ y[n] $, $ x[n] $ (indexed by integers)         | $ y(t) $, $ x(t) $ (functions of continuous time) |
| Operation              | Uses **differences**: $ y[n] - y[n-1] $, etc.      | Uses **derivatives**: $ \frac{dy}{dt} $, etc.     |
| Common in              | Digital signal processing, digital control systems  | Electrical circuits, mechanical systems             |
| Tool                   | **Z-transform**                                      | **Laplace transform**                               |

---

### ✅ How Does a First-Order Difference Equation Look Like?

A **first-order linear difference equation** has this general form:
$$
y[n] - a\, y[n-1] = b\, x[n]
$$
Where:
- $y[n]$ is the output
- $x[n]$ is the input
- $a$, $b$ are constants

This is the discrete-time analog of a first-order ODE:
$$
\frac{dy}{dt} + a y(t) = b x(t)
$$

---

### ✅ What is the **Z Transform**?

The **Z-transform** converts a discrete-time signal $x[n]$ into a complex frequency domain representation:
$$
X(z) = \sum_{n=0}^{\infty} x[n] z^{-n}
$$

It’s the **discrete-time equivalent** of the Laplace Transform.

- Helps analyze **linear time-invariant (LTI)** discrete systems
- Converts difference equations into algebraic equations in $z$
- Solves systems using algebra, then applies **inverse Z-transform** to get back time-domain

---

### ✅ Z-Transform of Basic Signals

| Signal         | Z-Transform $X(z)$ | ROC (Region of Convergence)      |
|----------------|----------------------|----------------------------------|
| Unit impulse $ \delta[n] $ | $1$                | Entire $z$-plane               |
| Unit step $ u[n] $         | $ \frac{1}{1 - z^{-1}} $ | $ |z| > 1 $                    |

---

### ✅ How to Use Z-Transform to Solve First-Order Difference Equation?

**Given:**  
$$
y[n] - a\, y[n-1] = b\, x[n] \quad \text{with } x[n] = \delta[n] \text{ (impulse input)}
$$

**Step 1: Take Z-transform**
$$
Y(z) - a\, z^{-1} Y(z) = b
\Rightarrow Y(z)(1 - a z^{-1}) = b
\Rightarrow Y(z) = \frac{b}{1 - a z^{-1}} = \frac{b z}{z - a}
$$

**Step 2: Inverse Z-transform**
$$
y[n] = b a^n u[n]
$$

This is the **impulse response** of the system.

---

### ✅ What is **Sampling Time** in Digital Systems?

**Sampling Time (Tₛ)** is the interval between successive samples when converting a continuous-time signal to discrete-time:

- If analog signal is $ x(t) $, the sampled signal is $ x[n] = x(nT_s) $
- Units: seconds/sample
- Defines **how fast the system updates** (like in a microcontroller or DSP)
- Sampling rate: $ f_s = \frac{1}{T_s} $ (samples per second)

**Why important?**
- It determines **system bandwidth**, aliasing behavior, and **accuracy of digital representation**
- Used in **discretizing** continuous systems (e.g., for digital control design)

---

Would you like a worked example showing how to solve a difference equation using Z-transform with a specific input (like unit step)?

# Week 14

Excellent, in-depth questions! Let’s break it down clearly.

---

### ✅ Why Do Digital Systems Require Discrete-Time Models?

Digital systems (like microcontrollers, digital filters, computers) **cannot process continuously-varying signals**. Instead:

- They operate in **discrete time** (step-by-step).
- All signals and controllers must be **sampled and digitized**.
- Real sensors and actuators are connected through **ADC/DAC** which bridge continuous (physical world) and discrete (digital controller).

Thus, to **analyze or control** real-world systems digitally, we **convert continuous models into discrete-time equivalents**.

---

### ✅ Real-World Applications That Require Discretization

1. **Digital Control Systems**  
   - Aircraft autopilots, self-driving cars, and robots use sampled feedback control.

2. **Signal Processing**  
   - Audio, biomedical signals (ECG), image processing: all use discrete-time filters (FIR/IIR).

3. **Simulation/Testing**  
   - Real-time simulation or model-in-the-loop (MIL) testing uses discrete-time plant models.

4. **Embedded Systems**  
   - Systems built on DSPs, FPGAs, or microcontrollers must discretize all continuous equations for implementation.

---

### ✅ Introduction to Discretization of Transfer Functions

Given a continuous-time system:
$$
H(s) = \frac{N(s)}{D(s)}
$$
We discretize it into:
$$
H(z) = \frac{N(z)}{D(z)}
$$
where $z$ is the **discrete-time complex variable** (analog of $s$).

---

### ✅ Why Do We Discretize Transfer Functions?

- To **implement** controllers/filters in digital processors.
- To **simulate** system response on a computer.
- To **analyze** stability and performance of digital control systems.

---

### ✅ Common Discretization Methods

| Method | Description | Mapping |
|--------|-------------|---------|
| **ZOH (Zero-Order Hold)** | Assumes input held constant over sample interval | $ z = e^{sT} $ |
| **Bilinear (Tustin)** | Warps s-plane to z-plane using trapezoidal rule | $ s = \frac{2}{T} \cdot \frac{z - 1}{z + 1} $ |
| **Forward Euler** | Simple, less accurate | $ s \approx \frac{z - 1}{T} $ |
| **Backward Euler** | Slightly more stable | $ s \approx \frac{1 - z^{-1}}{T} $ |

---

### ✅ How to Use `scipy.signal.cont2discrete` + Visualize

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import cont2discrete, TransferFunction

# Continuous system
num = [1]
den = [1, 3]  # H(s) = 1 / (s + 3)
sys = TransferFunction(num, den)

T = 0.1  # Sample time

# Discretize using different methods
methods = ['zoh', 'bilinear', 'euler', 'backward_diff']
systems_d = {}
for method in methods:
    d_sys = cont2discrete((num, den), T, method=method)
    systems_d[method] = d_sys

# Plot poles on complex plane
plt.figure(figsize=(8, 6))
for method, (num_d, den_d, dt) in systems_d.items():
    poles = np.roots(den_d)
    plt.plot(np.real(poles), np.imag(poles), 'o', label=method)

plt.axhline(0, color='gray', lw=1)
plt.axvline(0, color='gray', lw=1)
plt.title('Pole Mapping Under Different Discretization Methods')
plt.xlabel('Re(z)')
plt.ylabel('Im(z)')
plt.legend()
plt.grid(True)
plt.axis('equal')
plt.show()
```

---

### ✅ Pole Mapping Example

Given: continuous-time pole at $ s = -3 $, sample time $ T = 0.1 $

#### 1. **ZOH Mapping**
$$
z = e^{sT} = e^{-3 \cdot 0.1} = e^{-0.3} \approx 0.7408
$$
- So the discrete-time pole is at $ z \approx 0.7408 $

#### 2. **Bilinear (Tustin) Mapping**
$$
s = \frac{2}{T} \cdot \frac{z - 1}{z + 1} \Rightarrow z = \frac{1 + \frac{sT}{2}}{1 - \frac{sT}{2}} \\
z = \frac{1 + (-3)(0.1)/2}{1 - (-3)(0.1)/2} = \frac{1 - 0.15}{1 + 0.15} = \frac{0.85}{1.15} \approx 0.7391
$$

Both map into the **stable region inside the unit circle** but use different approximations.

---

Would you like to also compare the impulse or step response of these methods in Python plots?