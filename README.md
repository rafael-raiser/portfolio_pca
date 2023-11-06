# Principal Component Analysis (PCA) apllied to a set of galaxies images

## Whats is PCA?

PCA is a method to analyze and compact the content of a dataset. You can think of it as a generalization of the linear regression: given a set of points with two coordinates (x and y), one can apply linear regression to find the tendency line which represents the main direction of variance; this direction is called the first principal component of the set. When we approximate the position of the points with the height on the tendency line to which they are closest, we are essentialy reducing the dimensionallity of the dataset and transforming a 2-D problem into a 1-D one.

Figure 1 shows the two principal directions of variance, or principal components, of a set of points. The first one is the direction at which the variance is higher.

![figure1](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/ed1c2513-b4b6-4986-80fd-0a8eacf3a9ae)

(Figure 1: The 1st and 2nd principal components of a set of points on a plane)

The same logics can be applied to analyze an arbitrary set of D-dimensional data. With the right math, you can extract from the dataset D principal components (in the form of eigenvectors), each one with their respective proportional variance (their eigenvalues). These vectors are organized in descending order of variance (the one with larger variance being the 1st principal component etc.) so, in order to obtain compact the dataset, it's enough to pick M (M<D) first principal components. Of course, the data compacted in this way will be an approximation: the highest the value of M, the more accurate the approximation will be.

## Mathematical formulation of PCA

We now discuss how to represent a set ($\{\boldsymbol{x_1},\boldsymbol{x_2},...,\boldsymbol{x_N}\}$) containing N D-dimensional vectors (though here as column vectors) using only M (M<D) dimensions. For a better explanation on the procedure we recommend the Christopher Bishop's book "Pattern Recognition and Machine Learning".

Appart from some details regarding the standardization of the dataset, the first step is to calculate the mean vector and the deviation from the mean:

$$ \boldsymbol{y_n} = \boldsymbol{x_n - \bar{x}} $$

where $\boldsymbol{\bar{x}}=\sum_n^N \boldsymbol{x_n}/N$.

It can be shown that the principal components (i.e. the main directions of variance) arise from evaluating the eigenvectors of the covariance matrix S (with dimension DxD). The derivation of this comes from the minimization of the error of the approximations.

$$ S= \frac{1}{N} \sum_{n=1}^N \boldsymbol{y_n} \boldsymbol{y_n}^{T}  $$

The (unitary) eigenvectors of S are now calculated and sorted into descending order according to the the respective eigenvalues (the eigenvalues can be shown to be proportional to the variance). This gives rise to an orthogonal basis of the D-dimensional space: $\{\boldsymbol{e_1}, \boldsymbol{e_2}, ..., \boldsymbol{e_D}\}$. 

The last step is to obtain an approximation ($\boldsymbol{{{x'}_n}}$) of the original dataset using only the first M principal components; this is done by projection:

$$ \boldsymbol{{{x'}_n}} = \boldsymbol{\bar{x}} + \sum_{i=1}^D (\boldsymbol{y_n}^T \boldsymbol{e_i})\boldsymbol{e_i} $$

## PCA for images

A black and white image h pixels high and w pixels wide consists of a square matrix with D=h*w elements, each one representing a grayness value (Figure 2). Arranged in some proper way, these values can be represented by a vector; a set of images is nothing more than a set of vectors with D components (for colored images, each square pixel contains 3 numbers refering to the ammount of red, green and blue. The vector, in that case, would be 3D long).

![figure2](https://github.com/rafael-raiser/portfolio_pca/blob/main/images/imagematrix.png)

(Figure 2: Square pixels and grayness values)

Even for a single colored image of, let's say, 100x100 square pixels, the size of the vectors would be huge: D=30,000. Dealing with a dataset containing a large number of these images would require too much computational effort. Here is the point at which PCA comes in hand.

Just as it happens for ordinary data, PCA can be used to "compress" images by finding principal components of the dataset. For a dataset of faces, for example, one would expect the principal components to be circles, noses, eyes etc; the combination of these components in differents compositions can reproduce the original images. The quality of the reconstruction depends, of course, on how many principal components are chosen.


## The Galaxy Dataset

The present repository is a demonstration of PCA applied to the Galaxy DECals 10 Dataset (source: https://astronn.readthedocs.io/en/latest/galaxy10.html), containing 17736 images with size 256x256 distributed in different galactical morphologies.

We separate the 17736 images into 2 groups: the sample group containing 17,706 images was used to construct the eigenvectors (the principal components); the test group consisting of 20 randomly selected images was further used to evaluate the hability of the method to reconstruct these images based solely on the sample group information. Figure 3 shows the first 6 principal componenents and Figure 4 compares some of the reconstructed images with the original ones.

![evectors](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/15c764f0-2b4a-4cc7-adbe-3e888955bb43)

(Figure 3: The first 6 principal components of the Galaxy Dataset)


![original_vs_rec](https://github.com/rafael-raiser/portfolio_pca/assets/142827112/9619d4a7-70af-40b2-a435-216615de1f28)

(Figure 4: Original images (above) and reconstructed ones (below) using 100 principal components)

Whilst it's not a rule, the visualization of the principal components can provide some intuition on the nature of the dataset. While PC's 3 and 4 have, as expected for galaxies, circular symmetry, it's harder to find a similar explanation to PC's 1, 2, 5 and 6.

## Description of the scripts

'openG10.ipynb': opens the '.h5' file available on the Galaxy DECals 10 website and stores the data into Numpy files.

'load_images.ipynb': loads the Numpy files and randomly selects 17,706 images for the sample set and 20 for the test set.

'PCA.ipynb': performs the analysis and returns a visualization of the principal components and some of the reconstructed images.





