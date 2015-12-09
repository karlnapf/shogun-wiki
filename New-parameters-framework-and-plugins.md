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

shogun.kernel.gaussian

kernel = shogun.kernel("gaussian");
#kernel.set("width", shogun.range.exponential(-5.0, 5.0));
#kernel.set("width", shogun.prior.uniform(0, 1));
#kernel.set("width", shogun.just(3));
other_kernel = shogun.kernel("linear");

kernel.parameter("width").is(shogun.range());

svm = shogun.classifier("libsvm");
svm.set("kernel", shogun.any_of(kernel, other_kernel));
svm.train();

```


```
class SGObject {
    unordered_map<Tag, Parameter> parameters;

    template <T>
    void uses(string name) {
        parameters[Tag<T>(name)] = new parameter
    }

}

static Tag<CKernel> KERNEL("kernel");
static Tag<float> KERNEL_WIDTH("width");

class LibSVM {
    LibSVM() : Object() {
        uses<int>("max_iterations");
    }

    void train() {
        get(KERNEL).get(KERNEL_WIDTH);
    }
}

```

