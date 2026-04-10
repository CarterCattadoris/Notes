
# Part 1

## A. Theory

### 1. Mean and Variance
#### (a)$E[X]$
$$E[X] = \int_a^b x \cdot \frac{1}{b-a},dx = \frac{1}{b-a}\cdot\frac{x^2}{2} = \frac{b^2 - a^2}{2(b-a)} = \frac{a+b}{2}$$
$E[X] = (2+8) / 2 = 5$

#### (b)$E[X^2]$ and $Var(X) = E[X^2]-[E[X]]^2$
$$E[X^2] = \int_a^b x^2 \cdot \frac{1}{b-a},dx = \frac{1}{b-a}\cdot\frac{x^3}{3} = \frac{b^3 - a^3}{3(b-a)} = \frac{b^2+ab+a^2}{3}$$
$E[X^2]=\frac{64+16+4}{3}=\frac{84}{3}=28$

$Var(x)=E[X^2]-(E[X])^2=\frac{(b-a)^2}{12}$
$Var(X)=\frac{(8-2)^2}{12}=3$
### 2. Median Quartiles and IQR
$Q_{1} = 2 + 0.25(6) = 3.5$
$Q_{2} = 2 + 0.5(6) = 5$
$Q_{3} = 2 + 0.75(6) = 6.5$
$IQR = 6.5-3.5 = 3$
### 3. Range and Mode

(a) Theoretical range = $8-2=6$
(b) A continuous uniform distribution on [a,b] has no unique mode. Each value is equally likely so all values are modes
## B. Sample Descriptive Statistics

### 1. Order the Data
$2.4, 2.9, 3.1, 3.9, 4.8, 5.7, 6.3, 6.9, 7.4, 7.8$
### 2. Center
$\overline{x} = \frac{2.4 + 2.9 + 3.1 + \dots}{10} = \frac{51.2}{10} = 5.12$
$median = \frac{4.8+5.7}{2}=5.25$
mode: no values repeat
### 3. Spread
$2.4-5.12=-2.72^2= 7.4$
$2.9-5.12=-2.22^2=4.9$
$3.1-5.12=-2.02^2=4.1$
$3.9-5.12=-1.22^2=1.5$
$4.8-5.12=0.32^2=0.1$
$5.7-5.12=0.58^2=0.3$
$6.3-5.12=1.18^2=1.4$
$6.9-5.12=1.78^2=3.2$
$7.4-5.12=2.28^2=5.2$
$7.8-5.12=2.68^2=7.2$
sum = 35.3

sample variance = $\frac{35.3}{9}=3.92$
sample std dev = $\sqrt{ 3.92 }=1.98$
range = 7.8-2.4=5.4
Quartiles:
lower half = (2.4,2.9,3.1,3.9,4.8), Q1 = 3.1
Upper = (5.7,6.3,6.9,7.4,7.8), Q3 = 6.9
IQR = 6.9 - 3.1 = 3.8
### 4. Comparison to theory
Mean is very close, with 5.12 vs 5
median is 5.25 vs 5 which is also pretty close
range is 5.4 vs 6, pretty close but smaller as expected from a smaller sample
IQR is 3.8 vs 3 sample IQR is larger likely due to smaller sample variability 

# Part 2

## A. Theory

### 1. Mean and Variance
(a) $E[X]$
$$E[X] = \int_0^\infty x\lambda e^{-\lambda x}dx = -x e^{-\lambda x} + \int_0^\infty e^{-\lambda x}dx = 0 + \frac{1}{\lambda} = \frac{1}{\lambda}$$
$E[X] = 1 / 0.5 = 2$
(b) $E[X^2]$ and $Var(X)$
$$E[X^2] = \int_0^\infty x^2\lambda e^{-\lambda x}dx  = x^2e^{-\lambda x} + \int_0^\infty 2x e^{-\lambda x}dx = $$$$\left[ \frac{2x}{\lambda} e^{-\lambda x} \right]_{0}^\infty + \int_{0}^\infty \frac{2}{\lambda}e^{-\lambda x}dx = \frac{2}{\lambda}\left[ -\frac{1}{\lambda}e^{-\lambda x} \right]_{0}^\infty =$$ $$\frac{2}{\lambda}\left( 0-\left( -\frac{1}{\lambda} \right) \right)

= \frac{2}{\lambda^2}$$
$E[X²] = 2 / (0.5)² = 2 / 0.25 = 8$

$$Var(X) = E[X^2] - (E[X])^2 = \frac{2}{\lambda^2} - \frac{1}{\lambda^2} = \frac{1}{\lambda^2}$$
$Var(X) = \frac{1}{0.5^2}=4$
### 2. Median quartiles IQR
Using $Q_q = −(1/λ) ln(1 − p(q)) = −2 ln(1 − p(q)):$
$Q_{1}= 0.58$
$Q_{2}= 1.39$
$Q_{3}= 2.77$
$IQR= 2.77-2.58 = 2.2$
### 3. Support and mode
Support: $[0,\infty]$
Mode: 0 since f(x) is decreasing
## B. Sample Desc Stats

### 1. Order data
$0.2, 0.5, 0.8, 1.1, 1.6, 2.0, 2.6, 3.0, 3.5, 5.2$
### 2. Center
mean:$\overline x= (0.2 + 0.5 + 0.8 + 1.1 + 1.6 + 2.0 + 2.6 + 3.0 + 3.5 + 5.2) / 10 = 20.5 / 10$$\overline x = 2.05$
median: 
$(1.6+2)/2=1.8$
Mode:
none repeat, so none
### 3. Spread
(0.2 − 2.05)² = (−1.85)² = 3.4 
(0.5 − 2.05)² = (−1.55)² = 2.4 
(0.8 − 2.05)² = (−1.25)² = 1.6 
(1.1 − 2.05)² = (−0.95)² = 0.9 
(1.6 − 2.05)² = (−0.45)² = 0.2 
(2.0 − 2.05)² = (−0.05)² = 0.0 
(2.6 − 2.05)² = (0.55)² = 0.3 
(3.0 − 2.05)² = (0.95)² = 0.9 
(3.5 − 2.05)² = (1.45)² = 2.1 
(5.2 − 2.05)² = (3.15)² = 9.9
sum = 21.7

variance: 21.7250 / 9 = 2.41
std dev: √2.4139 = 1.55
range = 5.2-0.2 = 5

Quartiles:
lower half:
0.2, 0.5, 0.8, 1.1, 1.6, median = 0.80

Upper half: 2.0, 2.6, 3.0, 3.5, 5.2 median = 3.00

IQR = 3.00 − 0.80 = 2.20

### 4. Compare to theory
mean 2.05 vs 2 is very close
median of 1.8 vs 1.39 is kinda close with sample being higher
range 5 vs infinity, theoretical is always going to have an infinite range
IQR 2.2 vs 2.2 is identical

The sample mean and IQR closely match theoretical values. The sample median is higher than the theoretical median, which is expected sampling variability with only n = 10. The sample range is finite while the theoretical range is infinite, since a small sample is unlikely to capture extreme values.

The distribution is right-skewed, confirmed by the sample mean (2.05) exceeding the median (1.80). Large values like 5.2 pull the mean upward. With n = 10, all differences from theory are attributable to normal sampling variability.

