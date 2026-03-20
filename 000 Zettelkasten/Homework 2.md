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
