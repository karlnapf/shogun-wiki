This document aims to explain Shogun's continuous integration testing. This is different from [unit testing](Unit-testing). See [here](http://stackoverflow.com/questions/10752/what-is-the-difference-between-integration-and-unit-tests) or search the web if you don't know what these terms mean.

## Python modular integration tests
Those tests are the main part of our integration tests. All [Python](https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/python_modular) examples are used for integration testing (apart from being checked to run without error). Each example at the end returns computed values and which are compared to reference values.

### Python example structure
See [Python-examples](Python-examples). In a nutshell, each example contains a function that takes a number of parameters, and then returns computed values/instances for those values.

### Creating reference files
The example function returns something as

```
return knn,knn_train,output,multiple_k
```

Those can be
 * Basic data types
 * Vector types (numpy.array in Python)
 * Shogun objects (```CSGObject``` subclasses)

Those values are then serialised, using [pickle](https://docs.python.org/2/library/pickle.html) for numeric data and ```CSGObject::save_serializable``` for Shogun objects. The ```generator.py``` [script](https://github.com/shogun-toolbox/shogun/blob/develop/tests/integration/python_modular/generator.py) is responsible for this. For example, to generate the serialised file for ```classifier_knn_modular.py```, simply run

```
generator.py classifier_knn_modular
```

which will generate files ```classifier_knn_modular0.txt, classifier_knn_modular1.txt``` in the directory ```shogun/data/testsuite/python2-tests``` (same for python3). The number of files depends on the parameter list in the example. This is a list of lists that contains possible parameters to run the example with. Each inner list will result in a different serialised file. For example,

```
[[traindat,testdat,label_traindat,2.1,1,1e-5],[traindat,testdat,label_traindat,2.2,1,1e-5]]
```

gives two files.

These serialised objects are stored in the [shogun-data repository](https://github.com/shogun-toolbox/shogun-data/tree/master/testsuite/python2-tests), which involves committing them and sending a pull request, and updating the data revision subsequently (commit ```data``` in the [main repository](https://github.com/shogun-toolbox/shogun))

### Testing against reference files
If you run ```make test```, this will at some point run all python examples. For each of the produced results ```a```, the ```tester.py``` [script](https://github.com/shogun-toolbox/shogun/blob/develop/tests/integration/python_modular/tester.py) will then de-serialise the reference file's reference result ```b``` and compare them via ```CSGObject::equals(a,b)``` up to a certain floating point tolerance (currently 1e-5 for Shogun objects). If an error occurs, the debug output of ```CSGObject::equals``` is printed to help people find the differences.

You can check tests manually via for example

```
tester.py classifier_knn_modular
```

### A common source of errors: parameter changes
The integration test will fail if any of the registered parameters are changed. This is the most common source or errors: Change of
 * name
 * type
 * adding parameters
 * removing parameters

will all fail the integration tests. This means you have to re-generate the reference file from the above step if you need to do such changes. In order to not let errors slip through, make sure that

 * you check whether the test worked before you do the change
 * update the reference file and send a PR to shogun-data *before* sending your patch
 * update the data-revision in your patch

Only then, [travis](Travis) and our [buildbot](Buildbot) will not complain.

Using the debug output of ```CSGObject::equals```, which is printed whenever a test fails, these errors are easy to spot.

### Changed results
If the numerical results do actually differ, this might be caused by

 * some internals changed
 * a bug was introduced

It is your task to check which case happened. You might update the integration testing file if you are *sure* that no bug was introduced.

## Explicit integration tests
TODO

## See also
[#2508](https://github.com/shogun-toolbox/shogun/issues/2508)