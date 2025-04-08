# Week 6

Great set of questions! Let’s break them down one by one:

---

### 🧮 **1. How to add, subtract, multiply, and divide complex numbers?**

A complex number looks like this:  
$$
z = a + bi
$$
where $ a $ is the real part, $ b $ is the imaginary part, and $ i $ is the imaginary unit ($ i^2 = -1 $).

#### ➕ Addition:
Just add real parts and imaginary parts:
$$
(3 + 2i) + (1 + 4i) = (3+1) + (2i + 4i) = 4 + 6i
$$

#### ➖ Subtraction:
Same idea—subtract corresponding parts:
$$
(5 + 3i) - (2 + i) = (5 - 2) + (3i - i) = 3 + 2i
$$

#### ✖️ Multiplication:
Use distributive property (FOIL) and $ i^2 = -1 $:
$$
(2 + 3i)(1 + 4i) = 2 + 8i + 3i + 12i^2 = 2 + 11i - 12 = -10 + 11i
$$

#### ➗ Division:
Multiply numerator and denominator by the **conjugate** of the denominator:

$$
\frac{3 + 2i}{1 - i} = \frac{(3 + 2i)(1 + i)}{(1 - i)(1 + i)} = \frac{3 + 3i + 2i + 2i^2}{1^2 - i^2} = \frac{3 + 5i - 2}{1 + 1} = \frac{1 + 5i}{2} = \frac{1}{2} + \frac{5}{2}i
$$

---

### 🪞 **2. What is the conjugate in complex numbers?**

The **conjugate** of a complex number $ z = a + bi $ is:
$$
\bar{z} = a - bi
$$

Useful for simplifying expressions, especially division. Also:
$$
z \cdot \bar{z} = a^2 + b^2 \quad \text{(a real number)}
$$

---

### 📉 **3. What is the complex plane?**

Think of it as a 2D coordinate plane:

- The **x-axis** represents the **real part**
- The **y-axis** represents the **imaginary part**

So the complex number $ 3 + 4i $ is a point (3, 4) on the complex plane.

This lets us visualize complex numbers as **vectors** with direction and length.

---

### 🧭 **4. What is the polar form of complex numbers?**

Polar form uses a number's **magnitude** and **angle** (like polar coordinates):

$$
z = r(\cos\theta + i\sin\theta)
$$

Or using Euler’s formula (next question):

$$
z = re^{i\theta}
$$

Where:
- $ r = |z| = \sqrt{a^2 + b^2} $ is the **magnitude**
- $ \theta = \arg(z) = \tan^{-1}\left(\frac{b}{a}\right) $ is the **angle** from the positive real axis

This form makes **multiplication/division** and **powers/roots** super easy.

---

### 📐 **5. How was Euler’s formula discovered by Leonhard Euler?**

Euler’s formula is:
$$
e^{i\theta} = \cos\theta + i\sin\theta
$$

Euler derived it using **Taylor series expansions**:

$$
\begin{align*}
e^x &= 1 + \frac{x}{1!} + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots \\
\cos x &= 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \cdots \\
\sin x &= x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots \\
\end{align*}
$$

Now substitute $ x = i\theta $ into the exponential series:
$$
e^{i\theta} = 1 + i\theta - \frac{\theta^2}{2!} - i\frac{\theta^3}{3!} + \frac{\theta^4}{4!} + i\frac{\theta^5}{5!} - \cdots
$$

Grouping real and imaginary terms gives:
$$
e^{i\theta} = \cos\theta + i\sin\theta
$$

It’s one of the most beautiful and useful formulas in math.

---

### 🎵 **6. Why do people sometimes represent sine signals as complex numbers?**

Because complex numbers make signal math **much easier**, especially in:

- Electrical Engineering
- RF Systems
- Signal Processing

Instead of messy sines and cosines, you can represent a sinusoid like:
$$
A\cos(\omega t + \phi) = \text{Re}\left[Ae^{i(\omega t + \phi)}\right]
$$

Then you can use **exponentials** to analyze systems (e.g., filters, impedance, Fourier analysis), and just take the real part at the end.

It turns differential equations into algebra, and multiplication into addition—clean and elegant!


---

# Week 7

### 🧮 **1. Polar Form of Complex Numbers: How to Perform Calculations Like Multiplication or Division**

When you have two complex numbers in **polar form**:

$$
z_1 = r_1 e^{i\theta_1}, \quad z_2 = r_2 e^{i\theta_2}
$$

#### ✅ Multiplication:
$$
z_1 \cdot z_2 = r_1 r_2 e^{i(\theta_1 + \theta_2)}
$$

- Multiply the **magnitudes**
- Add the **angles**

#### ➗ Division:
$$
\frac{z_1}{z_2} = \frac{r_1}{r_2} e^{i(\theta_1 - \theta_2)}
$$

- Divide the **magnitudes**
- Subtract the **angles**

This is **super clean** compared to multiplying/distributing in rectangular form!

---

### 🐍 **2. In Python (NumPy): Calculations on Complex Numbers**

NumPy supports both **rectangular** and **polar** forms, and it's easy to go between them.

#### 🔹 Rectangular form:

```python
import numpy as np

z1 = 3 + 4j
z2 = 1 - 2j

# Addition, multiplication, etc.
print(z1 + z2)       # Complex addition
print(z1 * z2)       # Complex multiplication
print(z1 / z2)       # Complex division
```

#### 🔹 Convert to Polar Form:

```python
r = np.abs(z1)             # Magnitude
theta = np.angle(z1)       # Angle (in radians)

print(f"Magnitude: {r}, Angle: {theta} radians")
```

#### 🔹 Create a Complex Number from Polar Form:

```python
r = 5
theta = np.pi / 4  # 45 degrees

z = r * np.exp(1j * theta)  # e^(iθ)
print(z)  # Back to rectangular form
```

So you can go **polar → rectangular** using `r * np.exp(1j * theta)`  
and **rectangular → polar** using `np.abs()` and `np.angle()`.

---

### 🛠️ **3. Engineering: When to Use Rectangular vs Polar Form**

#### ✅ **Rectangular Form** $ a + bi $
- Use when adding or subtracting complex quantities.
- Ideal for working with vectors, phasors, or coordinate-based problems.
- Preferred in circuit analysis involving:
  - **KCL, KVL** (voltage/current sums)
  - **Impedance** networks with resistors/capacitors/inductors

#### ✅ **Polar Form** $ re^{i\theta} $
- Use when multiplying, dividing, or taking powers/roots of complex numbers.
- Very useful in:
  - **AC circuit analysis** (phasors)
  - **Signal processing**, modulation
  - **Fourier transforms**
  - **Bode plots** (gain/phase)
  - **Filters and frequency response**

👉 TL;DR:
- **Add/Subtract → Rectangular**
- **Multiply/Divide/Exponentiate → Polar**

---

# Week 8

### 🎵 **1. Why does a sine response always keep the same frequency?**

#### 📘 Answer:
Because **linear time-invariant (LTI) systems** *don’t create new frequencies* — they only **scale** and **phase shift** the input.

#### ⚙️ Using Complex Exponential:
A sine wave can be written using Euler’s formula:

$$
\sin(\omega t) = \frac{1}{2i} \left(e^{i\omega t} - e^{-i\omega t}\right)
$$

When you input $ e^{i\omega t} $ into an LTI system with transfer function $ H(s) $, the output will be:

$$
Y(s) = H(s) \cdot \text{input}
$$

Plug in $ s = i\omega $:

$$
\text{Response} = H(i\omega) \cdot e^{i\omega t}
$$

So the system scales the amplitude and rotates the phase — **but keeps the frequency the same**.

Same idea applies to sine:
- Only **magnitude and phase** are changed.
- **Frequency stays the same**.

---

### 🧮 **2. Given a sine input and transfer function, how to find the output expression (e.g., on a TI/SAT calculator)?**

Let’s say:
- Input: $ \sin(\omega t) $
- System: $ H(s) $ is given (e.g. $ \frac{1}{s+1} $)

#### Steps:

1. **Laplace Transform of Input:**
   $$
   \mathcal{L}\{\sin(\omega t)\} = \frac{\omega}{s^2 + \omega^2}
   $$

2. **Multiply by Transfer Function:**
   $$
   Y(s) = H(s) \cdot \mathcal{L}\{\text{input}\}
   $$

3. **Inverse Laplace Transform:**  
   Use calculator/table to get back to time-domain.

**Example:**

Input: $ \sin(2t) $,  
System: $ H(s) = \frac{1}{s+1} $

$$
Y(s) = \frac{1}{s+1} \cdot \frac{2}{s^2 + 4}
$$

Then, partial fraction and invert using table (SAT calculators like TI-89 can help with this).  
Final output = transient + steady-state sine.

---

### 💡 **3. Why plug in $ s = j\omega $ into $ H(s) $? And is that only for sine inputs?**

Yes — **plugging $ s = j\omega $** is specifically used for **steady-state sinusoidal analysis**.

Here’s why:

- In Laplace Transform, $ s = \sigma + j\omega $
- But for **pure sinusoids**, the exponential part $ e^{\sigma t} $ vanishes in steady state.
- So we only care about $ s = j\omega $

#### ⚠️ Not for step/impulse:
- Those are **not sinusoids** — they contain multiple frequencies or are broad-spectrum.
- You have to keep **all s** terms and inverse Laplace the whole thing.

✅ **So only plug $ s = j\omega $** when the input is a **steady-state sinusoid** and you want to find the **output’s steady-state amplitude and phase.**

---

### 🔁 **4. Can you elaborate more on the meaning of $ s = j\omega $?**

Yes! In Laplace:
- $ s = \sigma + j\omega $
- The **real part $ \sigma $** represents **growth/decay**
- The **imaginary part $ \omega $** is the **oscillation frequency**

So:

- When we set $ s = j\omega $, we're asking:
  > "What is the system’s response to a sinusoidal input of frequency $ \omega $, once transients are gone?"

This gives you:
- The gain: $ |H(j\omega)| $
- The phase shift: $ \angle H(j\omega) $

It's the **core idea of frequency response analysis** — like Bode plots, filters, etc.

---

### ⏳ **5. Why do people mostly study steady-state sine response, not transient?**

Because in real engineering systems:

- Transients **die out** due to damping
- Steady-state tells you the **long-term behavior**
- Systems often operate under **continuous sinusoidal inputs** (AC power, RF signals, etc.)

Also:

- Sine response at all frequencies = **frequency response**
- You can reconstruct the system’s behavior for any input (via Fourier analysis)

So, engineers often:
- Ignore transients unless they’re critical (e.g., startup spikes)
- Focus on **frequency-domain analysis** for filtering, gain, phase margin, etc.

---

# Week 9


### 📊 **1. What information can I get from a Bode plot of a system $ H(s) $?**

A **Bode plot** is a pair of plots:

- **Magnitude plot**: Shows how much the system amplifies or attenuates each frequency  
  → Vertical axis: $ 20 \log_{10} |H(j\omega)| $ in **dB**  
  → Horizontal axis: frequency $ \omega $ in **log scale** (rad/s or Hz)

- **Phase plot**: Shows how much the system **shifts the phase** of the input signal at each frequency  
  → Phase in **degrees**, often from −180° to +180°

#### ✅ From a Bode plot, you can read:
- **Gain at any frequency** (how strong output is for a sine input at that frequency)
- **Phase shift at any frequency**
- **Bandwidth** (range of frequencies where system passes signal well)
- **Cutoff frequency** (where gain drops to 3 dB below max)
- **Filter behavior**: low-pass, high-pass, band-pass, etc.
- **Stability margins** (for feedback systems: phase/gain margin)

---

### 🛠️ **2. More details: What does the shape of the Bode plot tell me?**

Let’s say you have a transfer function:

$$
H(s) = \frac{1}{s + 1}
$$

Its Bode plot will show:
- At low frequencies ($ \omega \ll 1 $): magnitude ≈ 0 dB (passes input)
- At high frequencies ($ \omega \gg 1 $): magnitude drops ~20 dB/decade (attenuates)
- Phase shifts from 0° to −90° around cutoff $ \omega = 1 $

So: Bode plot tells you **how your system treats different frequency components**.

This is critical when you're working with:
- Communication signals
- Filters
- Amplifiers
- Control loops

---

### 🎚️ **3. How are filters related to Bode plots?**

Filters are systems that **prefer some frequencies** and **reject others**.

Using Bode plots, you can **see exactly which frequencies pass or get blocked**.

#### Examples:

- **Low-pass filter**: Passes low frequencies, attenuates high ones  
  → On Bode: flat gain at low freq, then drop-off after cutoff

- **High-pass filter**: Blocks low frequencies, passes high ones  
  → On Bode: gain increases after cutoff

- **Band-pass filter**: Passes a range, blocks above and below  
  → On Bode: a "hump" around a center frequency

- **Band-stop (notch)**: Opposite of band-pass  
  → On Bode: dip in gain at a specific frequency

#### Bode plot shows:
- Where gain is high → signal goes through
- Where gain is low → signal is blocked
- Phase → how signal is delayed or rotated in time

---

### 🎛️ **4. What does low-pass/high-pass filter mean, and how do they look on Bode plots?**

#### 🔻 Low-Pass Filter:

- **Definition**: Allows low frequencies to pass; blocks high frequencies.
- **Typical Transfer Function**:
  $$
  H(s) = \frac{1}{sRC + 1}
  $$
- **Bode Magnitude**:
  - Flat (0 dB) at low freq
  - Starts dropping at **cutoff** $ \omega_c = \frac{1}{RC} $
  - Slope: −20 dB/decade
- **Bode Phase**:
  - 0° at low freq
  - Drops to −90° at high freq

#### 🔺 High-Pass Filter:

- **Definition**: Allows high frequencies to pass; blocks low frequencies.
- **Typical Transfer Function**:
  $$
  H(s) = \frac{sRC}{sRC + 1}
  $$
- **Bode Magnitude**:
  - Starts low at low freq (−∞ dB)
  - Rises to 0 dB after cutoff
  - Slope: +20 dB/decade
- **Bode Phase**:
  - +90° at high freq
  - 0° at low freq

---

### 📷 Visual Summary:

(Just imagine for now — or I can generate a plot if you want)

#### Low-pass filter:
```
Magnitude:   _____________
                        \
                         \
                          \__  (drops 20 dB/dec)

Phase:       0° ----------- -90°
```

#### High-pass filter:
```
Magnitude:       _______
                /
               /
    __________/

Phase:       +90° -------- 0°
```

---

# Week 10

### 📐 **1. How is Bode Magnitude related to Input/Output signals?**

Bode **magnitude** shows how much the system **amplifies or attenuates** a sine wave **at a specific frequency**.

In plain terms:

- Input: $ x(t) = A \sin(\omega t) $
- Output (steady state): $ y(t) = A' \sin(\omega t + \phi) $
- Then:  
  $$
  \text{Magnitude} = \frac{A'}{A} = |H(j\omega)|
  $$

And in decibels (dB):

$$
\text{Bode Magnitude (dB)} = 20 \log_{10}\left(\frac{A'}{A}\right)
$$

So:  
- If $ \text{Bode Mag} = 0 \text{ dB} $: output amplitude = input amplitude  
- If $ \text{Bode Mag} = -6 \text{ dB} $: output is about half the input  
- If $ \text{Bode Mag} = +6 \text{ dB} $: output is about twice the input

> 🔑 **Bode Magnitude tells you:**
> - "How big is the output **sinusoid** compared to the input at this frequency?"

---

### 📉 **2. Interpreting Bode Magnitude: Examples**

Let’s say you're looking at the Bode magnitude plot at **1 Hz**:

#### a) **Bode Magnitude = −5 dB**
- This means the **output is smaller** than the input at 1 Hz
- Use the formula:
  $$
  \frac{A'}{A} = 10^{\frac{-5}{20}} \approx 0.56
  $$
- So the output amplitude is **about 56%** of the input amplitude
- Indicates the system is **attenuating** 1 Hz signals

#### b) **Bode Magnitude = +5 dB**
- Output is **larger** than input
- $$
  \frac{A'}{A} = 10^{\frac{5}{20}} \approx 1.78
  $$
- So the output amplitude is **about 1.78×** the input amplitude
- Indicates the system is **amplifying** 1 Hz signals

You can always reverse dB back to linear ratio with:
$$
\text{ratio} = 10^{(\text{dB}/20)}
$$

---

### ⚙️ **3. Comparison: Passive Filter vs Active Filter**

| Feature | **Passive Filter** | **Active Filter** |
|--------|------------------|------------------|
| **Components** | Resistors, Capacitors, Inductors | Resistors, Capacitors, plus **Op-Amps** or transistors |
| **Power** | **No external power** needed | Requires **external power** (for op-amp) |
| **Gain** | Cannot provide gain (only attenuate) | Can **amplify** signal (gain > 1) |
| **Size** | Inductors are bulky, especially at low freq | No inductors needed — compact design |
| **Impedance Matching** | Poor — may load source or load | Excellent buffering (due to op-amp) |
| **Cost** | Simple and low-cost | Slightly more expensive (op-amp, power) |
| **Stability** | Generally very stable | Can be unstable if poorly designed |
| **Frequency Range** | Good at high frequencies | Better for **low-to-mid frequencies** |
| **Example Circuit** | RC low-pass, RL high-pass | Op-amp active low-pass or band-pass filter |

---

### 📝 Summary:

- Use **passive filters** when you just need simple filtering without amplification — especially at high frequencies (RF circuits).
- Use **active filters** when:
  - You need gain,
  - You want sharper cutoff without inductors,
  - You're working at audio or baseband frequencies (like 10 Hz – 100 kHz),
  - You need better impedance control or integration into analog signal paths.

---
