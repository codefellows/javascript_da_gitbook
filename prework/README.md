# Prework
## Setup Your Computer
There are really only three components you'll need to be successful in the course
* A text editor
* Node
* MongoDB

### Initial Mac Setup
Make sure you have homebrew installed, follow the directions at the bottom of
this page: http://brew.sh/

Afterwards run `brew install mongodb` to install MongoDB. You will also need the
curl utility to install node run `brew install curl`.

### Initial Linux Setup
To install the latest version of MongDB on Ubuntu or any of it's derivatives follow
the directions found here: http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/
make sure you read all the way through the directions.

If you're using Manjaro or Arch just run `pacman -S mongodb`

### Node Install
**IF YOU ALREADY HAVE NODE INSTALLED READ THIS ANYWAY!!**
#### Out with the old
First type `which node && which npm` if you get anything other than a blank line you already have node installed and need to remove it. If you used the node installer from their website use these commands:
```
sudo rm -rf $(which node)
sudo rm -rf $(which npm)
sudo rm -rf ~/.node
sudo rm -rf ~/.npm
```
Now if you type `which node && which npm` you should have a blank line.

#### In with the new
These instructions will help you install the latest version of node in a way the prevents you from needing root to install
global packages. You will need curl, python v2.x a C compiler(gcc or clang) and make installed. These can be obtained through whatever package manager your operating system uses (homebrew on Mac, apt-get on Ubuntu, etc).
```
curl -O http://nodejs.org/dist/v0.10.35/node-v0.10.35.tar.gz
tar xvf node-v0.10.35.tar.gz
cd node-v0.10.35.tar.gz
./configure --prefix=$HOME/.node
make && make install
```
These commands will download the latest version of node (currently 0.10.35) configure it to install into a .node folder in your 
home directory and will then compile it from source. Next you need to tell your shell to look for the node command in $HOME/.node/bin
On Linux:
```
echo "export PATH=$HOME/.node/bin:$PATH >> ~/.bashrc
echo "export NODE_PATH=$HOME/.node/lib/node_modules" >> ~/.bashrc
source ~/.bashrc
```
On Mac:
```
echo "export PATH=$HOME/.node/bin:$PATH >> ~/.bash_profile
echo "export NODE_PATH=$HOME/.node/lib/node_modules" >> ~/.bash_profile
source ~/.bash_profile
```
If you now enter the command `node --version` you should see `v0.10.35`

### Text Editor
A text editor is a very personal thing, so let the flame wars being! 
I use nothing but vim but most people find GUI based text editors easier to work with. The two most popular options at Codefellows
are Atom and Sublime Text. Atom is still in the early stages of development so you will
run into the occasional bug but it has a great set of features while remaining intuitive.
Sublime Text is great but the free version will annoy you with popups until you give them
an absurd amount of money for a text editor. If you want to use something else make sure
to clear it with an instructor or T.A. first. You'll have to follow the installation instructions
found on the website of your editor of choice. Also, make sure to follow a tutorial for
your editor of choice, even if you think you already have it down.

## Learn Some Stuff 
### Javascript
There are plethora of options for learning Javascript online and a multitude of
different directions to go within the language (boom, college words). To prepare for the course, focus
your attention on the language fundamentals. I recommend two main resources
  1. *Eloquent Javascript*
The author of this book has made it available in its entirety for free online: http://eloquentjavascript.net/.
Get through the first ten chapters if you can but at the minimum tackle the first six
  2. *Javascript the Good Parts*
This is a must read book for any serious Javascript developer. Buy this book and read it twice,
then read it once more. Seriously, there's a lot of info in here.
  3. *You don't know JavaScript*
This contains a handful of in depth books about very specific Javascript subjects. The scopes & closures
and this & object prototypes books are especially helpful. All of the books are available free 
online in the form of a github repo or available through O'Reilly publishing in both ebook and
print format. https://github.com/getify/You-Dont-Know-JS

### Git
Make sure you know git, we have a git/unix workshop that will teach you everything
you need to know and it is require for the course. You should be able to fork a github
repo, make changes to that repo and send a pull request at the very minimum. The Treehouse
course on git is a good resource if you want to brush up on your git skills.

### Unix
You should feel comfortable in a Unix command line. In fact, you should feel as comfortable
if not more comfortable in the command than you do in a GUI. If you feel a little lost, check
out the Treehouse course, then make sure to get some practice. I like this series of challenges
for practice: http://overthewire.org/wargames/bandit/

## Profit
![underpants gnome](http://stoneapeyow.files.wordpress.com/2013/06/underpants-gnome.jpg?w=290)

## Get into Slack and Canvas
If you're enrolled in the class and you haven't received two email invitations, one for canvas and
one for slack, email your instructor.
