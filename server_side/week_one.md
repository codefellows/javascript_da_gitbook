# Week One: Node Development Tools and Vanilla Node
## Day 1 
[Screencap from D37](https://www.youtube.com/watch?v=raocBJXEsrc&list=PLZshpIn7Zx07vD1qmuGPztQw4Eluye-Ah)
### Modular Patterns in Node
Node.js uses a version of the [Common.js modular pattern](http://wiki.commonjs.org/wiki/CommonJS) it adheres to most
of the Common.js spec but deviates where it doesn't make sense in the context of Node. Node.js only has a handful of
global variables and any user created variables will not be set to the global context. You can think of every 
Node.js file as being wrapped in an [iife](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression), with
some tools to expose variables, functions or objects to other files.

There are two Node globals that allow us to transfer data between files, `require` and `module`.
`require` is what gets pulled into a file and `module`, specifically `module.exports` determines
what gets sent to the `require` statement. Here's an example:
```javascript
//greet.js
module.exports = function() {
  return 'hello world';
}
```

```javascript
//hello.js
var greet = require('./greet.js');
console.log(greet()); //hello world
```

In this example greet.js exports a function that gets required into hello.js and saved into the variable greet.
When the greet function is called it returns 'hello world' which is then output to the screen using console.log.
### Mocha/Chai and Testing
Testing is a process that allows developers to be more convinced that their code is working correctly. It's an
important piece of writing code because testing by hand gets old quick. For testing Node.js we'll be using a 
combination of two libraries [mocha.js](http://mochajs.org/) and [chai](http://chaijs.com/). Mocha provides the
framework, while chai provides the actual test statements. The two combined read relatively close to spoken language.
Let's write a test for our greet function. This file should live in a new directory called `test` within the root of
the repository that contains `greet.js` and `hello.js`. You will also have to run `npm install -g mocha` and `npm install chai`.
```javascript
//test/greet_test.js
var greet = require('../greet');
var expect = require('chai').expect;

describe('greet', function() {
  it('should greet when called', function() {
    expect(greet()).to.eql('hello world');
  });
})
```

This is the basic setup for a mocha/chai test. First we need access to the chai expect library. You'll notice
that this doesn't use a relative path. That is because chai was installed using npm, which will be covered on day 2.
Each piece of Mocha takes a human readable string and a function. The string describes what's going on in the function.
The describe block should contain all the tests related to a specific library or file. Hence, we have a describe block
for `greet`. Each it block should contain a single test. A good rule of thumb (until we get to working with APIs) is one
expect statement per it block. In this case we're just confirming that the greet function returns 'hello world'. To run
the tests type `mocha` from the root of your repository. Mocha automagically will find the test folder and run any tests 
contained within.

#### Assignment
This assignment will have you create a simple Javascript object that will be 
exported using the Node modular pattern we went over in class.

Your object should have a function named 'greet' that takes a name as a 
parameter and returns the string 'hello ' + name 

You should have at least one test that verifies the output of the function.

Your submission should be a link to a pull request to your own repository.

Bonus:
For an extra point, create a command line utility that will be run using node 
greet.js 'some name' and will pass the input contained in that argument to the 
greet function and output the result to the screen.

For a second bonus point, write a test that makes sure that the arguments are 
being processed.

 

##### Rubric:
  * Proper Styling: 2pts
  * Proper Submission: 2pts
  * Mocha/Chai Test: 3pts
  * Use of Modular Pattern/design of greet object/function: 3pts 

## Day 2
### Npm
[npm](https://www.npmjs.com/) is the ecosystem that really makes Node.js worth 
working in. It gives a developer
access to hundreds of thousands of libraries built on top of Node. Every 
package you install with the command `npm install`
gets saved to a `node_modules` directory created wherever the command is run.
 *Make sure to add this directory to your .gitignore*.
### Package.json

[Screencap from D37](https://www.youtube.com/watch?v=dWly4ZcMwp0&list=PLZshpIn7Zx07vD1qmuGPztQw4Eluye-Ah)

`package.json` is a file that contains all of the meta data relevant to your 
project or library in an npm context. This
could be a list of dependencies, author information, version information, etc. 
Every package on npm and most of your 
projects will contain one of these files. To be guided through the process run 
`npm init` from the root of your repo.
Pay special attention to the name, version number and description. Make sure 
to read up on [semantic versioning](http://semver.org/)
To add a dependency and install it use the command `npm install --save` to add 
dev dependency use `npm install --save-dev`. 
Dependencies should consist of only the minimum packages needed to run your 
server (in the case of web development) or your library.
DevDependencies will be everything else, including packages needed for the 
build process and testing.
### Grunt
[Screencap from D37](https://www.youtube.com/watch?v=42jIeCan7L8&list=PLZshpIn7Zx07vD1qmuGPztQw4Eluye-Ah)

[Grunt](http://gruntjs.com/) is a build used to keep programmers consistent on 
the commands they are running from the command line
as well as simplifying the commands needed to complete a task. To install grunt 
two pieces are needed, first the grunt command which
can be obtained via the `grunt-cli` npm package using the command 
`npm install --save-dev grunt-cli`. Next, the `grunt` package provides
framework to create something that grunt-cli can understand: 
`npm install --save-dev grunt`. Last we'll get the grunt-contrib-jshint and 
grunt-simplemocha packages, to lint our code and test it, respectively. 
`npm install --save-dev grunt-contrib-jshint grunt-simplemocha`.
To make something that grunt can read create a file called `Gruntfile.js` 
in the root of your repository which should looks like this:
```javascript
//Gruntfile.js
module.exports = function(grunt) {
  grunt.loadNpmTasks('grunt-contrib-jshint');
  grunt.loadNpmTasks('grunt-simplemocha');

  grunt.initConfig({
    jshint: {
      all: {
        options: {
          node: true,
          globals: {
            describe: true,
            it: true
          }
        }
        src: ['**/*.js']
      }
    },

    simplemocha: {
      all: {
        src: ['test/**/*test.js'] 
      } 
    }
  });

  grunt.registerTask('test', ['jshint', 'simplemocha']);
  grunt.registerTask('default', ['test']);
};
```
`grunt.loadNpmTasks` will load the grunt modules that we installed using npm. 
`grunt.initConfig` takes
an object that describes the options used for these modules, each conisisting 
of a main task such as `jshint` and
subtask such as `all`. Consult the docs for each module on what exactly should 
go in them. Each task has to have at least
one subtask. This is part of how grunt is designed. Last, there are custom tasks 
that can be registered. Essentially these are a way of
running multiple tasks with a single command. The first parameter is the string 
you want to be able to pass to the `grunt command`, followed
by an array of tasks you want to run when someone types that command. For 
instance with this Gruntfile when you type `grunt test` it first
run jshint then simplemocha. `'default'` is a special task name that runs when 
you just type `grunt` by itself.

##### Assignment
For this assignment you will add a gruntfile and a package.json file to your 
previous assignment.

The package.json file should include all the dependencies and dev devpendencies 
for the project.

The Gruntfile should contain a task to run the mocha/chai test as well as run 
jshint on all of your code. This should include your tests and your Gruntfile.

Submit as a pull request to your own repo that contains just the code for this 
assignment(Gruntfile, package.json and jshint config file if applicable).

Bonus:
For an extra point, set up a watch task that reruns your tests/jshint on changes 
to any of your files (minus package.json)

For another bonus point move the jshint options (node and globals) into a 
jshintrc file that you can transfer between projects.

##### Rubric:
  * Correct Submission: 2pts
  * Passes Jshint: 2Pts
  * Package.json: 3pts
  * Gruntfile: 3pts

## Day 3
### Buffers
[Screencap from D37](https://www.youtube.com/watch?v=yMdGMOyKeWY&index=6&list=PLZshpIn7Zx07vD1qmuGPztQw4Eluye-Ah)

[Buffers](https://nodejs.org/api/buffer.html) contain in memory binary data for 
Node.js. When you work with files in Node, you work with Buffers. To create a new
buffer simply use the buffer constructor. `var myBuf = new Buffer()` you can 
pass strings into the Buffer constructor function
that then get saved as binary data. The default encoded is utf-8. You can get 
then get strings of different encodings using the
`toString` method. For instance to get a base64 encoding use 
`myBuf.toString('base64')`. Buffers can also be accessed liek an array using
square brackets to get the hex values of a byte, more on this later.
### Event Emitters
[Screencap from D37](https://www.youtube.com/watch?v=PlVMirtsHbU&index=7&list=PLZshpIn7Zx07vD1qmuGPztQw4Eluye-Ah)

[EventEmitters](https://nodejs.org/api/events.html) are a way to do event based 
programming in Node.js. This covers not only a series
of built-in events but custom events as well. Usuall the EventEmitter will be 
"inherited" into aother constructor. Here is the
standard pattern for that:
```javascript
var inherits = require('util').inherits;
var EventEmitter = require('events').EventEmitter;
var MyEventedConstruct = function() {};

inherits(MyEventedConstruct, EventEmitter);

var emitter = new MyEventedConstruct();
emitter.on('myCustomEvent', function(data) {
  console.log(data);
});

emitter.emit('myCustomEvent', 'here is some data');
```
After we have an EventEmitter constructor we can both catch events with the 
`.on` function and emit events with
the `.emit()` function.
### Streams
[Streams](https://nodejs.org/api/stream.html) are essentially combination of an 
event emitter and a buffer. Rather than trying
to explain how they work I'm just going to point you to the great resource 
[The Stream Handbook](https://github.com/substack/stream-handbook).
### Manipulation of Binary Data
[Screencap from D37](https://www.youtube.com/watch?v=miH9dLr2CaA&index=8&list=PLZshpIn7Zx07vD1qmuGPztQw4Eluye-Ah)

Going to expand on this but essentially being able to use `readUInt16LE` and 
`readUInt32LE` in order to work with the 
[bitmap spec](https://en.wikipedia.org/wiki/BMP_file_format).

#### Assignment
For this assignment you will be building a Bitmap reader and transformer. It 
will read a Bitmap in from disk, run one or more color transforms on the bitmap 
and then write it out to a new file. This project will require the use of node 
buffers in order to manipulate binary data. Your project should include tests, 
as well as a Gruntfile and package.json file. Make sure to run all your code 
through jshint and jscs. The process will look something like this:
1. open file using fs and read it into a buffer
2. convert buffer into a Javascript Object
3. Run a transform on that Javascript Object.
4. Turn the transformed object back into a buffer.
5. Write that buffer to a new file.

You can also just directly manipulate the buffer.

The wikipedia article found here (Links to an external site.) describes the byte 
specification of a "windows bitmap file." We'll be working the simplest version, 
meaning no compression. Your project should be able to take a transform as a 
callback that will be run once the bitmap file has been read into a buffer. 
Your project should include at least one transform. This is a difficult 
assignment so make sure to come to me with questions early. Ideas for easy transformations:
  * invert the colors (essentially subtract every color value from the max color value which is 255),
  * Grayscale the colors, multiply each color value by a constant, just make sure your values don't go over 255.
  * (red|green|blue)scale the colors, same as above but only multiply one of the colors.

Submit a url with the final project, no need for a pull request.

##### Rubric:
  * Tests: 3pts
  * Gruntfile/package.json 2pts
  * Read Bitmap Meta Data 5pts
  * Successfully Apply Transform 5pts
  * Project Design 5pts

## Day 4
### Data Structures and Algorithms 1: Javascript Arrays and Objects
# Assignment
For the first major assignment you will be creating a bitmap transformer. You program
will read in a bitmap file into a buffer, run a color transform on that buffer and then
write it out to disk. Your final repository should include testing, a Gruntfile and a
package.json file.
