# Week 1: Browserify and Angular.js
## Day 1
In front end web development there previously was no good way to manage
resources. Javascript code was frist put only in inline script tags, then in one
gigantic file(slowly being built up from a small file), then in a series of
files managed by script tags. All of these suck. Managing a series of javascript
files is still frequently done in a series of script tags. This quickly becomes
a pain. There are two different places that you have to worry about your code.
First in the actual javascript, then in the html. Dependencies quickly become
confused and there's easy way to keep variables out of the global context.
Thankfully there are now many modern build tools that make the process easier
and more sane.
### Webpack and Build Process
Webpack allows you to use common.js style dependency management in the browser.
It gives access to the usual require and module.exports statements as well as
supports advanced features like lazy loading and it allows you to use npm 
packages that have a front end component. It's relative simple to setup
with gulp. Just run `npm install gulp-webpack --save-dev` and add a task that 
looks like this:
```
var gulp = require('gulp');
var webpack = require('gulp-webpack');

gulp.task('webpack', function() {
  return gulp.src('src/entry.js')
    .pipe(webpack({
      output: {
        filename: 'bundle.js' 
      }
    }))
    .pipe(gulp.dest('build/'));
});
```
This task will take a single entry point, in this case `src/entry.js` which will
require in all of the other required javascript code. It then will bundle it
up with all the dependencies and output it to build/bundle.js.  
### Basic Angular.js
MVC, basic controllers and using directives. Two way data bindings and communication
between controller and view. Angular modules and how they work.
### Communicating with the server
$http service and basic CRUD (if there's time)
## Day 2
Setting up a test framework and mocking.
### Basic Angular Testing
Mocking out the controller constructor and $httpBackend. How angular actually
uses these pieces.
### Services
Moving pieces of the notes controller into a service. Services as singletons/
factories.
## Day 3
The other side of modular code, and more testing.
### Testing Services
It's super easy, just inject it.
### Directives
Code reuse that uses a view. Talk about EMAC style of directives, isolate scope
and data sharing.
