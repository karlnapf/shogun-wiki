# Releases
This document contains TODO lists for the next release.

## 4.2 [Takechi Hanpeita]
### Purpose:
 * Pre GSoC release, to make students get involved
 * Offers BSD license option
 * Last Shogun that does not require C++11 (which will be used for GSoC)

###TODO:
 * Make sure tests are green (include no warnings in libshogun and python modular)
 * BSD/GPL repository split
 * Fix remaining problems with meta example integration
 * See the [milestone](https://github.com/shogun-toolbox/shogun/milestones/Shogun%204.2.0%20-%20Takechi%20Hanpeita)

### Release text draft:
> Dear all,

> we are pleased to announce the 4.2 release of the Shogun Machine Learning Toolbox, in preparation of the coming Google Summer of Code 2016.

> This release's biggest change is the new BSD license option. You can now use (slightly slimmer version of) Shogun under a *non-viral* BSD3-style license. All of Shogun remains available under the GPL license. For details, see [here](TODO)

> The release also will be the last one which has C++11 as an *optional* requirement. From the next release on, this will be changed to a hard requirement.

> As usual, there are a number of improvements, mostly coming from our GSoC applicants. A full list and the download can be found at
> https://github.com/shogun-toolbox/shogun/releases/tag/shogun_4.2.0

> Heiko Strathmann, on behalf of the Shogun team

> About Shogun:
> http://www.shogun-toolbox.org

> Source code:
> https://github.com/shogun-toolbox

## 4.1 [DONE]
###Purpose:
 * Mostly contains Wu's new inference algorithms
 * Otherwise clean-up (drop migration, bug fixes)
 * Get back to speed.
 * Needed for pre GSoC 2016

###TODO:
 * Make sure tests are green
   * ~~we have a few serialization issues (http://buildbot.shogun-toolbox.org/builders/FC22%20-%20libshogun/builds/72/steps/test/logs/stdio) (Heiko)~~
   * ~~Fix typemaps for csharp (Viktor), [link](https://github.com/shogun-toolbox/shogun/issues/2425)~~
   * ~~R-modular tests fail~~
   * ~~Resolve all warnings for python modular build (Heiko)~~
 * ~~Make sure there are no fixable documentation warnings (Sergey, Wu)~~
 * Integrate new cookbook into main branch (not sure yet) (Sergey)
 * ~~Add new algorithms to NEWS (Heiko)~~
 * ~~Add clean-up patches to NEWS (Heiko)~~
 * Put new website online? (Kevin)
 * ~~Announce move to stack overflow for questions (Heiko)~~
 * ~~Write Release text (Heiko)~~

### Release text draft:
> Dear all,

> we are pleased to announce the 4.1.0 release of the Shogun Machine Learning Toolbox.

> This release features the work of the new Shogun-team member Wu Lin, who put a lot of work into Shogun's framework for large-scale variational inference for Gaussian Processes. A (very large) notebook explaining a lot of the methods can be found at http://www.shogun-toolbox.org/static/notebook/current/variational_classifier.html

> The release also features a computer-science feature by Esben Sörig, who designed a meta-language to write Shogun examples in, which are then automatically translated to all of Shogun's interface languages. Documentation can be found at https://github.com/shogun-toolbox/shogun/wiki/Example_Generation

> We also worked towards a smoother build process and did a number of internal efficiency improvements and clean-ups.

> A full list and the download can be found at
> https://github.com/shogun-toolbox/shogun/releases/tag/shogun_4.1.0

> On other news:
>  * We plan to start using Stack Overflow to reply to Shogun questions, rather than the mailing list. This will create a more documented set of Q&A. Github issues are used as before to report/solve problems. See http://stackoverflow.com/questions/tagged/shogun

>  * The Shogun foundation was recognised as a non-profit organisation by German tax law. This is an important step towards more sustainabl finances of the project.

> Heiko Strathmann, on behalf of the Shogun team

> About Shogun:
> http://www.shogun-toolbox.org

> Source code:
> https://github.com/shogun-toolbox