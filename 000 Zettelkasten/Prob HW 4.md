## Part 1

### Part 1A
Picture attached to submission
### Part 1B

a. Mean = 70, Median = 70, Mode = 70.

b. Variance = σ² = 8² = 64

c. std dev = $σ = 8$

d. 
$~68\%$ of data in $μ ± σ$, between 62 and 78
$~95\%$ of data in $μ ± 2σ$, between 54 and 86
$~99.7\%$ of data in $μ ± 3σ$, between 46 and 94
### Part 1C

1. A bin width of 5 would be reasonable. With a range of roughly 46 to 94 ($\pm 3\sigma$), this gives about 10 bins which is enough to show the bell shape without being too noisy for 100 observations.

2. Also on paper with submission

3. The histogram should be symmetric and bell shaped, centered around 70, with most values between 54 and 86

4. With 100 observations from a normal population, the histogram approximates the smooth curve. As sample size increases, the histogram bars align more closely with the theoretical pdf

## Part 2

1. np.random.seed() sets a fixed starting point for the random number generator so that the results are reproducible

2. numpy using np.random.normal() generates random samples from a normal distribution.

3. numpy and scipy using np.mean(), np.median(), np.var(), np.std() for mean/median/variance/std dev, and scipy.stats.mode() for the mode.
4. The mean (70.88) and median (70.97) are very close, which is expected for a symmetric normal distribution. The mode was 50.11, but that is not meaningful. Since no values repeat scipy just returns the smallest value.
5. The generated histogram is approximately bell-shaped and centered near 70, similar to the sketch from Part 1. It has some irregularity in bar heights due to random sampling
6. As sample size increases, the histogram becomes smoother and more closely matches the theoretical normal curve. 
7. The results are close to the theoretical values because the data was generated from that exact distribution

## Extension

When the sample size increases from 100 to 1,000, the histogram becomes noticeably smoother and more closely mirrors the theoretical normal curve. The bars are more uniform in their progression and the bell shape is cleaner. This happens because a larger sample better represents the population, reducing the effect of random variation in any single bin.