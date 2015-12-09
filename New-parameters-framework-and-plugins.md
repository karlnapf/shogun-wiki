Sergey and Heiko at NIPS 2015. We plan to re-work Shogun's parameter framework. The goal is to have

 * an easier syntax
 * Work towards allowing plugins for Shogun
 * Clean up the CSGObject base class

This is done via adding two approaches to change Shogun parameters.
 * String based: for Shogun users, wrong usage produces run-time errors, easy syntax (also in SWIG), slow
 * Tag (C++ struct) based: for Shogun devs, type-safe (in C++) at compile time, fast, for internal use (ugly interface via SWIG)

Tag-based
=========

Tags are fast and type-safe way to set and get parameters. Below is a snippet how this could work.

Tag is basically a templated class with only one field - its name
```cpp
template <class T>
class Tag 
{
  Tag(string name) : name_(name) { }
  string name_;
};
```
in SWIG we would have `IntTag`, `StringTag`, `KernelTag` (stands for `Tag<int>`, `Tag<string>`, `Tag<CKernel>`).

Its usage would look like: 
```cpp
SGObject object;
Tag<int> intParameter;
object.set(intParameter, 3)
```
while `set` implementation of `SGObject` would look
```cpp
template <typename T>
void set(Tag<T> tag, T value)
```

This is type-safe (you can't set a float with int tag or whatever type discrepancy it be, good for modelselection and internal usage) and fast (we can hash tags and put them into fast integer map). The thing is that we have to decide what `T` variants do we support (because of SWIG as it could not support exporting templates). Currently, it looks like we should export basic types available in all target languages (int, double, string, ...) and our *basic classes*. Basic classes are actually `CClassifier`, `CKernel`, but not `CLibLinearSVM`. This demarcation enables us to implement plugins under the hood. Plugins are described in next part.

String-based
============

For user convenience, we should also support cleaner way to do the same thing as with tags. This way, we just name our parameters and refer them via strings. For example, here's how we can set the gaussian kernel width 

```python
kernel = shogun.GaussianKernel()
kernel.set("width", 1.0)
```

If we tried to set `width` with a string we would get a runtime error:

```python
kernel.set("width", "твою мать");
# gets you runtime error
```

Plugins
=======

The parameters thing enables us to implement plugins seamlessly because we don't have to export all class interfaces explicitly. Advantages of plugins are:

* No need to recompile whole Shogun when you develop some other implementation
* Base shogun would have no dependencies on some crazy libraries so we can easily install it to any platform. Plugins would bother with concrete libraries and we get 
* We can have 'frozen' implementation of base shogun that actually could be installed and never touched again. Plugins could change arbitrary
* Scientists could use Shogun again as they don't have to bother with compiling base shogun

In Python (and any other swig-supported language) it would look like (remember `CKernel` was chosen to be a *base class* of shogun, so we provide it in the interface):

```python
X = ...
features = shogun.features("real_dense");
features.set("data", X);
kernel = shogun.kernel("gaussian");
svm = shogun.classifier("libsvm");
kernel.set("width", 5.0);
svm.set("kernel", kernel);
svm.train();
``` 

Due to Python's flexibility we also have possibility to use prettier syntax:
```
kernel = shogun.kernel.gaussian
```

Basically, a plugin would be a set of classes orchestrated by one plugin class:

```

#include <myplugin/myclassifier.h>

class MyPlugin : public shogun::Plugin
{
   void register()
   {
      provides<MyClassifier>();
   }
}
```

Some plugins would require other plugins, it would be handled via:

```
      requires<Distribution>("gaussian");
```

There is no constraint on possible dependency cycles, we can just load any required plugin. Plugins could be loaded automatically when you request it:

```python
import shogun
print Hello world

# actual loading of .so/.dylib/.dll happens there
kernel = shogun.kernel("gaussian");
```

Every algorithm, every kernel, every whatever would have a separate plugin and they can be grouped together to provide some reproducible code for some NIPS paper.

Next steps
==========

We would have to make the following steps (each include proper unit-testing, we should go for 100% test coverage) 

To create a proof of concept we would have to do:
* Implement a tag for some type
* Add generic storage of parameters to SGObject (some map)
* Make sure it works with swig in any target language 

Next, we can start implementing actual parameter system (should be done pre-GSoC!):

* Implement tags for generic types and get/set with tags
* Add additional interface for string-based get/set
* Make sure it works ;)

Next step would be to implement plugins:
* Implement base class for plugin
* Make one of the classes of shogun both a plugin and regular class
* If it works - document the migration process: remove the getters/setters of this class, drop avoidable dependencies, ...

Finally, we can start migrating all the classes to plugins (could be done during pre-GSoC students).