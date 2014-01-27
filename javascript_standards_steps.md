Goal
----
To create a standard for all of our javascript that can be easily followed
and makes our code base easier to understand and work with.

The changes have to be done in a way that requires small changes to "grandfather"
our code base to a cleaner future, while making it easier for developers to follow
the standard than not to.

Overview
--------
* setup a system to check the *syntax* of code changes before they are committed
* setup a system to check the *style* of code changes before they are committed
* clean up current code to conform *closer* to new style

Tools
-----
* [JSHint](http://www.jshint.com/)
  * checks syntax
* [JSCS](https://github.com/mdevils/node-jscs)
  * checks style
* [JSDoc](http://usejsdoc.org/)
  * standards for comments
* some IDE / editors will have plugins that will make using these core tools easier

Steps toward a cleaner code base
--------------------------------
1. install JSHint and JSCS on all developer machines
2. setup pre-commit hook to run JSHint and JSCS
3. use script or editor to switch tabs -> 2 space intent
4. run JS Beautifier to clean all code *closer* to standards