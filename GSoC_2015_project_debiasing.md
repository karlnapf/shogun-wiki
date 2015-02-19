# Debiasing as a fast alternative to batch computations in Gaussian process Regression

### Mentors
 * [Dino Sejdinovic](http://www.csml.ucl.ac.uk/people/sejdinovic)ub: [sejdino] (gith(https://github.com/sejdino))
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
Medium (optional: advanced)
You need
 * C++ coding
 * Basic statistics and linear algebra
 * Some knowledge of Gaussian Processes helpful but not essential
 * Optinal: experience with parallel computing

### Description
Bayesian inference is a cornerstone of modern data analysis but its feasibility is being challenged in the era of Big Data as in many Bayesian inference algorithms data needs to be processed in batches. Many subsampling low computational cost approaches have been proposed but they often introduce a bias to the inference procedure that is hard to quantify. Recent work on debiasing device used in this context has shown that it is possible to obtain unbiased Bayesian inference by choosing the sizes of the subsamples at random - which reduces the average computational cost to sublinear even though no bias is being introduced. This project would implement the debiasing device in Shogun, so that it can be apply together with the already existing Bayesian inference functionalities. In particular, the focus of this project would be to implement the debiasing device for Gaussian process regression.


### Details
TODO

### Waypoints and initial work
TODO

### Optional
Work on the cluster backend of Shogun, which related to [this project](GSoC_2015_cluster_shogun). They could be combined and debiasing is the application of the cluster project.

### Why this is cool
Scaling up of kernel methods and gaussian processes is a hot research topic. In this project, you will learn techniques to extend flexible and expressive machine learning algorithms like gaussian processes to the situations with millions of data points.

### Useful ressources
H. Strathmann, D. Sejdinovic and M. Girolami, Unbiased Bayes for Big Data: Paths of Partial Posteriors. 
arXiv preprint 1501.03326, 2015. http://arxiv.org/abs/1501.03326