# Large-Scale Gaussian Processes

Polish, update, and extend Shogun's framework for Gaussian Processes, with a focus on large-scale problems and sparse variational inference.

### Mentors
 * [Wu](https://www.linkedin.com/in/wu-lin-b1a587b7) (github: [yorkerlin](https://github.com/yorkerlin), IRC: yorkerlin)
 * [Emtiyaz Khan](http://www.cs.ubc.ca/~emtiyaz/)

### Difficulty & Requirements
**Medium to Difficult**


You need know:
 * [Gaussian Process basics](http://www.gaussianprocess.org/gpml/) (You should understand the [GP Notebook](http://www.shogun-toolbox.org/static/notebook/current/gaussian_processes.html))
 * Variational approximation basics (You should understand at least the full GP part of the [Notebook for Variational Inference](http://www.shogun-toolbox.org/static/notebook/current/variational_classifier.html))
 * Linear Algebra (math & in C++)

### Description
Following our previous successful project on [variational learning for Big Data](http://www.shogun-toolbox.org/page/Events/gsoc2014_ideas#variational_learning), we attempt to bring Shogun's Gaussian Processes (GP) to Big Data land. From a high level perspective, this means that the goal is to implement established methodology on how to scale up GPs to be able to process hundreds of thousands of points.


### Details
We want to focus on the following sub-tasks:

 * Variational inference for (full) GP
 * Variational inference for sparse GP
 * Stochastic variational inference for sparse GP
 * Applications
 

The project will start from the existing code base, which already contains a huge amount of work. We aim to fill the gaps in the above methods:

 * Implement all standard methods that are not yet in the framework
 * Benchmark existing methods against competing implementations (such as GPStuff, GPflow, GPML, etc)
 * Improve efficiency if necessary. Make explicit use of multi-core computation.
 * Unify gradient computations within Shogun.

### Waypoints and initial work
 * do benchmarks about all existing inference methods for (full) GP and sparse GP under the existing framework (entrance task) ([KLCovarianceInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CKLCovarianceInferenceMethod.html), [KLCholeskyInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CKLCholeskyInferenceMethod.html), [KLApproxDiagonalInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CKLApproxDiagonalInferenceMethod.html), [FITCInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CFITCInferenceMethod.html), and [SparseVGInferenceMethod](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CSparseVGInferenceMethod.html))

* Understanding the inference procedure and refactoring existing framework with the help from mentors   
* Make beautiful demos and benchmarks under the new framework
* Stochastic variational inference for sparse GP (optional)

### Refactoring existing framework
#### Variational Gaussian inference (Suggested Roadmap)
 * base class for computing gradient of Evidence Lower BOund (ELBO) wrt variaitonal variables 
 * base class for computing gradient of ELBO wrt hyper-parameters in likelihoods, mean functions, and co-variance/kernel functions
 * (base) class for using external or build-in minimizers ([LBFGSMinimizer](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1LBFGSMinimizer.html) and [NLOPTMinimizer](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1NLOPTMinimizer.html))
 * (for full GP) classes for computing gradient wrt variaitonal variables using existing hand-implemented codes and (possible) AutoDiff (eg Tensorflow or Stan)  
 * (for full GP) classes for computing gradient wrt hyper-parameters using existing hand-implemented codes and (possible) AutoDiff (eg Tensorflow or Stan)  
 * Benchmarks and notebooks for demos 
 * base class for MC samplers
 * classes for using existing MC samplers 
 * (for sparse GP) classes for computing gradient wrt variaitonal variables using existing hand-implemented codes and (possible) AutoDiff (eg Tensorflow or Stan)  
 * (for sparse GP) classes for computing gradient wrt hyper-parameters using existing hand-implemented codes and (possible) AutoDiff (eg Tensorflow or Stan)  
 * classes for HMC samplers from Stan (optional)
 * base class for model selection (eg, Bayesian OPT) (optional)



### Optional
 * MCMC inference 
 * Deep GP

### Why this is cool
Our primary goal is to scale up GPs to use them in "big data" applications. GPs are becoming more and more popular for big data because they provide both accurate predictions, tell us how confident we should be about our prediction (aka uncertainty quantification) and also whether we have selected the right model (aka model selection). With big data comes big noise, so these issues are becoming ever more relevant. Recently GPs are a popular choice beyond regression and classification for a wide range of appliations from numerical optimization to recommendation system and even to deep networks. The main bottleneck in these applications is scalability. Therefore, we want you to write easy-to-use, scalable code which will help the machine learning community to use GPs. 

### Useful ressources
 * [GPflow using Tensorflow](https://github.com/GPflow/GPflow)
 * [Shogun's variational Gaussian inference for full GP](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CKLInferenceMethod.html)
 * [Shogun's variational Gaussian inference for sparse GP](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CSparseInferenceBase.html)
 * [Notebook about Variational inference for GP](http://www.shogun-toolbox.org/static/notebook/current/variational_classifier.html)
 * [Approximations for Binary Gaussian Process Classification](http://www.jmlr.org/papers/volume9/nickisch08a/nickisch08a.pdf)
 * [Concave Gaussian Variational Approximations for Inference in Large-Scale Bayesian Linear Models](http://www.jmlr.org/proceedings/papers/v15/challis11a/challis11a.pdf)
 * [Variational Learning of Inducing Variables in Sparse Gaussian Processes](http://www.jmlr.org/proceedings/papers/v5/titsias09a/titsias09a.pdf)
 * [Gaussian Processes for Big data](http://auai.org/uai2013/prints/papers/244.pdf)
 * [Scalable Variational Gaussian Process Classification](http://staffwww.dcs.sheffield.ac.uk/people/J.Hensman/papers/KLsparse.pdf)
 * [Distributed Gaussian Processes](http://arxiv.org/abs/1502.02843)
 * [Deep Gaussian Processes](http://jmlr.org/proceedings/papers/v31/damianou13a.pdf)

Get back to the [main projects page](Google%20Summer%20of%20Code%202016%20Projects).