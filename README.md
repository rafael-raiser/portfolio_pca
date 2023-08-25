# Principal Component Analysis (PCA) apllied to a set of galaxies images

## Whats is PCA?

PCA is a method to represent and store huge amounts of data using what is called dimensionality reduction. You can think of it as a generalization of the linear regression: you have points in a a 2 dimensional points, each one with a x and y coordinate; when we apply linear regression to these points, a line representing the direction with more variance is drawn. Finally, you'll have a tendency line that represnt all the points sparsed in the 2D space into a single dimensional: if you specify an argument to the line, the line will give you the best approximation of the y-value of the point closest to the line.

![image](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/ed1c2513-b4b6-4986-80fd-0a8eacf3a9ae)

Essentially, this is dimensionality reduction. We just transformed a 2D problem into a 1D one.

The same logics can be applied to analyze an arbitrary set of D-dimensional data. With the right math, you can extract from your data D unitary vectors (actually eigenvectors) with their respective proportional variance (their eigenvalues). The eigenvectors with the highest eigenvalues are more suitable to represent the whole dataset. 

## PCA for images

In the case of images of size m x n, We can interpret an area of $m\cdot n$ px², rearranged in a proper way, as a vector with dimension $m\cdot n$. For black and white images, each element of the vector contains a number representing the grayness of that pixel; for colored images, each element would contain 3 numbers refering to the ammount of red, green and blue in that pixel (the vector, in this case, would be $3m\cdot n$ long).

Even for a single colored image of, let's say, 100x100 px², one would have to deal with vectors with 30000 elements. Treating a dataset containing a large number of these images would require too much computational effort. Here is the point PCA come in action.

Despite some mathematical formalities, the procedure is simple: one must construct the vectors for each image and, from them, calculate the covariance matrix S. In the following expression, N is the number of images (now vectors), $x_n$ is an individual vector and $\bar{x}$ is the average between all the vectors.

$$S= \frac{1}{N} \sum_{n=1}^N (x_n - \bar{x})(x_n - \bar{x})^{T}  $$

Then, one must calcuulate the eigenvectors and eigenvalues of S. The largest the eigenvalue, the most representative to the whole set is the respective eigenvector. In other words, the eigenvector with largest eigenvalue is the principal component of the whole dataset ans so on.

Figure below shows the 6 principal components (or eigenvectors with higer eigenvalues) to the galaxy-10 Dataset.



If each image has D px² (thus their vectorial representation is D-dimensional), we chose M<D eigenvectors with decreasing eigenvalues and, then, project the original vectorized-images into this set of eigenvectors.







