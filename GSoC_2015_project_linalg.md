# `linalg`: Unifying Shogun's linear algebra

### Mentors
 * [Soumyajit](Soumyajit%20De%20[Rahul]) (github: [lambday](https://github.com/lambday), IRC: lambday)
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Description
This venture was started as a part of one GSoC project last year. This year we aim at finalizing and polishing Shogun's [internal library for linear algebra](README_linalg). The goal is explore modern C++ linear algebra libraries to exploit their CPU/GPU powered linear algebra operations for Shogun and in turn offer Shogun algorithm coders a simple, uniform *backend independent* interface that they can use for their linear algebra calls using those libraries. Rather than writing implementation against a particular backend (that we currently do using Eigen3, Lapack, ViennaCL and Shogun's native implementation), algorithms should be written against `linalg`. This allows to
- change backends at compile time, and 
- in particular makes our algorithms independent of the current trend in linear algebra software. 
- It also will allow to put many operations on GPUs *without* having to change the implementation (to an extend).

The goal is not to write a complete linear algebra library on our own, but at least have some of the *most-used linalg calls* in our internal lib, such as
 * factorizing matrices
 * linear solvers
 * eigen solvers
 * applying the same operation to every element of a large matrix
 * dot products
 * various utilities (get/set diagonal, fill, get/set columns, supporting block based operations etc)

### Why this is cool
This project will massively increase both performance and sustainability of Shogun. We will get parallelism of many algorithms for free and at the same time open up ways for using different, better, backends (such as GPUs) in the future. It will furthermore allow to write algorithms without knowledge of backend internals. Nobody wants to deal with Lapack API directly ;)

### Details
Presently, a handful of operations are there in `linalg`, spread over two different modules, `Core` and `Redux`.
 * The first target is to **populate `linalg` with most-used linear algebra operations** for both dense and sparse matrices. This includes figuring out a nice way to handle 
    * element-wise operations
    * col/row-wise operations 
    * in-place operations, using blocking techniques (useful for large matrices)
    * block-based operations 
*while* using different third party/native backend. We'll be using Eigen3, ViennaCL/OpenCL and (optionally) LAPACK. We *don't* want native implementation for *each* of these operations, just the ones we've already got. So in most cases native implementation would involve moving existing code from other parts of Shogun to `linalg`. 
 * Most important part of this job is matrix factorization/linear solvers/eigen solvers. This requires some investigation on the benefits/disadvantages of storing the factorization results for successive linear/eigen solver calls. We want at least 
    * Cholesky
    * QR
    * LU
    * Eigen
    * SVD
(see issue [2526](https://github.com/shogun-toolbox/shogun/issues/2526), [2527](https://github.com/shogun-toolbox/shogun/issues/2527)).
 * We'd like to have iterative solvers such as 
    * Conjugate Gradient (CG)
    * Stabilized Bi-conjugate gradient (BiCG-stab)
 * A large part will be to **read through Shogun's core algorithms and make them use the new interface**. This is where you show off all the cool stuffs you did in GSoC :) Once we have that, the mop-up job is to remove the existing piece of linear algebra operations from `SGMatrix` and `SGVector` to make them lightweight.

### Difficulty & Requirements
**Medium**. You need knowledge on
 * Advanced C/C++ (knowledge about C++11 is a plus). A reasonable level of comfort with [templates](http://en.cppreference.com/w/cpp/language/templates), [template specialization](http://en.cppreference.com/w/cpp/language/template_specialization), [partial specialization](http://en.cppreference.com/w/cpp/language/partial_specialization), [traits](http://accu.org/index.php/journals/442), [SFINAE](http://en.cppreference.com/w/cpp/language/sfinae), ability to read/write non-trivial template code
 * Numerical Linear algebra
 * Eigen3, LAPACK (src level familiarity is a plus)
 * GPU programming (OpenCL/ViennaCL)
 * Shogun algorithms
 * OpenMP [Optional]

### Waypoints and initial work
 * Keep an eye on the [Github issues page](https://github.com/shogun-toolbox/shogun/issues) for related issues.

### Useful resources
 * [`linalg` README](https://github.com/shogun-toolbox/shogun/wiki/README_linalg)
 * [cppreference](http://en.cppreference.com/w/)
 * [`template` and `typename` in C++](http://eigen.tuxfamily.org/dox/TopicTemplateKeyword.html)
 * [Eigen3 doc](http://eigen.tuxfamily.org/dox/index.html)
 * [A Gentle Introduction to OpenCL](http://www.drdobbs.com/parallel/a-gentle-introduction-to-opencl/231002854)
 * [ViennaCL doc](http://viennacl.sourceforge.net/doc/)
 * [Numerical Linear Algebra by Trefethen and Bau](https://javierolivares.files.wordpress.com/2009/04/numerical-linear-algebra-trefethenbau.pdf)