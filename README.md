JavaScript, the winning style
=============================

_NOTE_: This 'research' was originally published as a blog article at http://seravo.fi/2013/javascript-the-winning-style and then transformed into a public Git repo on suggestion by [Eric Elliott](http://ericleads.com/).


If your code is easy to read, there will be fewer bugs, any remaining bugs will be easier to debug and new coders will have a lower barrier to participate in your project. Everybody agrees that investing a bit of time to following an agreed-upon coding style is worth all the benefits it yields. Unlike Python and some other languages, JavaScript does not have an authoritative style guide. Instead there are several popular ones:

* [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
* [npm’s coding style](https://npmjs.org/doc/coding-style.html)
* [Felix’s Node.js Style Guide](http://nodeguide.com/style.html)
* [Idiomatic JavaScript](https://github.com/rwldrn/idiomatic.js/)
* [jQuery JavaScript Style Guide](http://contribute.jquery.org/style-guide/js/)
* [Douglas Crockford’s JavaScript coding style](http://javascript.crockford.com/code.html)

Then of course, there are also the default settings chosen in JavaScript syntax checkers JSLint and JSHint. The question is, what is the ultimate JavaScript style to rule them all? Let’s make a consensus based on these six style guides.

Indentation
-----------
Two spaces, more if needed to align multiline statements
```js
var a = 9,
    b = 6;

if (true) {
  doThings();
}
```

Spaces between arguments and expressions
----------------------------------------
Use sparingly like below
```js
project.MyClass = function(arg1, arg2) {
```

Line length
-----------
Max 80 characters

Semicolons
----------
Always use semicolons and don’t rely on implicit insertion

Comments
--------
[jsDoc](http://usejsdoc.org/) conventions

Quotes
------
Prefer `'` over `"`

Variable declarations
---------------------
Multiple in one go with line ending commas like below
```js
var foo = "",
    bar = "",
    quux;
```

Braces
------
Use opening brace on the same line
```js
function thisIsBlock() {
```
These also imply that braces should be used in all cases.

Globals
-------
Don’t use globals

Naming
======

Variables
---------
Start first word lowercase and after that all words start with uppercase letter (Camel case)
```js
var foo = "";
var fooName = "";
```

Constants
---------
Use uppercase with underscore
```js
var CONSTANT = 'VALUE';
var CONSTANT_NAME = 'VALUE';
```

Functions
---------
Start first word lowercase and after that all words start with uppercase letter (Camel case)

Prefer longer, descriptive function names.
```js
function veryLongOperationName
function short()..
```
Use vocabulary like is, set, get:
```js
function isReady()
function setName()
function getName()
```

Arrays
------
Use plural forms
```js
var documents = [];
```

Objects and classes
-------------------
Use camel case
```js
var thisIsObject = new Date();
```

Suggested .jshintrc file
========================
[JSHint](http://www.jshint.com/) is a JavaScript syntax and style checker you can use to alert about code style issues. It integrates well into to many commonly used editors and is a nice way to enforce a common style. See JS Hint documentation for all available options: http://www.jshint.com/docs/#options We have created a jshintrc file that follows the recommendations set above in this article. You can place it in the root folder of your project and rename it to '.jshintrc' and JSHint-aware code editors will notice it and follow it though all code in your project.

Automatically JSHint files before Git commit
If you want to make sure that all of your JS code stays compliant to the style defined in your .jshintrc, you can set the following contents to your .git/hooks/pre-commit file, which is then run each time you try to commit any new of modified files to the project:
```shell
#!/bin/bash
# Pre-commit Git hook to run JSHint on JavaScript files.
#
# If you absolutely must commit without testing,
# use: git commit --no-verify

filenames=($(git diff --cached --name-only HEAD))

which jshint &> /dev/null
if [ $? -ne 0 ];
then
  echo "error: jshint not found"
  echo "install with: sudo npm install -g jshint"
  exit 1
fi

which jscs &> /dev/null
if [ $? -ne 0 ];
then
  echo "error: jscs not found"
  echo "install with: sudo npm install -g jscs"
  exit 1
fi

for i in "${filenames[@]}"
do
  if [[ $i =~ \.js$ ]];
  then
    echo jshint $i
    jshint $i
    echo jscs $i
    jscs $i
    if [ $? -ne 0 ];
    then
      exit 1
    fi
  fi
done
```
Happy coding!

JSCS
====
[jscs](https://github.com/mdevils/node-jscs) is a JavaScript style checker we use to fill in the gaps of where jshint doesn't reach, such as curly brace placement, naming conventions, etc. We've created a jscs.json that follows this guide and it should be placed in the root of your project folder renamed to '.jscs.json'.



License
=======

Copyright (C) 2013 Seravo Oy

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


