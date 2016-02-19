# A Shogun cookbook

### Mentors
 * Heiko (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)

### Difficulty & Requirements
Easy. You need to be able to
 * Write English
 * Experience in web-design
 * Code in Python
 * Desirable: Sphinx, CMake
 * Desirable: Shogun experience

### Description
This project is about bringing a new Shogun cookook to life. This puts together a year of work on Shogun's [meta language](https://github.com/shogun-toolbox/shogun/wiki/Example_Generation), and our [prototype](https://github.com/shogun-toolbox/shogun/tree/feature/sphinxdoc/doc/sphinx) for a sphinx-based API documentation system. The goal is to have API example that cover all target languages and all algorithms, in a form that looks like [this](https://www.dropbox.com/sh/t9hl77g3iaelqq8/AAB7b5LG0DmnFLBD0OeQ_ssla?dl=0&preview=shogun_cookbook.jpg)



### Details
As you see in the screenshot above, there will be code listings for all target languages (selected through a tab), and some text explaining the interface. The project is about transforming our [Python API examples](https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/python_modular) into Meta-language examples, which are automatically translated into executable code listings. In a second step, we can write some English text that explains the API in a minimal way, referencing the snippets in the code.

### Waypoints and initial work
To start, you can:

 * Check the files in our [prototype](https://github.com/shogun-toolbox/shogun/tree/feature/sphinxdoc/doc/sphinx) and try to run it locally.
 * Add an example for an existing Python example

Once all Python examples are translated to meta examples, we aim to completely remove the old ones. In a next step, all generated code listings should be embedded into our CMake build.

### Optional
We also aim to remove all static interface's examples and tests. Those have to migrated to the new system too.

### Why this is cool
Shogun's main strength is the support of a large number of target languages. This project is a great showcase for this killer feature.

### Useful ressources
 * Put a list of ressources/links here