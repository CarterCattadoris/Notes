202502091518
Status: #idea
Tags:[[Linear Systems (ELE251)]]

# Week 4
### **1. What is the Usage of Transfer Function in System Modeling and Analysis?**
The **transfer function** is a powerful tool that helps engineers and scientists **analyze and model dynamic systems**. It simplifies system behavior by converting complex differential equations into algebraic equations in the **Laplace domain**.

#### **Why Do We Use Transfer Functions?**
✅ **Predict System Behavior**: It describes how an input affects an output.  
✅ **Solve Differential Equations Easily**: Converts them into algebraic equations.  
✅ **Understand System Stability**: Helps determine if a system will settle or behave unpredictably.  
✅ **Compare Different Systems**: Standardized format makes analysis easier.  
✅ **Design and Tune Controllers**: Engineers use it to adjust system response.

#### **Example in Real Life**
🚗 **Cruise Control in Cars**  
- **Input:** Desired speed.  
- **System:** Car engine and control mechanism.  
- **Output:** Actual speed.  
- The transfer function helps ensure the car smoothly reaches and maintains the desired speed.

🔋 **Battery Charging System**  
- **Input:** Voltage applied to the battery.  
- **System:** Battery's charging circuit.  
- **Output:** Battery charge level.  
- The transfer function helps predict how fast the battery charges over time.

---

### **2. Relationship Between Transfer Function, Differential Equation, and Time Constant in a First-Order System**
A **first-order system** follows this differential equation:

$$
\frac{dy(t)}{dt} + a y(t) = b x(t)
$$

#### **Step 1: Convert to a Transfer Function**
Applying the **Laplace Transform**:

$$
s Y(s) + a Y(s) = b X(s)
$$

Factor out $ Y(s) $:

$$
Y(s) (s + a) = b X(s)
$$

Solve for the **transfer function**:

$$
H(s) = \frac{Y(s)}{X(s)} = \frac{b}{s + a}
$$

---

#### **Step 2: Identify the Time Constant**
A first-order system has the standard form:

$$
H(s) = \frac{K}{\tau s + 1}
$$

Comparing:

$$
H(s) = \frac{b}{s + a}
$$

we see that:
- **Time Constant** $ \tau = \frac{1}{a} $ (determines how fast the system responds).
- **System Gain** $ K = \frac{b}{a} $ (determines the steady-state output for a given input).

---

#### **Step 3: Interpretation of the Time Constant**
- **$ \tau $ (time constant) represents how quickly the system responds.**
- At **$ t = \tau $**, the system reaches **63% of its final value** for a step input.
- A **smaller $ \tau $ (larger $ a $)** means a **faster response**.
- A **larger $ \tau $ (smaller $ a $)** means a **slower response**.

🔹 **Example:** If $ a = 5 $, then $ \tau = \frac{1}{5} = 0.2 $ sec, meaning the system responds quickly.  
🔹 **Example:** If $ a = 0.5 $, then $ \tau = \frac{1}{0.5} = 2 $ sec, meaning the system responds more slowly.

---

### **3. Determining the Transfer Function from Input-Output Data**
If you have an **unknown first-order system** but have **input-output data**, you can determine its transfer function $ H(s) = \frac{b}{s + a} $ using **impulse or step response data**.

---

#### **Case 1: Using Impulse Response Data**
If you apply an **impulse input** $ x(t) = \delta(t) $, the output follows:

$$
y(t) = b e^{-at}
$$

From the **measured response**:
1. Find the **initial output** at $ t = 0 $ → this gives **$ b $**.
2. Find the **time constant** $ \tau $ from the decay rate → this gives **$ a = 1/\tau $**.

✅ **Example:**  
- If the impulse response is $ y(t) = 10 e^{-4t} $, then:  
  - $ b = 10 $,  
  - $ a = 4 $ (since $ e^{-4t} $ means $ \tau = 1/4 $).  
  - Transfer function:  

  $$
  H(s) = \frac{10}{s + 4}
  $$

---

#### **Case 2: Using Step Response Data**
If you apply a **step input** $ x(t) = u(t) $, the output follows:

$$
y(t) = \frac{b}{a} (1 - e^{-at})
$$

From the **measured response**:
1. Find the **final steady-state value** $ y_{\infty} $ → this gives **$ \frac{b}{a} $**.
2. Find the **time constant** $ \tau $ from how fast the system reaches 63% of $ y_{\infty} $ → this gives **$ a = 1/\tau $**.

✅ **Example:**  
- If the step response is $ y(t) = 4 (1 - e^{-2t}) $, then:  
  - $ \frac{b}{a} = 4 $,  
  - $ a = 2 $ (since $ e^{-2t} $ means $ \tau = 1/2 $).  
  - Solving $ \frac{b}{2} = 4 $, we get $ b = 8 $.  
  - Transfer function:

  $$
  H(s) = \frac{8}{s + 2}
  $$

---

### **4. Summary**
| **Concept** | **Formula / Explanation** |
|-------------|--------------------------|
| **First-Order Differential Equation** | $ \frac{dy(t)}{dt} + a y(t) = b x(t) $ |
| **Transfer Function** | $ H(s) = \frac{b}{s + a} $ |
| **Time Constant** | $ \tau = \frac{1}{a} $ |
| **Impulse Response** | $ y(t) = b e^{-at} $ |
| **Step Response** | $ y(t) = \frac{b}{a} (1 - e^{-at}) $ |
| **Find Transfer Function from Impulse Response** | Measure $ b $ and decay rate $ a $ from data |
| **Find Transfer Function from Step Response** | Measure steady-state $ y_{\infty} = \frac{b}{a} $ and $ \tau = 1/a $ |

Would you like a **graph of these responses** to visualize them? 😊

# Week 3
### **1. Solving a First-Order System with Impulse Input**
We have the system:

$$
\frac{dy(t)}{dt} + a y(t) = b x(t)
$$

where $ x(t) $ is an **impulse input**, i.e., $ x(t) = \delta(t) $.

#### **Step 1: Apply the Laplace Transform**
Taking the Laplace transform of both sides:

$$
s Y(s) + a Y(s) = b X(s)
$$

Since the Laplace transform of an impulse is **1**, i.e., $ X(s) = 1 $, we get:

$$
s Y(s) + a Y(s) = b
$$

#### **Step 2: Solve for $ Y(s) $**
Factor out $ Y(s) $:

$$
Y(s) (s + a) = b
$$

$$
Y(s) = \frac{b}{s + a}
$$

#### **Step 3: Inverse Laplace Transform**
Using the standard formula:

$$
\mathcal{L}^{-1} \left\{ \frac{1}{s + a} \right\} = e^{-at}
$$

we get:

$$
y(t) = b e^{-at}, \quad t \geq 0
$$

This is the **impulse response** of a first-order system.

---

### **2. Two More Numerical Examples (Impulse Input)**

#### **Example 1: $ a = 4, b = 10 $**
Equation:

$$
\frac{dy(t)}{dt} + 4 y(t) = 10 \delta(t)
$$

Solution:

$$
Y(s) = \frac{10}{s + 4}
$$

Taking inverse Laplace:

$$
y(t) = 10 e^{-4t}, \quad t \geq 0
$$

---

#### **Example 2: $ a = 2, b = 7 $**
Equation:

$$
\frac{dy(t)}{dt} + 2 y(t) = 7 \delta(t)
$$

Solution:

$$
Y(s) = \frac{7}{s + 2}
$$

Inverse Laplace:

$$
y(t) = 7 e^{-2t}, \quad t \geq 0
$$

---

### **3. Solving a First-Order System with Step Input**
Now, let's consider the same system but with a **step input**, i.e., $ x(t) = u(t) $.

#### **Step 1: Apply the Laplace Transform**
Taking the Laplace transform:

$$
s Y(s) + a Y(s) = b X(s)
$$

Since the Laplace transform of a step function is $ X(s) = \frac{1}{s} $, we get:

$$
s Y(s) + a Y(s) = \frac{b}{s}
$$

#### **Step 2: Solve for $ Y(s) $**
Factor out $ Y(s) $:

$$
Y(s) (s + a) = \frac{b}{s}
$$

$$
Y(s) = \frac{b}{s(s + a)}
$$

Using **partial fraction decomposition**:

$$
\frac{b}{s(s + a)} = \frac{A}{s} + \frac{B}{s + a}
$$

Solving for $ A $ and $ B $:

$$
A = \frac{b}{a}, \quad B = -\frac{b}{a}
$$

Thus,

$$
Y(s) = \frac{b}{a} \cdot \frac{1}{s} - \frac{b}{a} \cdot \frac{1}{s + a}
$$

Using the inverse Laplace transform:

$$
y(t) = \frac{b}{a} (1 - e^{-at}), \quad t \geq 0
$$

This is the **step response** of a first-order system.

---

### **4. Two More Numerical Examples (Step Input)**

#### **Example 1: $ a = 3, b = 6 $**
Equation:

$$
\frac{dy(t)}{dt} + 3 y(t) = 6 u(t)
$$

Solution:

$$
Y(s) = \frac{6}{s(s + 3)}
$$

Partial fraction:

$$
Y(s) = 2 \left( \frac{1}{s} - \frac{1}{s + 3} \right)
$$

Inverse Laplace:

$$
y(t) = 2 (1 - e^{-3t}), \quad t \geq 0
$$

---

#### **Example 2: $ a = 5, b = 10 $**
Equation:

$$
\frac{dy(t)}{dt} + 5 y(t) = 10 u(t)
$$

Solution:

$$
Y(s) = \frac{10}{s(s + 5)}
$$

Partial fraction:

$$
Y(s) = 2 \left( \frac{1}{s} - \frac{1}{s + 5} \right)
$$

Inverse Laplace:

$$
y(t) = 2 (1 - e^{-5t}), \quad t \geq 0
$$

---

### **5. What is a Transfer Function?**
A **transfer function** describes how a system **transforms** an input into an output in the Laplace domain. It is defined as:

$$
H(s) = \frac{Y(s)}{X(s)}
$$

where:
- $ X(s) $ is the **input**,
- $ Y(s) $ is the **output**.

It helps engineers analyze **system behavior** without solving differential equations directly.

---

### **6. How to Derive the Transfer Function from a First-Order Differential Equation**
Given:

$$
\frac{dy(t)}{dt} + a y(t) = b x(t)
$$

Taking the **Laplace Transform**:

$$
s Y(s) + a Y(s) = b X(s)
$$

Factor out $ Y(s) $:

$$
Y(s) (s + a) = b X(s)
$$

Solve for **transfer function**:

$$
H(s) = \frac{Y(s)}{X(s)} = \frac{b}{s + a}
$$

This is the **transfer function** of a first-order system.

---

### **7. Summary**
| **Scenario** | **Solution** |
|-------------|-------------|
| **Impulse Input $ x(t) = \delta(t) $** | $ y(t) = b e^{-at} $ |
| **Step Input $ x(t) = u(t) $** | $ y(t) = \frac{b}{a} (1 - e^{-at}) $ |
| **Transfer Function $ H(s) $** | $ H(s) = \frac{b}{s + a} $ |

Would you like a **graph** of these responses to visualize the behavior? 😊



# Week 2
### **Laplace Transform as a Lookup Table Approach**
Think of the **Laplace Transform** as a **shortcut tool** that converts complex differential equations into simple algebraic equations. Instead of worrying about the **integration process**, engineers use a **lookup table** to transform functions quickly.

The Laplace Transform takes a function from the **time domain** (which involves derivatives and integrals) and converts it into the **s-domain** (which simplifies solving equations).

---

## **1. Think of It as a Lookup Table**
Instead of manually solving differential equations, we can use a **Laplace Transform table** to convert functions.

| **Time Domain $ f(t) $** | **Laplace Domain $ F(s) $** |
|-----------------|-------------------|
| $ 1 $ (Step input) | $ \frac{1}{s} $ |
| $ e^{-at} $ | $ \frac{1}{s+a} $ |
| $ t $ (Ramp) | $ \frac{1}{s^2} $ |
| $ \sin(\omega t) $ | $ \frac{\omega}{s^2 + \omega^2} $ |
| $ \cos(\omega t) $ | $ \frac{s}{s^2 + \omega^2} $ |
| $ \delta(t) $ (Impulse) | $ 1 $ |

---

## **2. Example 1: Solving a First-Order System**
Let's say we have a **first-order system**:

$$
\frac{dy(t)}{dt} + 3y(t) = 5x(t)
$$

For an **impulse input**: $ x(t) = \delta(t) $

### **Step 1: Apply Laplace Transform**
Using the lookup table:
- $ \mathcal{L} \left\{ \frac{dy}{dt} \right\} = s Y(s) $
- $ \mathcal{L} \{ y(t) \} = Y(s) $
- $ \mathcal{L} \{ \delta(t) \} = 1 $

Applying to the equation:

$$
s Y(s) + 3Y(s) = 5(1)
$$

Factor:

$$
Y(s) (s + 3) = 5
$$

Solve for $ Y(s) $:

$$
Y(s) = \frac{5}{s + 3}
$$

### **Step 2: Use Lookup Table for Inverse Transform**
From the lookup table:

$$
\mathcal{L}^{-1} \left\{ \frac{1}{s + a} \right\} = e^{-at}
$$

So,

$$
y(t) = 5 e^{-3t}, \quad t \geq 0
$$

🔹 **No need for complex integration! Just lookup and apply.**  

---

## **3. Example 2: Step Input Response**
If we use a **step input** $ x(t) = U(t) $, then:

$$
X(s) = \frac{1}{s}
$$

Using the same equation:

$$
s Y(s) + 3Y(s) = 5 \cdot \frac{1}{s}
$$

Solve for $ Y(s) $:

$$
Y(s) = \frac{5}{s(s + 3)}
$$

Using **partial fraction decomposition**:

$$
\frac{5}{s(s+3)} = \frac{A}{s} + \frac{B}{s+3}
$$

Solving, we get:

$$
A = \frac{5}{3}, \quad B = -\frac{5}{3}
$$

Using the **lookup table**:

$$
\mathcal{L}^{-1} \left\{ \frac{1}{s} \right\} = 1, \quad \mathcal{L}^{-1} \left\{ \frac{1}{s + a} \right\} = e^{-at}
$$

$$
y(t) = \frac{5}{3} (1 - e^{-3t})
$$

🔹 **Again, we used the lookup table to solve it easily!**  

---

## **4. Why Use the Laplace Transform?**
✅ Converts **differential equations** into **simple algebraic equations**.  
✅ Uses **lookup tables** to avoid complex calculations.  
✅ Helps analyze **system behavior** efficiently.  
✅ Makes it easier to solve **control and circuit problems**.  

---

## **5. Summary**
- **Laplace Transform is a shortcut** that simplifies system equations.
- **Use a lookup table** instead of solving integrals manually.
- **Example:** Instead of solving $ \frac{dy}{dt} + 3y = 5x $ directly, we convert it into **simple algebraic form**, solve it, and then use a **lookup table** to get the final answer.

Would you like to see a **graphical representation** of these responses? 😊



# Week 1
### What is the Input?

- The **input** is the external stimulus or force applied to the system.
- It is what **drives the system** to produce a response.
- Represented as x(t)x(t)x(t) in the time domain or X(s)X(s)X(s) in the Laplace domain.

### **What is the Output?**

- The **output** is the response of the system due to the input.
- It represents the **measurable effect** caused by the input.
- Represented as y(t) in the time domain or Y(s) in the Laplace domain.

### Examples

| **System Type**                             | **Input x(t)**   | **Output y(t)**  | **Real-World Example**                      |
| ------------------------------------------- | ---------------- | ---------------- | ------------------------------------------- |
| **Electrical Circuit (RC Low-Pass Filter)** | Voltage Vin​     | Voltage Vout​    | A microphone circuit filters noise.         |
| **Mechanical System (Mass-Spring-Damper)**  | Force F(t)       | Position x(t)    | A car suspension system absorbs road bumps. |
| **Thermal System**                          | Heat energy Q(t) | Temperature T(t) | A heater warms up a room.                   |