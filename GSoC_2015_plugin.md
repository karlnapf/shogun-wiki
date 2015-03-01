# Framework for plugin-based architecture

### Mentors
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)
 * [Viktor](Viktor%20Gal) (github: [vigsterkr](https://github.com/vigsterkr), IRC wiking)

### Difficulty & Requirements
**Difficult**. You need to have:
 * advanced C++ and programming skills (deep understanding of shared libraries, linking, etc)
 * no fear of working with big legacy codebases

### Description
Currently, Shogun is made of a monolithic structure of classes which seems to be a bit cumbersome to extend and maintain. We consider some kind of plugin architecture as a possible way to solve these problems. Such an architecture would support dynamic behaviour of plugins: a user could download a new classifier and run it instantly without any rebuilds. In this task the student have a chance to get deep understanding of important low-level details of dynamic libraries and ABIs.

### Why this is cool

This is great a chance to speed up Shogun development and make it more flexible and easier to use. The project involves massive refactoring of all the Shogun code so you will learn how to handle big codebases (>100k LoC) which is a useful skill for any software engineer.

### Details

### Waypoints and initial work

* First of all, we'd have to prepare for such a major change. We need to have good infrastructure to load dynamic libraries, support generic attributes and other stuff like that 
* The easiest by concept but hardest by the amount of work to be done is to finally split all the Shogun code to separate dynamic modules

### Useful resources

* [Plugin architecture](http://blog.nuclex-games.com/tutorials/cxx/plugin-architecture/)
* [Building Your Own Plugin Framework](http://www.drdobbs.com/cpp/building-your-own-plugin-framework-part/204202899)