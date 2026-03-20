202603201145
Status: #idea
Tags:[[Probability and Statistics (CIS321)]]

## Part 1

1. Population: the entire set of whatever you are interested in. Sample: a subset of that population. We often sample because measuring the entire population can be expensive and time intensive, especially for a broadly scoped problem. Sampling provides a reasonable amount of data to make inferences about the entire population
2. The population for this problem is the number of minutes every single passenger going through the transportation hub waits for a taxi
3. Descriptions
	1. mean: average, sum all values then divide by number of values. Gives you the "center" of the data but skews towards the extremes
	2. median: middle value when all values are sorted in number order. Resistant to outliers unlike the mean is so it can give you a better sense of the actual midpoint
	3. mode: value that appears most often in a set of data. Another measure of central tendency
	4. range: max - min. Very sensitive to outliers. tells you total spread of the data
	5. variance: measures how far (on average) data is from the mean. A higher value means values are on average farther from the mean (positive or negative)
	6. Standard Deviation: square root of variance to keep the units the same as the original data. Easier to interpret because of that
	7. Minimum: smallest value in the dataset
	8. Maximum: largest value in the dataset
	9. IQR: difference between the 75th percentile and the 25th percentile. Finds the spread of the middle part of the data making it a better measure of variability since it ignores outliers.

## Part 2

1. $E(x) = (0)(0.03)+1(0.06)+2(0.09)+3(0.1)+4(0.08)+5(0.07)+6(0.05)+7(0.04)+8(0.03)+10(0.07)+12(0.06)$$+15(0.05)+18(0.04)+22(0.05)+27(0.04)+33(0.03)+40(0.04)+50(0.04)+65(0.03)$
=13.64 minutes
2. $\sigma ^2 = (0 - 13.64)²(0.030) + (1 - 13.64)²(0.060) + (2 - 13.64)²(0.090) + (3 - 13.64)²(0.100) + \dots$
= 240.68 minutes
3. $\sigma = \sqrt{240.68} =$ 15.51 minutes
4. $P(X ≤ 0) = 0.030$
$P(X ≤ 1) = 0.030 + 0.060 = 0.090$
$P(X ≤ 2) = 0.090 + 0.090 = 0.180$
$P(X ≤ 3) = 0.180 + 0.100 = 0.280$
$P(X ≤ 4) = 0.280 + 0.080 = 0.360$
$P(X ≤ 5) = 0.360 + 0.070 = 0.430$
$P(X ≤ 6) = 0.430 + 0.050 = 0.480$
$P(X ≤ 7) = 0.480 + 0.040 = 0.520$ 
Median = 7 mins
5. mode=3 minutes
6. $P(X ≤ 1) = 0.030 + 0.060 = 0.090$
$P(X ≤ 2) = 0.090 + 0.090 = 0.180$
$P(X ≤ 3) = 0.180 + 0.100 = 0.280$
Q1 = 3

$P(X ≤ 7) = 0.480 + 0.040 = 0.520$ 
$P(X ≤ 8) = 0.550$
$P(X ≤ 10) = 0.620$
$P(X ≤ 12) = 0.680$
$P(X ≤ 15) = 0.730$
$P(X ≤ 18) = 0.770$
Q3 = 18

IQR = Q3 - Q1 = 18 - 3 = 15 minutes

## Part 3
### Sample A
3, 3, 4, 5, 6, 20, 25, 30
1. mean = $\frac{3+3+4+5+6+20+25+30}{8}=12$
2. variance = $\left( \frac{1}{7} \right)[(3-12)^2+(3-12)^2+(4-12)^2+(5-12)^2+(6-12)^2+(20-12)^2+(25-12)^2+(30-12)^2]$= 124
3. std dev = $\sqrt{ 124 } = 11.14$
4. median is between 5 and 6, so 5.5
5. mode = 3, appears twice
6. Range = 30 - 3 = 27
7. $Q_{1} = \frac{3+4}{2} = 3.5$, $Q_{3} = \frac{20+25}{2}=22.5$, IQR = 22.5 - 2.5 = 19
### Sample B
18, 22, 27, 33, 40, 50, 65, 65
1. mean = $\frac{18+22+27+33+40+50+65+65}{8} = 40$
2. variance = $\left( \frac{1}{7} \right)[(18-40)^2+(22-40)^2+(27-40)^2+(33-40)^2+(40-40)^2+(50-40)^2+(65-40)^2+(65-40)^2]$
=339.43
3. std dev = $\sqrt{ 339.43 } = 18.42$
4. median is between 33 and 40, so 36.5
5. mode = 65, appears twice
6. range = 65 - 18 = 47
7. Q1 = $\frac{22+27}{2}=24.5$, Q3 = $\frac{50+65}{2}=57.5$, IQR = 57.5-24.5 = 33

## Part 4
1. Their respective statistics are different because they contain different subsets of the population. Sample A is mostly shorter wait times with a few longer ones, producing a lower median and mean while Sample B has mostly longer wait times producing higher values for both. 
2. Sample A better represents the population. Its mean and median are a lot closer to the populations compared to sample B. It also shares the same mode of 3, and has a slightly closer standard deviation. Overall, all of its descriptive statistics are a lot closer so it better represents the population