# Flexible modelselection 2
Following up on one of our very first GSoC (2011) projects, this project intends to clean up, unify, extend, and scale-up Shogun's modelselection and parameter framework. It is a cool mixture of dealing with old and new code.

### Mentors
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)

### Difficulty & Requirements
Medium to advanced. Depends on ambitions, but we are flexible on student's abilities.

You need to know about
 * Modelselection basics (x-validation, search-algorithms, implementation)
 * Shogun's modelselection framework
 * Shogun's parameter framework
 * Intermediate C++
 * Bayesian optimisation frameworks like [MOE](https://github.com/Yelp/MOE) are a plus
 * Stochastic optimisation frameworks, like [cma](http://en.wikipedia.org/wiki/CMA-ES) are a plus
 * Knowledge on Shogun's [cluster computing plans](https://github.com/shogun-toolbox/shogun/wiki/GSoC_2015_cluster_shogun) is a plus
 * Knowledge on [other libraries'](http://scikit-learn.org/stable/model_selection.html) modelselection or other [modelselection frameworks](https://github.com/mwhoffman/pybo) is a plus

### Description

Shogun's modelselection was built at a time when Shogun was quite different than it is today. This is true even more for the parameter framework itself. As a result, we have a working (and powerful) framework for modelselection that is hard to understand, hard to use, and pollutes Shogun's base classes. Again the same is true for the parameter framework. The goal of this project is to modernise and unify both frameworks, and in a second part to extend it with flexible black-box optimisation schemes. As an optional part, we could work on distributed/parallel computation for modelselection.

### Details
***Parameter framework***
Unifying parameter manipulation.

Currently, Shogun's base class allows subclasses to register every parameter and its type. This eventually allows for accessing them in an automated way (i.e. in a loop without knowing number, name or type of parameters beforehand). This is for example used for serialisation (which we intend to drop during this project). Certain parameters of choice can be marked as "available" for modelselection (or even for gradient based optimisation). Our framework is then able to manipulate values of those parameters from within optimisation algorithms.

Since those parameter lists pollute the base class, we would like to rework the parameter framework in order to allow for the same functionality with a much simpler API (we could generate automatic getters/setters on the fly). Sergey, could you add details here?

***Seperation of concerns***
Global modelselection only deals with truly free parameters.

The next step would be to check the Gaussian Process framework (which massively uses the parameter framework to modify parameters). GPs allow to learn hyperparameters in a guided way - that only works for GPs. The same is true for many learning algorithms. Therefore, there is no need to use the global framework for such optimisations. The GP hyperparameter learning should therefore be decoupled from the global framework. This will allow to drop the gradient modelselection parameters from the base class.

***Developing a clean API***
Once the parameter access and manipulation is sorted, we need an alternative way to specify free parameters to learn. This needs to be done in an elegant and flexible way, what is also easy to use. I.e. *not* like the current [parameter trees](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CModelSelectionParameters.html).

***Bayesian and stochastic optimisation for modelselection***
Bayesian optimisation and stochastic optimisation are powerful frameworks for blackbox optimisation. We aim to integrate bindings for both during the project. There is plenty of external libraries that do the algorithms for us, so this task is mostly about designing interfaces that tell Shogun to cross-validate the algorithm on the next set of parameters and reporting its performance. We aim for both [MOE](https://github.com/Yelp/MOE) and [CMA-ES](http://en.wikipedia.org/wiki/CMA-ES).

### Waypoints and initial work
The project consists of two major themes, which perfectly fit into our GSoC 2015 focus.

***Cleaning up***
 * Reworking Shogun's parameter framework
 * Reworking the way parameters are marked for modelselection
 * Migrating existing modelselection algorithms to reworked framework
 * ...

***Provide new ML pipeline tools***
 * Integrate new algorithms for modelselection (CMA/MOE)

### Optional
As modelselection often is expensive, an optional part of the project could investigate how to scale up the process using parallel computing, see the [independent jobs project](https://github.com/shogun-toolbox/shogun/wiki/GSoC_2015_cluster_shogun). This would involve extending Shogun's computing interface to make use of multi-core or multi-machine backends. Depending on how ambitious the student is.

### Why this is cool
There is hardly any algorithm without free parameters. Currently Shogun only has brute force search to tune them automatically. While this works for SVMs, it it hopeless for anything more than 2 parameters. Certainly, a clean and easy way to quickly tune parameters would massively boost Shogun's usability. The project spans a huge range on topics within and outside of Shogun, including framework internals as well as cutting edge algorithms for optimisation. Super interesting even for ourselves. Be ready to learn a lot.

### Useful resources
 * Shogun's modelselection [classes](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CModelSelection.html)
 * [Parameter trees](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1CModelSelectionParameters.html)
 * [MOE](https://github.com/Yelp/MOE) are a plus
 * [CMA-ES](http://en.wikipedia.org/wiki/CMA-ES)

Github issues on the topic (contain old and recent ideas)
 * https://github.com/shogun-toolbox/shogun/issues/1251
 * https://github.com/shogun-toolbox/shogun/issues/959
 * https://github.com/shogun-toolbox/shogun/issues/1251
 * https://github.com/shogun-toolbox/shogun/issues/1265