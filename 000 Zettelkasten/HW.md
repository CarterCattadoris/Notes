# Homework 3: Uniform & Exponential Distributions

---

## Part I — Uniform Distribution (35 pts)

**Given:** X ~ Uniform(a, b), a = 2, b = 8, f(x) = 1/(b − a) = 1/6 for 2 ≤ x ≤ 8.

---

### A. Theory (15 pts)

#### 1. Mean and Variance (8 pts)

**(a) E[X]**

General formula:

$$E[X] = \int_a^b x \cdot \frac{1}{b-a},dx = \frac{1}{b-a}\cdot\frac{x^2}{2}\Big|_a^b = \frac{b^2 - a^2}{2(b-a)} = \frac{a+b}{2}$$

Plugging in:

> **E[X] = (2 + 8) / 2 = 5.00**

**(b) E[X²] and Var(X)**

$$E[X^2] = \int_a^b x^2 \cdot \frac{1}{b-a},dx = \frac{1}{b-a}\cdot\frac{x^3}{3}\Big|_a^b = \frac{b^3 - a^3}{3(b-a)} = \frac{b^2+ab+a^2}{3}$$

Plugging in:

E[X²] = (64 + 16 + 4) / 3 = 84 / 3 = 28.00

General variance formula:

$$Var(X) = E[X^2] - (E[X])^2 = \frac{(b-a)^2}{12}$$

Plugging in:

> **Var(X) = 28 − 25 = 3.00** (equivalently (8−2)² / 12 = 36/12 = 3.00)

---

#### 2. Median, Quartiles, and IQR (5 pts)

Using Q_q = a + p(q)(b − a):

|Quartile|p(q)|Calculation|Value|
|---|---|---|---|
|Q1|0.25|2 + 0.25(6)|**3.50**|
|Q2 (median)|0.50|2 + 0.50(6)|**5.00**|
|Q3|0.75|2 + 0.75(6)|**6.50**|

> **IQR = Q3 − Q1 = 6.50 − 3.50 = 3.00**

---

#### 3. Range and Mode (2 pts)

**(a)** Theoretical range = b − a = 8 − 2 = **6.00**

**(b)** A continuous uniform distribution on [a, b] has **no unique mode**. Every value in the interval is equally likely (f(x) is constant), so all values are modes — the distribution is "flat."

---

### B. Sample Descriptive Statistics (20 pts)

**Data:** 6.3, 2.9, 7.8, 4.8, 3.1, 6.9, 5.7, 7.4, 2.4, 3.9

#### 1. Ordered Data (2 pts)

> **2.4, 2.9, 3.1, 3.9, 4.8, 5.7, 6.3, 6.9, 7.4, 7.8**

---

#### 2. Center (6 pts)

**Sample mean:**

x̄ = (2.4 + 2.9 + 3.1 + 3.9 + 4.8 + 5.7 + 6.3 + 6.9 + 7.4 + 7.8) / 10 = 51.2 / 10

> **x̄ = 5.12**

**Sample median (Q2):**

n = 10 (even). Median = average of 5th and 6th ordered values:

> **Q2 = (4.8 + 5.7) / 2 = 5.25**

**Sample mode:**

> No values repeat, so **there is no sample mode**.

---

#### 3. Spread (8 pts)

**Deviations from x̄ = 5.12:**

|xᵢ|xᵢ − x̄|(xᵢ − x̄)²|
|---|---|---|
|2.4|−2.72|7.3984|
|2.9|−2.22|4.9284|
|3.1|−2.02|4.0804|
|3.9|−1.22|1.4884|
|4.8|−0.32|0.1024|
|5.7|0.58|0.3364|
|6.3|1.18|1.3924|
|6.9|1.78|3.1684|
|7.4|2.28|5.1984|
|7.8|2.68|7.1824|
||**Sum**|**35.2760**|

**Sample variance:**

> **s² = 35.2760 / (10 − 1) = 35.2760 / 9 = 3.92** (rounded)

**Sample standard deviation:**

> **s = √3.9196 ≈ 1.98**

**Range:**

> **Range = 7.8 − 2.4 = 5.40**

**Quartiles (Tukey median-of-halves):**

Lower half (positions 1–5): 2.4, 2.9, 3.1, 3.9, 4.8 → Q1 = median = **3.10**

Upper half (positions 6–10): 5.7, 6.3, 6.9, 7.4, 7.8 → Q3 = median = **6.90**

> **IQR = 6.90 − 3.10 = 3.80**

---

#### 4. Comparison to Theory (4 pts)

|Measure|Sample|Theoretical|Comment|
|---|---|---|---|
|Mean|5.12|5.00|Very close; small sampling error|
|Median|5.25|5.00|Reasonably close|
|Range|5.40|6.00|Sample range is smaller — expected, since a finite sample rarely captures the full theoretical range|
|IQR|3.80|3.00|Sample IQR is somewhat larger, reflecting sampling variability with only n = 10|

Overall, the sample statistics approximate the theoretical values well. Small deviations are expected due to the small sample size (n = 10).

---

---

## Part II — Exponential Distribution (65 pts)

**Given:** X ~ Exponential(λ), λ = 0.5, f(x) = 0.5e^(−0.5x) for x ≥ 0.

---

### A. Theory (20 pts)

#### 1. Mean and Variance (8 pts)

**(a) E[X]**

General formula (integration by parts with u = x, dv = λe^(−λx) dx):

$$E[X] = \int_0^\infty x,\lambda e^{-\lambda x},dx = \left[-x e^{-\lambda x}\right]_0^\infty + \int_0^\infty e^{-\lambda x},dx = 0 + \frac{1}{\lambda} = \frac{1}{\lambda}$$

Plugging in:

> **E[X] = 1 / 0.5 = 2.00**

**(b) E[X²] and Var(X)**

General formula (integration by parts twice):

$$E[X^2] = \int_0^\infty x^2,\lambda e^{-\lambda x},dx = \frac{2}{\lambda^2}$$

E[X²] = 2 / (0.5)² = 2 / 0.25 = 8.00

$$Var(X) = E[X^2] - (E[X])^2 = \frac{2}{\lambda^2} - \frac{1}{\lambda^2} = \frac{1}{\lambda^2}$$

> **Var(X) = 8 − 4 = 4.00** (equivalently 1/(0.5)² = 4.00)

---

#### 2. Median, Quartiles, and IQR (8 pts)

Using Q_q = −(1/λ) ln(1 − p(q)) = −2 ln(1 − p(q)):

|Quartile|p(q)|1 − p(q)|ln(1 − p(q))|Q_q = −2 · ln(1 − p(q))|
|---|---|---|---|---|
|Q1|0.25|0.75|−0.2877|**0.58**|
|Q2 (median)|0.50|0.50|−0.6931|**1.39**|
|Q3|0.75|0.25|−1.3863|**2.77**|

> **IQR = Q3 − Q1 = 2.77 − 0.58 = 2.20** (rounded; exact: 2ln(3) ≈ 2.1972)

---

#### 3. Support and Mode (4 pts)

**(a)** The support of the exponential distribution is **[0, ∞)** — i.e., x ≥ 0.

**(b)** The **mode is 0**. Since f(x) = λe^(−λx) is a strictly decreasing function for x ≥ 0, it attains its maximum value of λ = 0.5 at x = 0.

---

### B. Sample Descriptive Statistics (45 pts)

**Data:** 3.0, 0.5, 1.6, 5.2, 0.8, 2.6, 1.1, 3.5, 0.2, 2.0

#### 1. Ordered Data (3 pts)

> **0.2, 0.5, 0.8, 1.1, 1.6, 2.0, 2.6, 3.0, 3.5, 5.2**

---

#### 2. Center (10 pts)

**Sample mean:**

x̄ = (0.2 + 0.5 + 0.8 + 1.1 + 1.6 + 2.0 + 2.6 + 3.0 + 3.5 + 5.2) / 10 = 20.5 / 10

> **x̄ = 2.05**

**Sample median (Q2):**

n = 10 (even). Median = average of 5th and 6th ordered values:

> **Q2 = (1.6 + 2.0) / 2 = 1.80**

**Sample mode:**

> No values repeat, so **there is no sample mode**.

---

#### 3. Spread (20 pts)

**Deviations from x̄ = 2.05:**

|xᵢ|xᵢ − x̄|(xᵢ − x̄)²|
|---|---|---|
|0.2|−1.85|3.4225|
|0.5|−1.55|2.4025|
|0.8|−1.25|1.5625|
|1.1|−0.95|0.9025|
|1.6|−0.45|0.2025|
|2.0|−0.05|0.0025|
|2.6|0.55|0.3025|
|3.0|0.95|0.9025|
|3.5|1.45|2.1025|
|5.2|3.15|9.9225|
||**Sum**|**21.7250**|

**Sample variance:**

> **s² = 21.7250 / 9 = 2.41** (rounded)

**Sample standard deviation:**

> **s = √2.4139 ≈ 1.55**

**Range:**

> **Range = 5.2 − 0.2 = 5.00**

**Quartiles (Tukey median-of-halves):**

Lower half (positions 1–5): 0.2, 0.5, 0.8, 1.1, 1.6 → Q1 = median = **0.80**

Upper half (positions 6–10): 2.0, 2.6, 3.0, 3.5, 5.2 → Q3 = median = **3.00**

> **IQR = 3.00 − 0.80 = 2.20**

---

#### 4. Comparison to Theory (12 pts)

|Measure|Sample|Theoretical|Comment|
|---|---|---|---|
|Mean|2.05|2.00|Very close|
|Median|1.80|1.39|Sample median is higher than theoretical|
|Range|5.00|∞|A finite sample always yields a finite range; the theoretical distribution extends to infinity|
|IQR|2.20|2.20|Nearly identical|

**Discussion:**

The sample mean (2.05) closely matches the theoretical mean (2.00), suggesting the sample is representative of the population center. The sample median (1.80) is noticeably higher than the theoretical median (1.39); with only n = 10 observations, sampling variability can produce such differences, particularly for a skewed distribution.

The exponential distribution is **right-skewed** — the long right tail means occasional large values (like 5.2 in this sample) pull the mean above the median. This is confirmed by our sample: x̄ = 2.05 > Q2 = 1.80. The right skew also explains why the theoretical range is infinite while the sample range is finite — extremely large values are possible but rare.

The sample IQR (2.20) matches the theoretical IQR (2.20) remarkably well, which is partly coincidental for n = 10 but suggests the middle 50% of the sample captures the spread of the distribution accurately. The sample variance (2.41) is below the theoretical variance (4.00), likely because no extreme outliers appeared in this particular sample to inflate the squared deviations.

Overall, the sample statistics reasonably approximate the theoretical values, with deviations attributable to **sampling variability** inherent in small samples (n = 10).