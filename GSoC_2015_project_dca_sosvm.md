# A dual coordinate ascent solver for SO-SVM

### Mentors
 * Vojtech Franc (http://cmp.felk.cvut.cz/~xfrancv/)
 * [Viktor Gal](http://maeth.com/) (github: [vigsterkr](https://github.com/vigsterkr), IRC: wiking)

### Difficulty & Requirements
Medium.

You need to be able to
 * very good in C/C++
 * basics of optimization


### Description

The structured output Support Vector Machines (SO-SVM) is a supervised
method for learning parameters of a linear classifier with possibly
huge number of classes. Learning is translated into a convex
optimization program size of which scales with the number of classes
making the problem intractable by off-the-shelf solvers. A dual
coordinate ascent (DCA) based methods, well known e.g. from two-class
SVMs, have been recently proposed for solving the SO-SVM [1][2]. The
DCA algorithms combine advantages of approximate online solvers and
precise cutting plane methods used so far. In particular, the DCA
algorithms process training example in a on-line fashion by a simple
update rule and they provide a certificate of optimality at the same
time. The goal of this project will be to implement several variants of
the DCA algorithms published in [1][2], namel, the Block-coordinate 
Frank-Wolfe and FASOLE. 

[1] S.Lacoste-Julien, M.Jaggi, M.Schmidt, and P.Pletscher. Block-coordinate
    Frank-Wolfe optimization for structural SVMs. ICML, 2013.
[2] V.Franc: FASOLE. Fast Algorithm for Structured Output LEarning. ECML, 2014.


### Waypoints and initial work
 * Reading the papars [1][2] to get familiar with BCFW and FASOLE.
 * Getting familiar with Shogun's framework for SO learning.
 * Implementing BCFW.
 * Implementing FASOLE.
 * Benchmarking, comparison with methods already in Shogun.
 * Writing documentation.

### Why this is cool

The project is about implementing the current state-of-the-art solvers
for SO learning which has many exciting application in domains like
computer vision, bio-informatics, text processing and so on.


### Useful ressources
 * S.Lacoste-Julien, M.Jaggi, M.Schmidt, and P.Pletscher. Block-coordinate
   Frank-Wolfe optimization for structural SVMs. ICML, 2013.
   http://jmlr.org/proceedings/papers/v28/lacoste-julien13-supp.pdf
 * V.Franc: FASOLE. Fast Algorithm for Structured Output LEarning. ECML, 2014.
   http://cmp.felk.cvut.cz/ftp/articles/franc/Franc-Fasole-ECML2014.pdf
