# Fundamental Machine Learning Algorithms

The aim of the project is to improve our implementation of fundamental ML algorithms. You can build on a good foundation - and continue where we stopped [last year](https://www.google-melange.com/gsoc/project/details/google/gsoc2014/mazumdarparijat/5738600293466112).

## The usual suspects

**Update**: This project is in high demand, so we might accept 2 students for it: you would then work together, one person benchmarking, the other improving the code, then vice versa. One can also imagine one part benchmarking and one part improving. Together, the two of you could have a very big impact!

This requires some preparation: we need a well-documented list of all the algorithms that need work. So if you're interested in this project, it would be a good idea to start benchmarking some of our algorithms. Eventually, rather than doing this with Python scripts, we would like to use an [existing benchmarking system](https://github.com/zoq/benchmarks). This could be your first pull-request :)

But make sure you also look at the other projects -- the point is to get
involved in Shogun itself. You can guess from the [mailing list archives](getting in touch)
how many people will apply for each project.

### Mentors
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)
 * [Ryan Curtin](https://github.com/rcurtin)

### Difficulty & Requirements
**Easy to Medium** -- depends on you. You need
 * ML Algorithms in C++
 * Re-factoring existing code / design patterns
 * Knowledge of very basic ML algorithms
 * Basic Linear Algebra
 * Desirable: Experience with other ML toolkits (preferably Python, such as [scikit-learn](http://scikit-learn.org/stable/), or c++ such as [MLPack](http://www.mlpack.org/))
 * Desirable: Some initial experience in an [existing benchmarking system](https://github.com/zoq/benchmarks)
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
 * Neural networks
 * Gaussian Processes
 * ...

As an example, have a look at issue [#2987](https://github.com/shogun-toolbox/shogun/issues/2987), which illustrates the problems on KMeans: It is slow, partly wrong, and does not scale.
Another example is [#3048](https://github.com/shogun-toolbox/shogun/issues/3048) which shows that Shogun's PCA is 10x faster than sklearn.

### Waypoints and initial work
After having identified a number of algorithms, the typical approach would be to

1.) Write a script/program to compare performance with an existing ML library, on a challenging practical application. Such a benchmark should test various aspects: correctness, speed, different data sizes, different problem flavours. *UPDATE:* This step now should be done as part of [mlpack's benchmarks](https://github.com/zoq/benchmarks). Ryan will be an additional mentor to help us. The results page can be found [here](http://www.mlpack.org/benchmark.html). We highly appreciate any ideas to make this part as smooth as possible.

2.) Identify the most severe bottlenecks where Shogun does not perform well. This might be pure software-engineering related questions, but also depends on the mathematical formulations of the algorithms (see e.g. [PCA improvements](https://github.com/shogun-toolbox/shogun/issues/1876)).

3.) Re-write the code that concerns the algorithms in question. Test. Produce clean code that is easy to read (see for example our HMM implementation if you want to see unreadable code)

4.) Give the whole implementation a general clean-up: Documentation, unit testing, examples.

5.) IPython notebook with a real-world application

6.) A report showcasing Shogun's performance compared to other libraries.

The [K-means issue](https://github.com/shogun-toolbox/shogun/issues/2987) is a great place to start.

### Optional
Once the Shogun implementation runs competitive, we can look to gain further speed-ups by multicore computations, approximations, and other means. We can also have a survey on Shogun's mailing list to identify methods that people like to be improved. A third option would be to simplify existing interfaces to make our algorithms easier to use.

### Why this is cool
This project offers the chance to learn about many fundamental ML algorithms from a practical perspective, with a focus on efficiency. As the usual suspects are the most used algorithms by Shogun users, it is likely that many people will execute code that you wrote. 