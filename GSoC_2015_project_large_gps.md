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
Following last year's successful project on [variational learning for Big Data](http://www.shogun-toolbox.org/page/Events/gsoc2014_ideas#variational_learning), we attempt to bring Shogun's Gaussian Processes (GP) to Big Data land. From a high level perspective, this means that the goal is to implement established methodology on how to scale up GPs to be able to process hundreds of thousands of points. The focus is on regression and classification. As this year's GSoC focusses partly on applications, the project contains a second part where we apply those models to real-world datasets.

### Details
 * Stochastic Variational inference (regression & classification)
 * Distributed GP (possibly touching the Shogun cluster project)
 * Applications

### Waypoints and initial work
 * Step 1
 * Step 2
 * ...

### Optional

**Alternatives to scale up kernel machines. Also useful for other of Shogun's methods**
 * Incomplete Cholesky
 * Random Fourier Features

Other:
 * Deep GP

### Why this is cool
Motivation to get involved here.

### Useful ressources
 * [Gaussian Processes for Big data](http://auai.org/uai2013/prints/papers/244.pdf)
 * [Scalable Variational Gaussian Process Classification](http://staffwww.dcs.sheffield.ac.uk/people/J.Hensman/papers/KLsparse.pdf)
 * [Distributed Gaussian Processes](http://arxiv.org/abs/1502.02843)
 * [Deep Gaussian Processes](http://jmlr.org/proceedings/papers/v31/damianou13a.pdf)