# Large-Scale Gaussian Processes

### Mentors
 * [Marius](https://www2.informatik.hu-berlin.de/~kloftmar/)
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
Medium
You need know
 * Applied Statistical Hypothesis Testing
 * Linear Algebra
 * Linear Algebra in C++
Helpful
 * Gaussian Process basics, SVM basics

### Description
In this project, we aim to implement large-scale statistical testing into SHOGUN. There is some prior work mainly on kernel mean embeddings. We will implement standard statistical tests used in large scale manner in genome-wide association studies. This includes Fisher's exact test and mixed models (Lippert et al.). The major focus of the project is on multiple testing, so multiple testing threshold corrections will be implemented, starting with the family-wise error rate (FWER) and probably also the (augmented) false discovery rate (FDR). If there is enough time, extensions of multiple testing to GPs and SVMs can be tackled.

### Waypoints and initial work
 * Check / debug current Fisher's exact test implementation
 * implement chi square test and trend test
 * Implement FWER computation using Young-Westfall permutation procedure
 * Mixed Model Testing with kernel matrix (Lipper et al)
 
### Optional
 * Implement FDR computation using Young-Westfall permutation procedure
 * SVM based testing, GP based testing
 

### Useful ressources
 * http://en.wikipedia.org/wiki/Statistical_hypothesis_testing
 * http://en.wikipedia.org/wiki/Fisher%27s_exact_test
 * http://en.wikipedia.org/wiki/Cochran%E2%80%93Armitage_test_for_trend
 * http://en.wikipedia.org/wiki/Chi-squared_test
 * http://en.wikipedia.org/wiki/Multiple_comparisons_problem
 * http://en.wikipedia.org/wiki/Familywise_error_rate
 * http://en.wikipedia.org/wiki/False_discovery_rate
 * http://www.nature.com/nmeth/journal/v8/n10/abs/nmeth.1681.html