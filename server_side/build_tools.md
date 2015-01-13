# Basic Build Tools
Coding professional Javascript doesn't mean inventing everything from scratch.
An important part of creating Javascript projects is using peices of software
that have been created by someone else. In this class we'll be using a series
of build tools as well as the node package ecosystem npm.
## Node Package Manager
Node Package Manager or NPM is primary source of Node.js modules and libraries.
Their website https://npmjs.com contains a lot of good docs as well as information
on all the packages available through npm. We'll be accessing npm through their
command line interface that comes with node.
## package.json
A package.json file is all the meta data for a package that's hosted on npm. It
contains not only information on to install the package but also has information
like who created the package, what license it uses and scripts to run everything
from automated testing to starting a server.
## Grunt
Grunt is going to be our primary build tool. It essentially describes all the
tasks that we mgiht want to accomplish on a development machine. This could be
anything from running tests, to building a production version of our code, to
seeding database. It's probably most comparable to a Makefile from c/c++.
