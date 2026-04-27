## Part A
### A1

**Distribution:** Since σ is unknown and we're estimating µ with x̄, the sampling distribution of x̄ follows a t-distribution with df = n − 1 = 11.

$$SE(\bar{x}) = \frac{s}{\sqrt{n}}= 1.910 \text{ ms}$$

**Meaning:** If we repeated this sampling procedure many times, the sample mean reaction time would typically vary from sample to sample by about 1.91 ms.
### A2

**Margin of error:** $ME = t* · SE = (2.201)(1.910) = 4.204 ms$

**Interval:** $251.833 ± 4.204 → (247.63 ms, 256.04 ms)$

**Interpretation:** We are 95% confident that the true population mean reaction time lies between 247.63 ms and 256.04 ms.

### A3

**(B):** The 95% refers to the long-run success rate of the procedure, if we repeated this sampling and interval construction many times, about 95% of the resulting intervals would contain $µ$. For any one specific interval (like ours), µ is either in it or not.

### A4

**Independence:** Reasonable assuming the 12 reaction times were collected from independent trials/subjects
**Nearly normal sampling distribution:** The 12 values are tightly clustered (range 241–263) with no extreme observations, so this is reasonable.
## Part B

### B1
$$H_0: \mu = 250 \quad \text{vs.} \quad H_a: \mu < 250$$
left tailed
### B2
**Distribution under H₀:** t with df = n − 1 = 11.

$$t = \frac{\bar{x} - \mu_0}{SE} = \frac{251.833 - 250}{1.910} = 0.960$$
### B3

**Left-tailed:** $p = P(T₁₁ ≤ 0.960)$. Using the t-table at $df = 11, t = 0.960$ falls between 0.876 (cum. prob 0.80) and 1.088 (cum. prob 0.85), so $p ≈ 0.82$.

_Meaning of the p-value:_ If the population mean really were 250 ms, there's about an 82% chance of observing a sample mean as small as (or smaller than) ours just from random sampling variability
### B4
$p ≈ 0.82 ≫ 0.05$ → fail to reject H₀.

**Conclusion:** The data do not provide evidence that the population mean reaction time is less than 250 ms
### B5. Connection to the CI

1. Yes, $µ₀ = 250$ lies inside the 95% CI $(247.63, 256.04).$
2. Therefore a two-sided test at $α = 0.05$ would also fail to reject µ₀ = 250
## Part C
### C0

Positive. Higher study hours track with higher exam scores across the table.

### C1
$\overline{x} = 5.4$
$s_{x} = 2.2$
$\overline{y} = 75.9$
$s_{y}=9.8$
$s_{xy} = 21.6$
$r = 0.9943$

### C2
1. $r ≈ 0.99$ indicates a very strong, positive, linear association between hours studied and exam score in this sample.
2. Correlation does not prove causation. A lurking variable could drive both. This is observational data with no random assignment to study-hour levels, so we cannot conclude that adding study hours _causes_ higher scores.

### C3

**Hypotheses:** $H₀: ρ = 0 vs. Hₐ: ρ ≠ 0$

**Distribution under $H_0$:** t with $df = n − 2 = 8.$

**Test statistic:**

$$t = r\sqrt{\frac{n-2}{1-r^2}} = 0.9943\sqrt{\frac{8}{1-0.9887}} = 26.44$$

**p-value:** $p = 2·P(T_{8} ≥ 26.44)$. From the t-table at df = 8, the largest tabulated value is 5.041. Our t is over five times larger, so p < 0.001 (Excel =T.DIST.2T(26.44, 8) ≈ 5 × 10⁻⁹).

**Meaning of the p-value:** If hours studied and exam score were truly uncorrelated in the population, the chance of observing a sample correlation this extreme is effectively zero
### C4

$p < 0.001 ≪ 0.05 → reject H₀.$

**Conclusion in context:** There is overwhelming evidence that the population correlation $ρ$ between hours studied and exam score is not zero. Since r > 0, the relationship is positive.
## Quick reflection

1. The CI ↔ two-sided test duality (B5) once you see that $µ₀$ is inside 95% CI you see also see that p > 0.05. 
2. If a 95% CI and a two-sided test at $α = 0.05$ always agree, why do we learn both?