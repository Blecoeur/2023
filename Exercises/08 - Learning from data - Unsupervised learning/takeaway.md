# Unsupervised Learning

## K-means Clustering
```python
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters=2, random_state=0).fit(X)
# Plotting the data using the labels as the colors
plt.scatter(X[:,0], X[:,1], c=kmeans.labels_, alpha=0.6)
for c in kmeans.cluster_centers_:
    plt.scatter(c[0], c[1], c='red', marker='+') # Plotting the centroids
```

## Dimensionality Reduction
### t-SNE
```python
from sklearn.manifold import TSNE
X_reduced_tsne = TSNE(n_components=2, init='random', learning_rate='auto', random_state=0).fit_transform(X)
```	
### PCA
```python
from sklearn.decomposition import PCA
X_reduced_pca = PCA(n_components=2).fit(X).transform(X)
```

## Density based: DBSCAN
```python
from sklearn.cluster import DBSCAN
labels = DBSCAN(eps=0.5).fit_predict(X) # Need to tune eps

plt.scatter(X[:,0], X[:,1], c=labels, alpha=0.6)
```

## Tips and tricks
### Scaling
```python
from sklearn.preprocessing import StandardScaler
X_scaled = StandardScaler().fit(X).transform(X)
```

### Choosing the number of clusters
- Elbow method: plot the inertia (sum of squared distances of samples to their closest cluster center) as a function of the number of clusters
- Silhouette score: measure of how similar a point is to its own cluster (cohesion) compared to other clusters (separation)