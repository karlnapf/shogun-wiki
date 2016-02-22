# Easy installation on major platforms
**This is among the MOST IMPORTANT projects for GSoC**. It does not involve any Machine Learning but is a good way for hackers to get involved in Shogun. We might take 2 students with different OS skills here.
See also the [windows](GSoC_2015_windows) project.

### Mentors
 * [Sören](https://github.com/shogun-toolbox/shogun/wiki/AUTHORS) (IRC: sonney2k)
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)
 * [Viktor Gal](http://maeth.com/) (github: [vigsterkr](https://github.com/vigsterkr), IRC: wiking)

### Difficulty & Requirements

**Easy.**
Rather easy but massive and needs diligence.


It suits you best if you:

* Are not afraid of Mac OS X, Linux and Windows
* Know essentials of building tools like CMake and Makefile
* Are ok with patching some C++ code
* Feel like a real DevOps guy or a [duct tape programmer](http://www.joelonsoftware.com/items/2009/09/23.html)

### Description

We have to admit that Shogun is not really user-friendly to install. Users are going through some troubles even on quite major platforms which we should support better. We want to solve that. This project is the first step towards more smooth user experience that starts from the installation of Shogun on your favourite platform. The main goal of this project is to let users install Shogun on all major platforms in just a few clicks. And these should be documented (replacing all outdated documentation).

### Details

This project is a massive initiative to finally make Shogun really easy to try on all major platforms. 

Key points:
 * Compiling Shogun is flawless
 * Builds are put on our [buildbot](http://buildbot.shogun-toolbox.org/)
 * Nightly binary packages

All of these commands are expected to work on any popular platform Linux/Max/Win machine:
 * ```apt-get install shogun```
 * ```yum install shogun```
 * ```brew install shogun```
 * ```port install shogun```
 * ```shogun_installer.exe```

In addition, we want the Python bindings to be installable as:
 * ```pip install shogun```
 * ```conda install shogun```

Finally, an updated shogun [docker image](https://www.docker.com/) image with a pre-installed Shogun IPython notebook server. This is the bases for the [Shogun cloud](https://github.com/shogun-toolbox/shogun-cloud), where our [notebooks](http://www.shogun-toolbox.org/page/documentation/notebook) might be tried without installing Shogun.

Apart from the stable versions of such binaries, we expect to have them updated in a nightly fashion. In addition, we want the main builds be represented/updated on our buildbot. The key here is a clean system that produces all such things with minimal maintenance efforts, and has a good documentation.

### Waypoints and initial work
 * Try building Shogun on various platforms and fix and document problems that appear (good entrance task)
 * See our outdated [debian package](https://packages.debian.org/source/sid/shogun). A fully documented and easy to maintain debian package that eventually makes its way into debian testing is what we want.
 * Another good initial point might be to update our [nightly binary builds](https://launchpad.net/~shogun-daily/+archive/ubuntu/ppa) on ppa.
 * Work on the shogun cloud, make it work again. Include a nightly docker image on the buildbot.
 * A re-worked mac OSX [build](http://buildbot.shogun-toolbox.org/builders/osx2%20-%20modular_interfaces) are another good point, Homebrew or Macports, including a nightly binary build
 * Drafting the necessary steps to make any of the above commands work is essential before the project starts.
 * Build Shogun under windows/cygwin, see our [outdated build](http://buildbot.shogun-toolbox.org/builders/cyg1%20-%20libshogun). This might be done possibly in [another project](GSoC_2015_windows))

#### Related entrance issues:
 * [#2720](https://github.com/shogun-toolbox/shogun/issues/2720)
 * [#352](https://github.com/shogun-toolbox/shogun/issues/352)
 * ...

### Optional
The possible optional part of the project is to provide a series of videos or blog posts that show how easy one can install Shogun with all the work carried out during the project.

### Why this is cool
If you can get this to work, Shogun will finally be easy to install on any major platform. This will be a major boost for the whole project and its popularity. Again ***TOP PRIORITY***!

### Useful resources
* [CMake documentation](http://www.cmake.org/documentation/)
* [Windows installer](https://msdn.microsoft.com/en-us/library/cc185688(v=vs.85).aspx)
* [Homebrew](http://brew.sh/)
* [Macports](https://www.macports.org/)

Get back to the [main projects page](Google%20Summer%20of%20Code%202016%20Projects).