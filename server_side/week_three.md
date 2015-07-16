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
### BasicHTTP using Passport
The basic http standard, passport as a middleware and how that middleware is generated.
Also go over some basic encryption and why we don't store passwords.
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
