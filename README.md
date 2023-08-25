# Principal Component Analysis (PCA) apllied to a set of galaxies images

## Whats is PCA?

PCA is a method to represent and store huge amounts of data using what is called dimensionality redution. You can think of it as a generalization of the linear regression: you have points in a 2 dimensional plane, each one with a x and y coordinate; when we apply linear regression to these points, the tendency line (or linear fit) represents the direction at which the variance is bigger. Thus, this direction is called the first principal component of the set.
With the linear regression, a 2d problem is approximated to a 1d problem. Of course, one may think about the second principal component of the set: it is a direction perpendicular to the PC-1. The image below show the two PC's for the case of a linear regression.
![image](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/ed1c2513-b4b6-4986-80fd-0a8eacf3a9ae)

Essentially, this is dimensionality reduction. We just transformed a 2D problem into a 1D one.

The same logics can be applied to analyze an arbitrary set of D-dimensional data. With the right math, you can extract from your data D unitary vectors (actually eigenvectors) with their respective proportional variance (their eigenvalues). The eigenvectors with the highest eigenvalues are more suitable to represent the whole dataset. 

## PCA for images

In the case of images of size m x n, we can interpret an area of m x n px², rearranged in a proper way, as a vector with m x n elements. For black and white images, each element of the vector contains a number representing the grayness of that pixel; for colored images, each element would contain 3 numbers refering to the ammount of red, green and blue in that pixel (the vector, in this case, would be 3m x n long).

Even for a single colored image of, let's say, 100x100 px², one would have to deal with vectors with 30000 elements. Dealing with a dataset containing a large number of these images would require too much computational effort. Here is the point at which PCA comes in hand.

Just as it happens for ordinary data, PCA can be used to "compress" images by finding principal components of the dataset. For a dataset of faces, for example, one would expect the principal components to be circles, noses, mouths etc. The combination of these PC's in differents compositions can reproduce the faces. The quality of the reconstruction depends, of course, on how many principal components are applied.

Putting aside some mathematical formalities, the procedure is simple: one must construct the vectors for each image, each element containing the grayness of one pixel. From all the vectors of the dataset, the covariance matrix S is calculated. In the following expression, N is the number of images (now vectors), $x_n$ is an individual vector and $\bar{x}$ is the average between all the vectors.

$$S= \frac{1}{N} \sum_{n=1}^N (x_n - \bar{x})(x_n - \bar{x})^{T}  $$

Then, one must calculate the eigenvectors and eigenvalues of S. The largest the eigenvalue, the most representative to the whole set is the respective eigenvector. In other words, the eigenvector with largest eigenvalue is the principal component of the whole dataset and so on.

The next step is to chose the number a eigenvectors (in decreasing order along the eigenvalues) smaller than the original dimension of the images. Then, we project the original images into this new basis of eigenvectors, generating compressed images.

## The Galaxy Dataset

The present repository is a demonstration of PCA applied to the Galaxy DECals 10 Dataset (source: https://astronn.readthedocs.io/en/latest/galaxy10.html), containing 17736 images with size 256x256 distributed in different galactical morphologies.

We separate the 17736 images into 2 groups: the sample group containing 17736-20 images was used to construct the eigenvectors (the principal components); the test group consisted of 20 randomly selected images and were further used to evaluate the hability of the method to reconstruct these images based solely on the sample group information. Figure below shows the first 6 principal componenents.

![evectors](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/15c764f0-2b4a-4cc7-adbe-3e888955bb43)

The next figure shows a comparison between original images from test groups (upper row) and reconstructed images using 100 principal components.

![original_vs_rec](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/9619d4a7-70af-40b2-a435-216615de1f28)






