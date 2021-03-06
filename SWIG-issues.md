##  SWIG
Compiling modular interfaces more and more gets a problem. Both compile time and memory requirements explode with more classes added to Shogun. We already sometimes hit the memory limit of travis, which results in unfinished (gray) builds, for example [this one](https://github.com/shogun-toolbox/shogun/issues/2562).

Furthermore, the SWIG magic might be very interesting for other projects, so it could be a good idea to pull it out from the Shogun source tree into a seperate mini-project.

This article presents some thoughts and possible solutions to this problem.
 
## Initial draft
See [here](https://github.com/shogun-toolbox/shogun/pull/2567). Reduce the size of SWIG's from 991480 to 813388. Peak memory usage from 2.4GiB to 1.9 GiB. This is just due to a few include guards.

## Why SWIG is big
Every method in Shogun's header files that are included in the ```modular.i``` generates a couple of lines in the SWIG output. In particular, templated methods are expensive as they are instantiated for all basic data-types in Shogun. The way to solve this therefore must be to reduce the number of methods exposed to SWIG. [Here](https://github.com/shogun-toolbox/shogun/issues/2562) is the top 10 list of classes with most methods exposed to the modular interfaces.

## D-pointer-like ideas and why they do *not* help
In an optimal world, there is a class that *only* represents the interface to modular interfaces, i.e. how Shogun is used from outside C++. This class in its .cpp file then might call methods of an implementation helper class. See for example the [LMNN](http://www.shogun-toolbox.org/doc/en/latest/LMNN_8cpp_source.html) class, which uses a helper class in its implementation that contains a bunch of helper methods.

This is closely related to D-pointers. We investigated this and concluded that it will not help us.  SWIG only touches public methods. As all helper methods that would go into an implementation class can just be made protected, this problem can easily be solved. 

The other problem with this approach is that there are C++ methods that *need* to be public, but should *not* be in SWIG. The only solution for those is explicitly ignore them (see below). Creating separate interface classes just for SWIG will not help as instances of them need to be passed around in the modular interfaces, and these instances need to implement certain interfaces on a C++ level. Let's clarify this through an example. Consider the following code from the Python modular interface:

```
fname='fm.csv'
feats=RealFeatures(CSVFile(fname))
```

The class `CSVFile` implements a bunch of methods to read data from disk, e.g. `get_vector(float*& vector, int& len)`. This method needs to be public to be accessible from feature classes (such as RealFeatures). However, it does not need to be accessible at all from the modular interfaces provided by SWIG. Therefore, it must be a public method of `CSVFile`, but we don't want SWIG to generate any bindings for it.

## What helps?
Here are two suggestions. The first one can be applied to *any* of the classes that blow up SWIG's output, the second involves clean-ups that might need a bit more thought, but are cleaner solutions.

#### SWIG's ```%ignore``` and the ```#ifndef SWIG // SWIG should skip this``` guard
There are a number of public methods that *have* to be public (for example the ```CLibSVMFile::get_vector*``` methods that are called from other C++ classes), but that we do not want to expose to SWIG. These can be explicitly ignored. See example below.

#### Clean up ```SGVector``` and similar
All ```SG*``` classes are primarily meant for data exchange with Shogun's interfaces (in particular modular interfaces). As such, they are only meant to represent data, not offer operations on those (apart from fundamental access such as ```[]``` operators and similar). However, currently, those classes contain lots of algrothmic code, see for example [here](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1SGVector.html): ```range_fill, abs, permute```, etc.
Every of those methods will result in a wrapper method in SWIG, for *every* of the template arguments. All such methods should be moved into ```CMath, CStatistics, linalg```, or similar. This way, SWIG produces less code, and separation of concerns is respected: these objects are just there for passing data through Shogun's internal and external interfaces.


## Examples and their impact
### SWIG's %ignore
Adding in ```LibSVMFile.h```
```
#ifdef SWIG // Methods to hide from SWIG
%ignore get_vector;
%ignore get_matrix;
%ignore get_ndarray;
%ignore get_sparse_matrix;
%ignore get_string_list;
%ignore get_sparse_matrix;

%ignore set_vector;
%ignore set_matrix;
%ignore set_ndarray;
%ignore set_sparse_matrix;
%ignore set_string_list;
%ignore set_sparse_matrix;
#endif
```
or alternatively putting
```
#ifndef SWIG // SWIG should skip this part
... all set_get-vector/matrix methods
#endif // #ifndef SWIG // SWIG should skip this part
```
and compiling reduces the number of lines in ```modshogunPYTHON_wrap.cxx``` by roughly 20k (from 990k to 970k).
Excluding all ```SGVector``` that are not needed (mostly linear algebra), reduces the file by 80k lines.
Memory usage (tuning both above classes) dropped from 2.34 to 2.17GiB. Keep in mind these are just two files.

*Note:* I believe that these SWIG ignores should *not* be in a separate file (currently ```modshogun_ignores```). It's way harder to maintain. Doing those in the interface classes makes it very easy to get a feeling for where its forgotten, etc.

## Further improvements
We can remove methods from SWIG. However, at some point, due to the sheer number of classes added to Shogun, we are likely to break memory bounds -- all SWIG output is put into a single file. This opens another door to deal with the problem. Shogun could be split into multiple modules (say core-framework and algorithms, where algorithms could be partitioned into more parts), which could be translated through SWIG seperately. This allows to scale the number of exposed classes much even further.

## Appendix
###Comparing peaks of memory used by a process group

[Source](https://gist.github.com/netj/526585) (retrieved 26th October, 2014).

```
#!/usr/bin/env bash
# memusg -- Measure memory usage of processes
# Usage: memusg COMMAND [ARGS]...
#
# Author: Jaeho Shin <netj@sparcs.org>
# Created: 2010-08-16
set -um
 
# check input
[ $# -gt 0 ] || { sed -n '2,/^#$/ s/^# //p' <"$0"; exit 1; }
 
# TODO support more options: peak, footprint, sampling rate, etc.
 
pgid=`ps -o pgid= $$`
# make sure we're in a separate process group
if [ $pgid = $(ps -o pgid= $(ps -o ppid= $$)) ]; then
    cmd=
    set -- "$0" "$@"
    for a; do cmd+="'${a//"'"/"'\\''"}' "; done
    exec bash -i -c "$cmd"
fi
 
# detect operating system and prepare measurement
case `uname` in
    Darwin|*BSD) sizes() { /bin/ps -o rss= -g $1; } ;;
    Linux) sizes() { /bin/ps -o rss= -$1; } ;;
    *) echo "`uname`: unsupported operating system" >&2; exit 2 ;;
esac
 
# monitor the memory usage in the background.
(
peak=0
while sizes=`sizes $pgid`
do
    set -- $sizes
    sample=$((${@/#/+}))
    let peak="sample > peak ? sample : peak"
    sleep 0.1
done
echo "memusg: peak=$peak" >&2
) &
monpid=$!
 
 
# run the given command
exec "$@"
```