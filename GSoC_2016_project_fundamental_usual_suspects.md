# Fundamental Machine Learning Algorithms

Continuing where we stopped [last year](https://www.google-melange.com/gsoc/project/details/google/gsoc2014/mazumdarparijat/5738600293466112).

## The usual suspects

### Mentors
 * Heiko (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)
 * [Vincent Adam](https://sites.google.com/site/myvincentadam/)

### Difficulty & Requirements
Easy to Medium -- depends on you. You need
 * ML Algorithms in C++
 * Re-factoring existing code / design patterns
 * Knowledge of very basic ML algorithms
 * Basic Linear Algebra
 * Desirable: Experience with other ML toolkits (preferably Python, such as [scikit-learn](http://scikit-learn.org/stable/), or c++ such as [MLPack](http://www.mlpack.org/))
 * Desirable: Practical experience with ML
 * Desirable: Some experience with Shogun

### Description
This project is about improving Shogun's implementations of "the usual suspects". That is, basic ML algorithms that should be available in every toolbox (see below). The focus in Shogun often lies on cutting-edge algorithms, leaving the usual suspects with too little attention. This results in non competitive implementations in terms of speed, scalability, and stability. We aim to identify such algorithms, benchmark them, and finally improve efficiency, code cleanliness, and test coverage. We want Shogun's implementations to be (at least) as fast as the fastest third party library!

### Details
Involved algorithms definitely would include:

 * K-Means
 * (Kernel) Ridge Regression
 * Lasso
 * KNN
 * PCA/LDA
 * ...

As an example, have a look at issue [#2987](https://github.com/shogun-toolbox/shogun/issues/2987), which illustrates the problems on KMeans: It is slow, partly wrong, and does not scale.

### Waypoints and initial work
After having identified a number of algorithms, the typical approach would be to

1.) Write a script/program to compare performance with an existing ML library, on a challenging practical application. Such a benchmark should test various aspects: correctness, speed, different data sizes, different problem flavours.

2.) Identify the most severe bottlenecks where Shogun does not perform well. This might be pure software-engineering related questions, but also depend on the mathematical formulations of the algorithms (see e.g. [PCA improvements](https://github.com/shogun-toolbox/shogun/issues/1876)).

3.) Re-write the code that concerns them. Test. Produce clean code that is easy to read (see for example our HMM implementation if you want to see unreadable code)

4.) Give the whole implementation a general clean-up: Documentation, unit testing, examples.

5.) IPython notebook with a real-world application

The [K-means issue](https://github.com/shogun-toolbox/shogun/issues/2987) is a great place to start.

### Optional
Once the Shogun implementation runs competeitive, we can look into further speed-ups to be gained by multicore computations, approximations, and other. We can also have a survey on Shogun's mailing list to identify methods that people like to be improved. A third option would be to simplify existing interfaces to make our algorithms easier to use.

### Why this is cool
This project offers the chance to learn about many fundamental ML algorithms from a practical perspective, with a focus on efficiency. As the usual suspects are the most used algorithms by Shogun users, it is likely that many people will execute code that you wrote. 