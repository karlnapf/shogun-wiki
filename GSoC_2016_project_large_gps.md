# Large-Scale Gaussian Processes, tensorflow, and autodiff

*Note:* This project description is likely to be updated soon, in favour of a re-factoring of Shogun's GPs using [Google tensorflow](https://www.tensorflow.org/) and its autodiff capabilities
### Mentors
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)
 * [Wu](Wu%20Lin) (github: [yorkerlin](https://github.com/yorkerlin), IRC: yorkerlin)
 * [Emtiyaz Khan](http://www.cs.ubc.ca/~emtiyaz/)
 * [Vincent Adam](https://sites.google.com/site/myvincentadam/)

### Difficulty & Requirements
Medium to Difficult
You need know
 * Gaussian Process basics
 * Variational approximation basics
 * Linear Algebra
 * Linear Algebra in C++

### Description
Following last year's successful project on [variational learning for Big Data](http://www.shogun-toolbox.org/page/Events/gsoc2014_ideas#variational_learning), we attempt to bring Shogun's Gaussian Processes (GP) to Big Data land. From a high level perspective, this means that the goal is to implement established methodology on how to scale up GPs to be able to process hundreds of thousands of points. The focus is on regression and classification. We also focuss on applications of GPs to big data where we will consider application to recommendation systems and to learning preferences of people in a social network.

### Details
 * Variational inference for (full) GP using Tensorflow
 * Variational inference for sparse GP using Tensorflow
 * Stochastic variational inference for sparse GP using Tensorflow
 * Applications

### Waypoints and initial work
 * Exact inference for (full) GP regression using Tensorflow (entrance task) (ExactInferenceMethod)
 * Variational inference for (full) GP binary classification using Tensorflow ([KLCovarianceInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CKLCovarianceInferenceMethod.html), [KLCholeskyInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CKLCholeskyInferenceMethod.html), and [KLApproxDiagonalInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CKLApproxDiagonalInferenceMethod.html))
 * Variational inference for sparse GP (regression & classification) using Tensorflow  ([FITCInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CFITCInferenceMethod.html) and [SparseVGInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CSparseVGInferenceMethod.html))
 * Make beautiful demos and benchmarks  
 * Stochastic variational inference for sparse GP using Tensorflow (optional)

### Refactoring existing framework
#### Variational Gaussian inference (Suggested Roadmap)
 * base class for computing gradient of Evidence Lower BOund (ELBO) wrt variaitonal variables 
 * base class for computing gradient of ELBO wrt hyper-parameters in likelihoods, mean functions, and co-variance/kernel functions
 * base class for using external or build-in minimizers ([LBFGSMinimizer](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1LBFGSMinimizer.html) and [NLOPTMinimizer](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1NLOPTMinimizer.html))
 * (for full GP) classes for computing gradient wrt variaitonal variables and hyper-parameters using Tensorflow and existing hand-implemented codes 
 * (for full GP) classes for computing gradient wrt hyper-parameters using Tensorflow and existing hand-implemented codes (tricky part)
 * classes for using build-in LBFGS minimizer 
 * base class for MC samplers
 * classes for using existing MC samplers 
 * (for sparse GP) classes for computing gradient wrt variaitonal variables and hyper-parameters using Tensorflow and existing hand-implemented codes 
 * (for sparse GP) classes for computing gradient wrt hyper-parameters using Tensorflow and existing hand-implemented codes (tricky part)
 * classes for HMC samplers from Stan (optional)
 * base class for model selection (eg, Bayesian OPT) (optional)

#### MCMC inference (optional)

### Optional

**Alternatives to scale up kernel machines. Also useful for other of Shogun's methods**
 * Incomplete (banded) Cholesky inference for GP binary classification using Tensorflow
 * Random Fourier Features

Other:
 * Deep GP

### Why this is cool
Our primary goal is to scale up GPs to make it possible to apply GPs to many such applications useful for big data. GPs are becoming more and more popular for big data since not only they provide accurate predictions but they also tell us how confident we should be about our prediction (aka uncertainty quantification) and that whether we have selected the right model (aka model selection). These issues are even more relevant in the era of big data since the amount of noise also increases with the amount of data. Recent work extends the use of GPs beyond regression and classification, to a wide range of appliations from numerical optimization to recommendation system and even to deep networks, making GPs a popular choice. The main bottleneck in these applications is scalability and we want to make easy-to-use scalable code which will help the use of GPs for the machine learning community even more. 

### Useful ressources
 * [GPflow using Tensorflow](https://github.com/GPflow/GPflow)
 * [Shogun's variational Gaussian inference for full GP](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CKLInferenceMethod.html)
 * [Shogun's variational Gaussian inference for sparse GP](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CSparseInferenceBase.html)
 * [Approximations for Binary Gaussian Process Classification](http://www.jmlr.org/papers/volume9/nickisch08a/nickisch08a.pdf)
 * [Concave Gaussian Variational Approximations for Inference in Large-Scale Bayesian Linear Models](http://www.jmlr.org/proceedings/papers/v15/challis11a/challis11a.pdf)
 * [Variational Learning of Inducing Variables in Sparse Gaussian Processes](http://www.jmlr.org/proceedings/papers/v5/titsias09a/titsias09a.pdf)
 * [Gaussian Processes for Big data](http://auai.org/uai2013/prints/papers/244.pdf)
 * [Scalable Variational Gaussian Process Classification](http://staffwww.dcs.sheffield.ac.uk/people/J.Hensman/papers/KLsparse.pdf)
 * [Distributed Gaussian Processes](http://arxiv.org/abs/1502.02843)
 * [Deep Gaussian Processes](http://jmlr.org/proceedings/papers/v31/damianou13a.pdf)