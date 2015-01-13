# Introduction To Testing
Testing falls in the category of things that distinguish good devs from
devs that are not that good. I bet you were expecting an awesome metaphor
but I just don't have that much creativity right now. It's like the difference
between a bycicle and a fish or something. Anyway, testing. We're going to be
using three larger libraries and a few smaller ones to test our server side code.
However, before we get into that let's talk about why we want to test. The case
for testing is prbably best illustrated by the classic story of the octopus and
the grasshopper.

All summer long the grasshopper developed new features on his enterprise Java
server. While the octopus added no new features and did nothing but write tests.
Then the winter came and with it a new version of Java that depricated a lot of
previously used features of the language. The grasshopper had no idea which pieces
of code work and which didn't and immediately died of an aneurysm or something.
While the octopus easily found the broken the pieces of code using unit tests,
also he got a racecar.

But don't take my word for it, [listen to Mr. T](http://blog.codinghorror.com/i-pity-the-fool-who-doesnt-write-unit-tests/).
The three testing tools that we will be making the most use out of in this course
are Mocha, Chai and Sinon.
## Mocha
Mocha contains the actual test runner. It works both on the server side and in
browser and was created by T.J. Hallowaychuck whose praises you will hear me
sing repeatedly throughout the course. On the server side we will need 
mocha installed globally to be able to run tests. `npm install -g mocha` but
it will not actually be saved as a dependency of our project. Mocha gives
us the access to a series of test structures that let us better organize our
tests. The first of these structures is the describe block. which looks
something like this:
```javascript
describe("my first test", function() {
  // test code goes in here
});
```
The describe blocks are ways to break our tests into groups. Every mocha test
should have at least one describe block. It's really a function that takes
two parameters. The first is string describing what your test is designed to test,
the second is a function that contains the actual test code. 
