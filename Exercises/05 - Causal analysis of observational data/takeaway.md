# Causal Analysis of Observational Data
<img src="./data/pairplot.png" width="60%" alt="test"/>

```python 
import seaborn as sns
sns.pairplot(df)
```

## Pairwise matching
```python
import statsmodels.formula.api as smf

def get_similarity(propensity_score1, propensity_score2):
    '''Calculate similarity for instances with given propensity scores'''
    return 1-np.abs(propensity_score1-propensity_score2)

for col in ['col1', 'col2', 'col3']: # the interesting columns
    df[col] = (df[col]-df[col].mean())/df[col].std() # standardize the columns that are not categorical

mod = smf.logit(formula='treatment ~ col1 + col2 + col3', data=df)
res = mod.fit()

df['propensity_score'] = res.predict(df)

# Separate the treatment and control groups
treatment_df = df[df['treat'] == 1]
control_df = df[df['treat'] == 0]

# Create an empty undirected graph
G = nx.Graph()

# Loop through all the pairs of instances
for control_id, control_row in control_df.iterrows():
    for treatment_id, treatment_row in treatment_df.iterrows():

        # Calculate the similarity 
        similarity = get_similarity(control_row['Propensity_score'],
                                    treatment_row['Propensity_score'])

        # Add an edge between the two instances weighted by the similarity between them
        G.add_weighted_edges_from([(control_id, treatment_id, similarity)])

# Generate and return the maximum weight matching on the generated graph
matching = nx.max_weight_matching(G)

matched = [i[0] for i in list(matching)] + [i[1] for i in list(matching)]
balanced_df = df.iloc[matched]
```
Note that if the balanced df is not balanced enough on some feature, we can repeat the matching part by only adding the weighted edges if both control and treatment instances have the same value on that feature.