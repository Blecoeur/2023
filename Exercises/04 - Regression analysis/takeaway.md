# Regression analysis

```python
import statsmodels.formula.api as smf
# Define the model
model = smf.ols(formula=formula, data=df)
# Fit the model
results = model.fit()
print(results.summary())
```
Summary contains informations like:
- *R-squared/Adj. R-squared*: how much of the variance in the data is explained by the model
- *Intercept*: the value of the intercept (mean when all variables are 0)
- *Coef*: the value of the coefficient (slope) for each predictor
- *P>|t|*: p-value of the coefficient (probability that the coefficient is 0)
- *Cond. No.*: condition number (diagnostic for multicollinearity) --> should be small

The formula is writen using patsy formula syntax:
- `~` separates the left-hand side of the model from the right-hand side
- `+` adds new columns to the design matrix
- `:` adds a new column to the design matrix with the product of the other two columns
- `*` is a shorthand: `a * b` expands to `a + b + a:b`
- Intercepts are added by default
- `C(a)` denotes categorical variable `a`

When predictors are of different scales, it is important to standardize the predictors before fitting the model. `(X-X.mean())/X.std()`