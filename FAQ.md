# Frequently Asked Questions

#### Which language and shogun interface should I use
I personally consider the modular interfaces (python_modular, octave_modular) to be "best". Here best means very flexible and easily extensible. However, in case you just want to train a single SVM with a single or multiple kernels all of the static interfaces are sufficient. And well, of course you should be using python http://www.python.org :-)

#### I've found a bug, where should I report it?
Either report it in our bug tracker https://github.com/shogun-toolbox/shogun/issues or ask on the mailinglist.

#### Do I need CPLEX to use multiple kernel learning?
No, as of version 0.7.0 you won't need cplex if you want to learn the weights in front of the kernels. However, to enable Multiple Kernel Learning with CPLEX(tm) just make sure cplex can be found in the PATH. For standard 1-norm multiple kernel learning (MKL) the GNU Linear Programming Kit (GLPK) version at least 4.29 or CPLEX is required. For general p-norm MKL with p>1 it will work nonetheless.

#### Is it multiple kernel learning when I use many kernels?
No, a plain combination of features/kernels will remain a plain concatenation. Only in case you learn the kernel weights you really do MKL. In the static interfaces you can issue
```
    [W]=sg('get_subkernel_weights') 
```

and check whether all weights W are still 1.0.

#### Does shogun compile under Microsoft Windows?
Yes! With cygwin 1.7.1 the cmdline, python, python_modular and octave compile cleanly. However, octave_modular won't work since the swig version in cygwin is outdated - if you want that interface you need to compile swig manually. In addition neither R and matlab interfaces do currently compile: cygwin does not yet include up-to-date mingw packages. As none one of us use windows, and things (in external dependencies) break frequently, feel free to submit patches to cygwin. Ohh and one hint: use

```
    make DESTDIR= install
```

to install (etc.). A plain ./configure;make;make install will fail since repeated slashes (e.g., '//usr/local') in cygwin are problematic but in posix systems simply ignored.

#### How does shogun do its memory management?
As does python, we use reference counting internally, i.e. objects holding a reference to another object should increase the reference count of the object they are referencing and decrease the counter when they finished using the object. It should be noted that loops (e.g., object A holding a reference to object B and vice versa) are not detecting and may thus create memory leaks. However, this scenario can so far be easily avoided - just don't create a combined kernel that contains itself as a subkernel ;-)

