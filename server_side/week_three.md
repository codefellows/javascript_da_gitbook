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
Don't store dem p4zzw3rdzzzzz
#### Storage Concerns
Security is difficult. It takes only a cursory at tech headlines to realize
that even the leaders in the tech sector have difficulty keeping their data
secure. The easiest way to keep your users personal information from getting
into the hands of those with less than good intentions is to not store it. This
is pretty impractical to create a modern web application, so the next best is
to make it so that it's impossible to read, ever. Third best is save non only
non important data. We're going to be use a combination of all of these to
keep track of our users and their authentication credentials. 
##### Hashing
Hashing is a way of creating encoded pieces of text that can never be decoded by
running it through a "hashing" algorithm. This differs from encyption which can 
be both encoded and decoded. Hashing has been used for a long time, primarily to 
store passwords. It has also been used more recently for creating 
"crypto currencies" and in git to create unique references to reference specific 
commits or branches. We are only going to store hashed passwords inside of our 
database. When a user attempts to authenticate we will hash the incoming 
password using the same algorithm and compare the result with the stored hashed
password.
##### Salting
The process of salting involves inject random or pseudorandom data into a hash.
This prevents ["rainbow table"](https://en.wikipedia.org/wiki/Rainbow_table)
based attacks. Which are essentially a large database of hashes for an alorithm
and the input that was used to generate those hashes. Using salt means that your
hashed passwords are unique to your server, even if a potential attacker gets a
dump of your user data, they won't be able to recover plain text passwords.
This may not matter to your website(since they managed to get a data dump) but 
it will keep that attacker from being able to use the same credentials on another
site. The easiest way to attack a website is through its users.
##### Bcrypt
[Bcrypt](https://en.wikipedia.org/wiki/Bcrypt) is a hashing algorithm that uses 
the [blowfish cypher](https://en.wikipedia.org/wiki/Blowfish_cipher). The process
is complex but it essentially uses the data you're encrypting as a key to encrypt
it with. So you can technically decrypt it but only if you already know the data
that is contained within the hash. At which point, there's no point in decrypting
it. 
#### Setting up the mongoose model
To be able to store user data we need to create a user model. It should contain
places for us to store the username and password in our database. This going to
placed in a sub object contained within the model. It should look something
like this:
```
var userSchema = mongoose.Schema({
  basic: {
    username: String,
    password: String
  }
});
```
#### Why a subobject
The resoning for a subobject is for security. While there is no way to 'unhash'
a password we still don't want to give away our auth information. This could
potentially allow a user to build a rainbow against our site by creating new
accounts with various passwords and GETing the user object with the resulting
hash. Having a subobject makes it easier to delete it out of the model before
 `res.send`ing it anywhere.
#### Adding methods to a Mongoose schema
Mongose schemas make it easy to add a method to our model. Essentially each
schema contains a `.methods` object that has key/value pairs where the value
is a function that can be called on the model. Inside those functions `this` will
refer to the model data. ex:
```
var someSchema = new mongoose.Schema({
  someVal: String
});
someSchema.methods.printSomeVal = function() {
  console.log('someVal is equal to ' + this.someVal);
};
module.exports = mongoose.model('someModel', someSchema);
```
We can then console.log the someVal with the added text by calling `printSomeVal()`
on an instance of the someModel model.
#### Using the bcrypt module
The bcrypt module is fairly easy to use. Like most of the built in modules in 
node the majority of the functions have async and sync versions. We'll be adding
methods to our User model. One to generate the initial hash and one to compare
an incoming password with the hash saved on disk. 
Hashing:
```
var bcrypt = require('brcypt'); //node.bcrypt.js

userSchema.methods.generateHash = function(password, callback) {
  bcrypt.hash(password, 8, function(err, hash) {
    if (err) return callback(err);
    callback(null, hash); 
  });
};
```
The 8 in the hash call signifies how man iterations of salt this hashing 
function will generate. The amount of time it takes to hash your password
grows considerably when the number is increased. 8 miliseconds for the hashing
function is considered "safe" as per [this stack overflow response](http://security.stackexchange.com/a/3993)
but that might be overkill or not enough for your particular application. There
is always a tradeoff in security between convenience and how secure a system is.
So it's something you'll have to play with. Make sure not to save the model
before the generateHash's callback function has been called.

The other method that needs to be written is the compare function. This takes
a password and compares it to the on stored on the model.

```
userSchema.methods.compareHash = function(password, callback) {
  bcrypt.compare(password, this.basic.password, function(err, res){
    if (err) return callback(err);
    callback(null, res); //res can be false
  });
};
```
An important detail to remember is that a password that does not match the
one in the database is not an error. It will simple have a res equal to false,
so you must remember to check for that case in your callback function.
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
# Assignment
This assignment is essentially a precursor to your 4th week project. Create a single
resource JSON REST API with a presistence layer and authentication. If you're feeling
ambitious create a web interface for this application using html and jQuery. Once
again this should include testing, a Gruntfile and package.json file. This should also
be deployed using Heroku or AWS and have travis.ci integrationdd authentication 
using BasicHTTP and Tokens to your single resource. Make sure you use the 
asynchronous version of the bcrypt hashing functions and provide validation to 
make all incoming emails are unique.

#### Rubric:
  * Unique Emails: 2pts
  * Async Bcrypt: 2pts
  * Testing: 2pts
  * Auth middleware: 4pts.
