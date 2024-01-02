# Data wrangling in practice
## Do I have **missing data**?
### Detecting missing data
```python
# Will print basic information about the dataframe, like the number of non-null values or the type of each column
df.info()
```
### If yes, how to deal with it?
```python
# Remove rows with missing values
df.dropna()
```
```python
# Fill missing values with a specific value
df.fillna(0)
```
Value can be:
- Mean
- Median
- Some arbitrary value
- Value estimated by another model
- Value got from another dataset

It is also possible to drop the column if it has too many missing values and is not important.

## Do I have **corrupted data**? (e.g. measurement errors, processing bugs, ...)
### Detecting corrupted data
```python
# Will print out some basic statistics for each column
df.describe()
```

```python
# For each column, plot a histogram of the values
df.hist(bins=100)
```
I need to detect **outliers**, which are values that are far from the rest of the data.

### If yes, how to deal with it?
```python
# Remove rows with corrupted values
df = df[df['column'] < 100]
```
Can use other techniques, cf missing values.

## Transforming data into the right format
### Do I have **categorical data**?
```python
# Will print out the unique values for each column
df['column'].unique()
```
Use it to detect categorical data.

#### If yes, how to deal with it?
```python
# One-hot encoding
pd.get_dummies(df['column'])
```
Useful for regression

### Example of the timestamp format
```python
import datetime
pd.to_datetime(df['column']) # Can choose the format using it as a parameter
```