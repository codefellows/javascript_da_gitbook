# Week 3: Express, MongoDB and Authentication
## Day 1
Wow, building a vanilla Node.js HTTP server was a pain in the ass, let's see
how siple it is to do with express.
### Express Basics
How to setup an express app and get it communicating with the HTTP module.
Pulling the port in through env variable.
### Middleware
Middleware execution order, how to write our own middleware, use of the next keyword.
### It's so damn easy!
Holy crap this is easy. Look how easy it is to pull in a variable from the URL.

#### Assignment
Re write your HTTP server with simple persistence using express and use a 
feature or pluggin of Express that was not covered in class.

##### Rubric:
  * Conversion to Express.js: 3pts
  * Testing 3pts
  * Express feature: 4pts

## Day 2
Adding persistence to express and testing
### MongoDB
Running mongodb and using the mongo console.
### Adding a MongoDB presistence layer
Draw the picture of the architecture we'll be creating.
### Using Mongoose
Schema definitions, routes and how to use find to get specific data.

#### Assignment
Create a single resource rest API with Express that's backed by Mongo. I'm 
leaving this pretty open to interpretation. I want you to write this from 
scratch, don't just copy and paste code from class or previous projects. Add a 
feature of Mongoose that we didn't use class, such as data validation.

##### Rubric
  * Use of Express: 3pts
  * Use of Mongo: 3pts
  * Tests: 2pts
  * Project Organization: 2pts

## Day 3
Time to start adding authentication.
### Authentication vs Authorization
Authentication: who you are
Authorization: what you're allowed to do
### User Creation and User Data Storage
Don't store dem passwerds
### BasicHTTP Using Passport
The basic http standard, passport as a middleware and how that middleware is 
generated. Also go over some basic encryption and why we don't store passwords.

Passport uses what it calls "strategies" that are semi user defined, in order
to create a middle ware that can placed on any route that needs Authentication.
For instance, in our application we'll be using a BasicHTTP strategy in order
to determine if a user is who they say they are. This strategy uses a base64 
encoded string in the form of `'username:password'` that get sets in a request
header. The header would look something like this:
```
headers: {
  'Authorization': 'Basic base64 encoded string'
};
```
Note that this header is named 'Authorization' but it's actually used primarily for
Authentication. This data should always be sent over an HTTPS connection, 
otherwise it's trivial for an attacker to get your plain text password out of
the request. You can read more about the BasicHTTP standard in [rfc 2617](https://tools.ietf.org/html/rfc2617)

What the passport Strategy provides is a way to read and verify this header.
Passport also provides methods for workign with OAuth, Digest, and a variety of
other industry standard Authentication methods. Which is why we're using it, 
instead of just creating our own middleware. Once passport has pulled the data
out of the header it needs to know what to do with it. In the definition of the
strategy you have to determine what needs to be done with the username/password
that has been received. There are three different ways that the authentication
process can fail (four if you count database failure), if the Authentication 
hasn't failed, it has succeded and we can move on to the next piece of middleware. 
The three different failure are:
  1.  An invalid Authorization header or no header (passport takes care of this
for use)
  2.  There is no user corresponding to the username
  3.  The password does not match the one in the database

Passport strategies take the form a function passed into a new Strategy object.
This function will contain a series of parameters based on the type of authentication
used. In our case, it will be a username and a password. If it was OAuth, it would
be an OAuth token. All strategies will have a last parameter of `done` or `next`
that will be a callback passed to your strategy by passport. This is a Node style
callback. So, if you call with just a single parameter, that parameter becomes
an error. If you call it with the first param equal to `null` the second parameter
becomes the object that passport will set to req.user for subsequent pieces of
middleware. For example:
```
done('no such user'); //sends back a 401
done(null, someUser); //sets req.user to the someUser var and calls next();
```
You can read more about setting up the passport Basic strategy in their
[docs](http://passportjs.org/docs/basic-digest)

### Creating a token and sending it back after BasicHTTP Auth
Authenticate with basic http, generate a token and use that token for subsequent
requests. Not only confirms came from our server but can easily be expired.
### Using that Token to Authenticate
Sending the token back and the creation of the eat_auth middleware. Pulling the
token from the body or the header depending on which exists.
### Basic Security Concerns
HTTPS, the intarwebs and what data should be sent back to the user, also logging.
# Assignment
This assignment is essentially a precursor to your 4th week project. Create a single
resource JSON REST API with a presistence layer and authentication. If you're feeling
ambitious create a web interface for this application using html and jQuery. Once
again this should include testing, a Gruntfile and package.json file. This should also
be deployed using Heroku or AWS and have travis.ci integrationdd authentication using BasicHTTP and Tokens to your single resource. Make sure you use the asynchronous version of the bcrypt hashing functions and provide validation to make all incoming emails are unique.

#### Rubric:
  * Unique Emails: 2pts
  * Async Bcrypt: 2pts
  * Testing: 2pts
  * Auth middleware: 4pts.
