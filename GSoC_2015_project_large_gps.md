# Large-Scale Gaussian Processes

### Mentors
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)
 * [Emtiyaz Khan](http://www.cs.ubc.ca/~emtiyaz/)

### Difficulty & Requirements
Medium
You need know
 * Gaussian Process basics
 * Variational approximation basics
 * Linear Algebra
 * Linear Algebra in C++

### Description
Following last year's successful project on [variational learning for Big Data](http://www.shogun-toolbox.org/page/Events/gsoc2014_ideas#variational_learning), we attempt to bring Shogun's Gaussian Processes (GP) to Big Data land. From a high level perspective, this means that the goal is to implement established methodology on how to scale up GPs to be able to process hundreds of thousands of points. The focus is on regression and classification. We also focuss on applications of GPs to big data where we will consider application to recommendation systems and to learning preferences of people in a social network.

### Details
 * Sparse GP approximations.
 * Stochastic Variational inference (regression & classification)
 * Distributed GP (possibly touching the Shogun cluster project)
 * Applications

### Waypoints and initial work
 * Extend current GP implementation to sparse approximation.
 * Implement variational inference for sparse approximation (Titsias' method).
 * Implement Stochastic variational inference for GP latent variable model.
 * Apply to large scale recommendation systems.
 * Make beautiful demos.

### Optional

**Alternatives to scale up kernel machines. Also useful for other of Shogun's methods**
 * Incomplete Cholesky
 * Random Fourier Features

Other:
 * Deep GP

### Why this is cool
Our primary goal is to scale up GPs to make it possible to apply GPs to many such applications useful for big data. GPs are becoming more and more popular for big data since not only they provide accurate predictions but they also tell us how confident we should be about our prediction (aka uncertainty quantification) and that whether we have selected the right model (aka model selection). These issues are even more relevant in the era of big data since the amount of noise also increases with the amount of data. Recent work extends the use of GPs beyond regression and classification, to a wide range of appliations from numerical optimization to recommendation system and even to deep networks, making GPs a popular choice. The main bottleneck in these applications is scalability and we want to make easy-to-use scalable code which will help the use of GPs for the machine learning community even more. 

### Useful ressources
 * [Gaussian Processes for Big data](http://auai.org/uai2013/prints/papers/244.pdf)
 * [Scalable Variational Gaussian Process Classification](http://staffwww.dcs.sheffield.ac.uk/people/J.Hensman/papers/KLsparse.pdf)
 * [Distributed Gaussian Processes](http://arxiv.org/abs/1502.02843)
 * [Deep Gaussian Processes](http://jmlr.org/proceedings/papers/v31/damianou13a.pdf)