# Principal Component Analysis (PCA) apllied to a set of galaxies images

## Whats is PCA?

PCA is a method to represent and store huge amounts of data using what is called dimensionality reduction. You can think of it as a generalization of the linear regression: you have points in a a 2 dimensional points, each one with a x and y coordinate; when we apply linear regression to these points, a line representing the direction with more variance is drawn. Finally, you'll have a tendency line that represnt all the points sparsed in the 2D space into a single dimensional: if you specify an argument to the line, the line will give you the best approximation of the y-value of the point closest to the line.

![image](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/ed1c2513-b4b6-4986-80fd-0a8eacf3a9ae)

Essentially, this is dimensionality reduction. We just transformed a 2D problem into a 1D one.

The same logics can be applied to analyze an arbitrary set of D-dimensional data. With the right math, you can extract from your data D unitary vectors (actually eigenvectors) with their respective proportional variance (their eigenvalues). The vectors with highest eigenvalues are more suitable to represent the whole dataset. If you are starting from a 100-dimensional problem, for example, you could choose to work with the 10 eigenvectors with largest eigenvalues and your representation would probably


