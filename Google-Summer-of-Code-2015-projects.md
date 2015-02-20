# A list of potential GSoC 2015 projects.
To add, please create a new wiki page for each project that you describe. Name them as "GSoC_2015_project_MCMC" etc. Here is a [template](GSoC_2015_project_template).

# Main focus
This year's GSoC is about improving Shogun, rather than extending it. Exceptions allowed.

 * *Fewer* new algorithms. Rather improve existing ones: Usability, efficiency, documentation, application
 * *Fewer* students. More intense mentoring, interaction between students, blogging, documenting
 * Projects on
   * Installation: most important
   * Clean ups of: framework, build process, algorithms, usability, documentation
   * Removing legacy code
   * Efficiency: High performance computing, parallelisation, cloud, benchmarking
   * Applications: Using Machine Learning as a tool to improve the world, rather than toy examples
   * Pipelines & Framework: Improve usability on standard workflow pipelines
   * Usablity: Building and Installing Shogun has to be easier

**[Mentors (and students) this year](GSoC_2015_mentors_students_)**

# Projects
**ALL** students will be required to document existing Shogun code on a weekly basis during GSoC. We need a list of all methods in Shogun, along with slim documentation on how to use them. Details to follow!

## Improving Shogun
These are roughly ordered in our priority in them. Most of them *do not* focus on Machine Learning but rather on software engineering.

 * [**Easy installation on major platforms**](GSoC_2015_project_installation)
 * [Native MS Windows port](GSoC_2015_windows)
 * [A Shogun Detox](GSoC_2015_clean_up_infrastructure)
 * [Unifying Shogun's linear algebra](GSoC_2015_project_linalg)
 * [HMM cleanup and application](GSoC_2015_project_hmms)
 * [Shogun cloud extensions](GSoC_2015_cloud_shogun)
 * [Native MS Windows port](GSoC_2015_windows)
 
## Extending Shogun:
The projects we would like to limit in numbers.

### Algorithms
 * [Fundamental ML 2: LGSSMs](GSoC_2015_project_fundamental)
 * [Large Scale Gaussian Processes](GSoC_2015_project_large_gps)
 * [Hip Deep learning](GSoC_2015_project_deep_learning)
 * [Solver for the KKT System](GSoC_2015_project_kkt)
 * [Dual coordinate ascent solver for SO-SVM](GSoC_2015_project_dca_sosvm)
 * [LP/QP Framework](GSoC_2015_project_lpqp)
 * [Density Estimation in Infinite Dimensional Exponential Families](GSoC_2015_project_kernel_infinite_exponential)
 * [Debiasing & Cluster computing](GSoC_2015_project_debiasing)


### Framework
 * [Independent jobs Framework](GSoC_2015_cluster_shogun)
 * [MCMC & Stan](GSoC_2015_project_MCMC_Stan)


# TODO list
## Other ideas:
 * Cool pipelines
   * A kaggle pipeline for supervised prediction.
   * Spectrometer (there is an open-source hardward project on this)
   * Music brainz predictions (The cool hair guy at GSoC is the one we should talk to here)
   * Some bio thing?
   * Collaboration with MLPack for toolkit wide performance/accuracy testing

## Infrastructure:
 * Easy Model selection!
 * Get rid of static interfaces, migrate all tests etc
 * Matlab swig bindings
 * [REST interface](GSoC_2015_project_rest)

## Clean ups:
 * Modularise Shogun
 * [Replace parameter framework](GSoC_2015_project_parameters)
 * Benchmark existing algos and improve!