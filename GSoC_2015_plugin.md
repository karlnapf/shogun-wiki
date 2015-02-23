# Framework for plugin-based architecture

### Mentors
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)
 * [Viktor](Viktor%20Gal) (github: [vigsterkr](https://github.com/vigsterkr), IRC wiking)

### Difficulty & Requirements
**Difficult**. You need to be able to:
 * advanced C++ skills (rather deep understanding of shared libraries, linking, etc)

### Description
Currently, Shogun is made of a monolithic structure of classes which seems to be a bit cumbersome to extend and maintain. We consider some kind of plugin architecture as a possible way to solve these problems. Such an architecture would support dynamic behaviour of plugins: a user could download a new classifier and run it instantly without any rebuilds. In this task the student have a chance to get deep understanding of important low-level details of dynamic libraries and ABIs.