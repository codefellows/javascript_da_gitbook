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
## Day 3
First complete Web server.
### Full REST Server in Vanilla Node
Demonstration of switching multiple request types and url handling.
### Beginnings of a Framework
Creating an object based routing system, essentially a precursor to a framework.
# Assignment
For this assignment you will be building a basic server side REST framework. 
It should essentially be a series of functions that help you build a server
side REST framework. This assignment is intentionally open ended but here are some
concerns to keep in mind:
  * Your framework should favor asynchronous over syncronous code
  * It should probably use callbacks or some other form of async management
  * It should make it easier to process the different REST actions for various routes
    * GET
    * POST
    * PUT
    * PATCH
    * DELETE 
Your framework should have testing and the number one thing to remember is don't
over think it. Keep your framework simple and concise. If you're feeling ambitious
place it on npm. 
