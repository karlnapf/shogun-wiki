# Large-scale Approximate Kernel Methods

Focussing on one of Shogun's main strengths, this project is to polish and unify existing methods, and add a few new players.

### Mentors
 * [Sören](https://github.com/shogun-toolbox/shogun/wiki/AUTHORS) (IRC: sonney2k)
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
Easy to difficult, depends on what we aim for. You need knowledge of
 * The kernel trick (any of SVM, KRR, K-PCA, etc)
 * The relation between the dual and the primal formulation when using kernels
 * desirable: knowledge of approximate kernel methods (random features, etc)
 * Basic ML (what are the interfaces)
 * Basic Shogun (again, what are the interfaces)
 * Basic Linear Algebra
 * Optional: Knowledge of Shogun's ```linalg``` interface [link](https://github.com/shogun-toolbox/shogun/wiki/README_linalg)

### Description
Approximate kernel methods are of increasingly popularity. The provide means to scale up traditional kernel-based algorithms. The idea is to perform computations in an explicit approximate feature space, which has a simpler structure and an explicit (data independent) basis.  Mathematically, this means that the underlying optimization problem is solved in its primal representation, rather than the dual one. As Shogun has one of its main focus on such large-scale kernel methods, this project is to polish, unify, and extend Shogun's kernel method implementations. The project is divided into two parts. Improving existing algorithms, and adding some state-of-the-art methods.


### Details
Goals include

 * Part I: Unify and speed-up existing implementations
  * Re-factor the interface of CKernelMachine to support both primal and dual formulations.
  * Re-work the framework for approximate features to work well with the primal formulation above.
  * Put the (existing) random Fourier features code into that framework, and polish it.
  * Work on the numerical code: Benchmark / speed up / parallelise / Use ```linalg```
  * Improve documentation, write an IPython notebook that covers all implemented methods.
  * Algorithms to consider: KRR, K-PCA, SVM.


 * Part II: Adding new methods
  * Implement random binning features
  * Low rank approximations: Incomplete Cholesky factorisation of kernel matrices, and its embedding into the primal interface above
  * Sparse approximations: Nystrom -- random sub-sampling of entries of the kernel matrix. Leverage scores for choosing sampling weights.
  * more to come ...

### Why this is cool
Kernel methods are quite sexy, but don't scale up well. This project collects tools to solve this problem. It allows to learn about kernel basics, how to scale them up mathematically / from an implementation point of view. In addition, there are some interesting software-design questions to answer. For sure allows you to impress girls in the pub next door ;)

### Entrance tasks
 * Benchmark and improve KRR [issue](https://github.com/shogun-toolbox/shogun/issues/2991)
 * Start an ipython notebook about random fourier features
 * Implement incomplete Cholesky algorithm (see below for Python reference)
 * Draft a more detailed schedule. 
  * A good point to start would be to collect information about all implemented approximate kernel methods in Shogun.
  * Another good point is to look at [scikit](http://scikit-learn.org/stable/auto_examples/plot_kernel_approximation.html)'s implementation of the random fourier features and Nystrom methods. How can we learn from their design.

### References
Papers:
 * [Original paper](http://www.eecs.berkeley.edu/~brecht/papers/07.rah.rec.nips.pdf) on random features (random Fourier & random binning) 
 * [Nystrom approximation with fast leverage scores](http://www.stat.berkeley.edu/~mmahoney/pubs/elalaoui-nips15.pdf)
 * [Slides on incomplete Cholesky](http://www.di.ens.fr/~fbach/ICML_2005_CSI_3.pdf)

Code:
 * [incomplete Cholesky](https://github.com/karlnapf/kernel_exp_family/blob/master/kernel_exp_family/kernels/incomplete_cholesky.py) and [unit tests](https://github.com/karlnapf/kernel_exp_family/blob/master/tests/kernels/test_incomplete_cholesky.py) in Python
 * [scikit on approximate kernel methods](http://scikit-learn.org/stable/auto_examples/plot_kernel_approximation.html)
 * [Shogun class for random features](http://shogun-toolbox.org/doc/en/3.0.0/classshogun_1_1CRandomFourierDotFeatures.html)