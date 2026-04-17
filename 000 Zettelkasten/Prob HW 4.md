## Part 1

### Part 1A
Picture attached to submission
### Part 1B

**a.** Mean = 70, Median = 70, Mode = 70.

**b.** Variance = σ² = 8² = 64

**c.** std dev = $σ = 8$

**d.** 
$~68\%$ of data in $μ ± σ$, between 62 and 78
$~95\%$ of data in $μ ± 2σ$, between 54 and 86
$~99.7\%$ of data in $μ ± 3σ$, between 46 and 94
### Part 1C

**1.** A bin width of 5 would be reasonable. With a range of roughly 46 to 94 ($\pm 3\sigma$), this gives about 10 bins which is enough to show the bell shape without being too noisy for 100 observations.

**2.** Also on paper with submission

**3.** The histogram should be symmetric and bell shaped, centered around 70, with most values between 54 and 86

**4.** With 100 observations from a normal population, the histogram approximates the smooth curve. As sample size increases, the histogram bars align more closely with the theoretical pdf

## Part 2

### Before Running the Code

**1.** `np.random.seed()` sets a fixed starting point for the random number generator so that the results are reproducible

**2.** Library: **NumPy** (`numpy`). Function: `np.random.normal()` generates random samples from a normal distribution.

**3.** Library: **NumPy** and **SciPy** (`scipy.stats`). Functions: `np.mean()`, `np.median()`, `np.var()`, `np.std()` for mean/median/variance/standard deviation, and `scipy.stats.mode()` for the mode.

---

### After Running the Code

**3.** Yes, the mean, median, and mode should be close in value. The normal distribution is symmetric, so all three measures of center converge to μ = 70 for large samples. Small differences are due to sampling variability.

**4.** The generated histogram should closely resemble the hand-drawn sketch from Part 1 — approximately bell-shaped, centered at 70, symmetric, with spread governed by σ = 8.

**5.** As sample size increases, the histogram becomes smoother and more closely matches the theoretical normal curve. Random variation between bins decreases and the bell shape becomes more defined.

**6.** The sample statistics are close to the theoretical values because the data was drawn from the known distribution N(70, 64). With a reasonably large sample, the law of large numbers ensures sample statistics approximate population parameters. Small differences are normal sampling variability.

---

## Optional Extension

When the sample size increases from 100 to 1,000, the histogram becomes noticeably smoother and more closely mirrors the theoretical normal curve. The bars are more uniform in their progression and the bell shape is cleaner. This happens because a larger sample better represents the population, reducing the effect of random variation in any single bin.