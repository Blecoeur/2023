# Describing Data
## Statistical tests
### Kolmogorov-Smirnov test
```python
from statsmodels.stats import diagnostic

stat, p = diagnostic.kstest_normal(df['IncomePerCap'].values, dist = 'norm') # Can choose other distributions
```
stat is the Kolmogorov-Smirnov statistic. p is the p-value.
Null hypothesis: the data is XXX distributed.

### Pearson correlation
To check whether two variables are linearly correlated. 
```python	
from scipy import stats
corr, p = stats.pearsonr(x, y)
```
corr is between -1 and 1. p is the p-value.
Null hypothesis: the two variables are uncorrelated.

### Spearman correlation
To check whether two variables are monotonically correlated.
```python
from scipy import stats
corr, p = stats.spearmanr(x, y)
```
corr is between -1 and 1. p is the p-value.
Null hypothesis: the two variables are uncorrelated.

### T-test
To check whether two groups have the same mean.
```python
from scipy import stats
t, p = stats.ttest_ind(x, y) #Assuming that both 
```
t is the t-statistic (difference between the arithmetic means). p is the p-value.
Null hypothesis: the means of the two groups are the same.