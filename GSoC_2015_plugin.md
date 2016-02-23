# A unified interface for Machine Learning & a framework for plugin-based architecture

### Mentors
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)
 * [Viktor](Viktor%20Gal) (github: [vigsterkr](https://github.com/vigsterkr), IRC wiking)

### Difficulty & Requirements
**Difficult**. You need to have:
 * A good understanding of different ML algorithms (supervised/unsupervised/...)
 * Desirable: Experience with existing ML packages
 * advanced C++ and programming skills (deep understanding of shared libraries, linking, etc)
 * no fear of working with big legacy codebases (you know grep right?)

### Description
A highly challenging and interesting project, which consists of two parts: Designing a unified ML interface and low-level details of dynamic libraries.

Currently, Shogun is made of a monolithic structure of classes which is cumbersome to extend and maintain:

 * too many classes
 * too many dependencies
 * takes too long to add algorithms

We want to build a plugin architecture to solve these problems. Such an architecture would support dynamic behaviour of plugins: a user could download a new classifier and run it instantly without rebuilding Shogun. The core Shogun interface has to be designed to support a large number of ML paradigms, and these are hidden in plugins. This also drastically simplifies the compilation process (and time).

We have drafted a design document [here](https://github.com/shogun-toolbox/shogun/wiki/New-parameters-framework-and-plugins)


### Why this is cool

This is great a chance to speed up Shogun development and make it more flexible and easier to use. The project involves massive refactoring of all the Shogun code so you will learn how to handle big codebases (>100k LoC) which is a useful skill for any software engineer.

Another highly interesting part of the project would be to design a core API that supports all of Shoguns algorithms. But don't worry: our mentors are all ML veterans and can help you with this.

This is something we wanted to do for a long time, so you would have all developers on your side. As well as eternal fame for finally making Shogun easy to use again ;)

### Waypoints and initial work

The project consists of three parts

1. ML core interface design. (party can be done in application period)
2. Infrastructure to load dynamic libraries (see [design draft](https://github.com/shogun-toolbox/shogun/wiki/New-parameters-framework-and-plugins))
3. Refactoring existing code.

A detailed schedule is essential for the project.

### Useful resources

* [Design draft](https://github.com/shogun-toolbox/shogun/wiki/New-parameters-framework-and-plugins)
* [Plugin architecture](http://blog.nuclex-games.com/tutorials/cxx/plugin-architecture/)
* [Building Your Own Plugin Framework](http://www.drdobbs.com/cpp/building-your-own-plugin-framework-part/204202899)


Get back to the [main projects page](Google%20Summer%20of%20Code%202016%20Projects).