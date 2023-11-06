# Principal Component Analysis (PCA) apllied to a set of galaxies images

## Whats is PCA?

PCA is a method to analyze and compact the content of a dataset. You can think of it as a generalization of the linear regression: given a set of points with two coordinates (x and y), one can apply linear regression to find the tendency line which represents the main direction of variance; this direction is called the first principal component of the set. When we approximate the position of the points with the height on the tendency line to which they are closest, we are essentialy reducing the dimensionallity of the dataset and transforming a 2-D problem into a 1-D one.

Figure 1 shows the two principal directions of variance, or principal components, of a set of points. The first one is the direction at which the variance is higher.

![figure1](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/ed1c2513-b4b6-4986-80fd-0a8eacf3a9ae)
(Figure 1: The 1st and 2nd principal components of a set of points on a plane)

The same logics can be applied to analyze an arbitrary set of D-dimensional data. With the right math, you can extract from the dataset D principal components (in the form of eigenvectors), each one with their respective proportional variance (their eigenvalues). These vectors are organized in descending order of variance (the one with larger variance being the 1st principal component etc.) so, in order to obtain compact the dataset, it's enough to pick M (M<D) first principal components. Of course, the data compacted in this way will be an approximation: the highest the value of M, the more accurate the approximation will be.

## PCA for images

A black and white image h pixels high and w pixels wide consists of a square matrix with D=h*w elements (Figure 2). Arranged in some proper way, these values can be represented as a vector; a set of images is nothing more than a set of vectors with N components (for colored images, each square pixel would contain 3 numbers refering to the ammount of red, green and blue. The vector, in that case, would be 3D long).

![figure2](https://github.com/rafael-raiser/portfolio_pca/blob/main/images/imagematrix.png)
(Figure 2: Square pixels and grayness values)

Even for a single colored image of, let's say, 100x100 square pixels, one would have to deal with vectors of size N=30,000. Dealing with a dataset containing a large number of these images would require too much computational effort. Here is the point at which PCA comes in hand.

Just as it happens for ordinary data, PCA can be used to "compress" images by finding principal components of the dataset. For a dataset of faces, for example, one would expect the principal components to be circles, noses, mouths etc; the combination of these PC's in differents compositions can reproduce the faces. The quality of the reconstruction depends, of course, on how many principal components are applied.

Putting aside some mathematical formalities, the procedure is simple: one must first rearrange the grayness or RGB values of the images into vectors. From all the vectors of the dataset, the covariance matrix S is calculated; in the following expression, N is the number of images (represented now by vectors), $x_n$ is an individual vector and $\bar{x}$ is the average vector.

$$S= \frac{1}{N} \sum_{n=1}^N (x_n - \bar{x})(x_n - \bar{x})^{T}  $$

Then, one must calculate the eigenvectors and eigenvalues of S. The largest the eigenvalue, the most representative to the whole set is the respective eigenvector. In other words, the vector with largest eigenvalue is the 1st principal component and so on.

In the next step, we compress the dataset by chosing the first M<N principal components. Just as in the case of points on a plane represented by their height on the tendency line, each image can be projected onto this subset of principal components. 

Let ${\boldsymbol{e_1}, \boldsymbol{e_2}, ..., \boldsymbol{e_M}}$ be the first M principal components. The approximation of the image represented by $\boldsymbol{x_n}$ will be

$$\bf{\tilde{x_n}}=\sum_{n=1}^M \bf{x_n}\cdot \bf{e_n} $$

Finally, the images can be recovered by rearranging the elements of the vector.

## The Galaxy Dataset

The present repository is a demonstration of PCA applied to the Galaxy DECals 10 Dataset (source: https://astronn.readthedocs.io/en/latest/galaxy10.html), containing 17736 images with size 256x256 distributed in different galactical morphologies.

We separate the 17736 images into 2 groups: the sample group containing 17736-20 images was used to construct the eigenvectors (the principal components); the test group consisted of 20 randomly selected images and were further used to evaluate the hability of the method to reconstruct these images based solely on the sample group information. Figure below shows the first 6 principal componenents.

![evectors](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/15c764f0-2b4a-4cc7-adbe-3e888955bb43)

The next figure shows a comparison between original images from test groups (upper row) and reconstructed images using 100 principal components.

![original_vs_rec](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/9619d4a7-70af-40b2-a435-216615de1f28)






