# Week 2: Async Patterns, REST, Vanilla Node Servers
## Day 1
Managing asynchronous code proves problematic for many. Today demontrates
several methods for manipulating data in an asynchronous manner.
### Callbacks
Not only how to pass a callback to a function but how to write a function
that takes a callback and calls that callback back.
### Promises
Using a library like Q or Blackbird.
### Event Emitter Promises 
Creating a promise like structure using Event Emitters and general async handling
with events.
#### Assignment
For this assignment you'll need to demonstrate three different ways of 
handling async code. First, using vanilla javascript. Write a modular function
that takes a call back as an argument, then call an fs read and call that
callback when when the read has succeeded after converting the buffer to an 
all uppercase string string. Your final product should be able to be called 
like this:
```
var myRead = require('myread');
myRead('./filename.awesome', function(err, data) {
  if (err) throw err;
  console.log(data);
});
```
Next, do the same thing using the q or blackbird promise library.
Last, do the same thing using an event emitter.

##### Rubric:
  * callbacks: 3pts
  * promise: 3pts
  * EventEmitter: 4pts

For a bonus point, write tests for each of these methods.

## Day 2
The precursor to building HTTP servers, specifically REST APIs.
### REST
Actions and verbs, resources and naming of URIs.
GET
POST
PUT
PATCH
DELETE
### ChaiHTTP
How to test an API using ChaiHTTP. Superagent underneath and using superagent-cli.
### Async Testing
Getting things done()
### Intro to Basic HTTP servers
Handling of super basic get requests. Also a TCP server that can demonstrate
what an HTTP request looks like (what is sent over the TCP/IP protocols.)

#### Assignment
For this assignment you should write an http server in vanilla node that 
responds to several different routes.

The server should respond to a request to /time that will send back the current 
time of the server.

It should also respond to a get request to /greet/name where name is any single 
word string. It should send back a string that greets that name.

It should also have a separate post request to /greet that takes the name in 
JSON format.

There should be tests using chaiHTTP for both routes, as well as a 
Gruntfile/package.json

##### Rubric:
  * Tests: 4pts
  * Routes: 4pts
  * Organization and Gruntfile/package.json 2pts
## Day 3
First complete Web server.
### Full REST Server in Vanilla Node
Demonstration of switching multiple request types and url handling.
### Beginnings of a Framework
Creating an object based routing system, essentially a precursor to a framework.
# Assignment
s assignment, write an http server that will act as a simple data store. It 
should respond to GET/POST/PUT/PATCH/DELETE requests for a single resource of 
your choosing, feel free to use express. The data coming in from a post request 
should be saved to a json file in a data folder in your repository, do not 
commit your data folder to git. For example if a request is sent to /notes with 
a body of {noteBody: 'hello world'} the json data in the body should be stored 
in it's own json file. You can pick a naming scheme for the file but I would 
recommend using the number of files that you have received so far. Submit as a 
pull request to your own repository.

##### Rubric:
  * Handles REST requests: 3pts
  * JSON storage: 3pts 
  * Tests: 2pts
  * Project Organization and Development Files: 2pts

## Day 4
### Stacks and Queueus in Javascript
#### Data Hiding with Javascript
