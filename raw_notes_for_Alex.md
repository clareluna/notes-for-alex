 FOR THE DA!!!!

 JS DA day 2

https://www.youtube.com/playlist?list=PLZshpIn7Zx064IJAVqF5ieJk7dpzXI9hm

homework assignment on canvas

navigation of NPM

Bower, alternative to NPM on client side

semantic versioning (1.0.0) if first number changes everything breaks, second number means adding new things not deleting old code, third number is for patches to fix bugs

	if first number is 0 anything can change at any time!

npm init allows you to build package-JSON
	don’t worry about entry point unless creating a library - default to index.js

Test command: 

RFC- look it up

dependency vs development dependency
	dependency — minimum you need to run the code client side
	dev dependency — all the testing and structure for coder side

In index.js store library info and requirements

making a node file executable ( #! ) usr/bin/node 

exports == setting module.exports equal to empty object

should always set exports and module export to the same thing or only use one of the two

creating an entry point	
	globals=  module and require
		new __dirname —> will always be consistent for the relative path

command line argument
	stored in an array like object

Modifying package JSON


node package manager
	debugger statements in REPL will run debugger (node debug filename)

	use step only if you think there is a bug in library. Step will read through library elements one by one

instead use next, it will show you every function call that happens

your top three: cont(inue), next, step, repl (to step into repl)

works the same as breakpoints in console

npm test 

if getting weird errors remove node modules  
npm cache clear (remove linkage to possibly corrupted files)
npm install

else, there is an error in package JSON file

Keep it DRY - if using more than twice it gets its own file, if over 100 lines break it into more files

look at git-hub README pages for plugins — offers lots of info on testing	
	
JS DA day 3 - bitmap Transformer

binary data —
endianness —> refers to byte order

little endian - least sig byte stored first
big endian - most sig byte stored first

	hex value: DEADBEEF — in little endian EF stored first

		ex : EF, BE, AD, DE

majority of systems stored as little endian 

buffers stored in memory not on stack, majority of other variables are on stack

extra five bonus point : detect endianness of machine and use appropriate methods
	try without if else statements (only use one if statement)

buf.readUInt32LE(offset[, noAssert])

important for finding out how ‘full’ your stack is. stacks fill up quick with data on them

a byte is two hexadecimal values. a bit is one hex value

Look up byte values and understand how they get stored

BIT MAPS

https://en.wikipedia.org/wiki/BMP_file_format

cannot run a toString() on bitmap because it is binary

does not have mode of compression, so do not need to deal with compression algorithms

goal: to take in color bitmap and then transform to different color

for another 3 points — how to make it work with any image size (will need to deal with padding)

toString() takes two variables  where to start and where to read to 

what buf method for 4 bytes —> readUInt32LE(2)
	
in pallet data store RGBA data (each a single byte) all between 0-255, or 00-FF

pixel data stored as 2D array, Cartesian coordinates (0-100 for each row) 
--------------------
| . . . . . . . . . . .. . 0-100
|. . . . . . . . . . .. . 101 - 200
|. . . . . . . . . . .. . 201 -300
|. . . . . . . . . . .. . 301- 400
|. . . . . . . . . . .. . 401 -500

change pallet colors will change pixel data

for extra 5 bonus points - make transformer work for with and without pallet data

header is always 40bytes for BM bitmap

buf.readUInt32LE(18)
100 (width)
buf.readUInt32LE(22)
100 (height)

bit per pixel = 8 , not pallet version is 32

jpeg type of compression, for this assignment will not worry about it

don’t need to deal with image size, horizontal resolution

buf.readUInt32LE(46)
256 (number of colors)

buf.readUInt32LE(10) // the offset of the starting address where byte data starts
1078

buf.readUint32LE(2)
11078 //pallet data

JS DA Day 3

watch files: split gulp.task('default', ['jshint', 'test']); to each of the joshing and test to watch all files

building blocks of node

Buffers
Event Emitters
Streams
Binary data in node

Buffer- array like object 
inside node, there are files of the node modules, look for buffer.js in node 
	We are going to use these three most	
		utf8
		hex
		base64

	make buffer.js file, assign buf to new Buffer
		in terminal node debug buffer.js
			run but.toString(‘base64’)

convert bianary data to string

max hex decimal number is ff 265
can run forEach call() on buf

array methods do not return buffers they return arrays, will need to convert if used elsewhere

what uses buffers? —> everything, like...
	filesystem  

node globals —> process, module, __dirname
(look more up)

ENOENT - does not exist in terminal speak

Execution of event loop different than execution of javascript
	in event loop the event loop starts in chronological order 
JS will run through first, then event loop with run in second pass through

Event emitters - 
	similar to .on() .on(click)
	event emitter allows you to create and listen for you own events

see event_emitter_demo.js
	never .prototype on EventEmitter, do it on var statement. Else can lead to weird errors 
	See slide around 10:15am in lecture youtube
		util.library

process.nextTick(function() {
	fileEvents.emit(‘random’, ‘hello world from random’);
});


callbacks can come back in chunks, readFile comes back all as one

setTimeout(function() {function}, time) can change the firing order of console.logs

common to use event emitters to chain data chunks together

NODE STREAMS
	data can come in in chunks, so event emitters are your friends to compile chunks before running through

stream is an event emitter that has functions on top of it



WORK on making asychronous code, required for lab assignment

Tyler tidbit
if (err) throw err —> if (err) return err
	else it crashes the server, not great for hosting server

try/catch not a function —> will continue going until try is resolved. not great if no resolve

JS DA Day 4

Async testing



Object.keys (and then use array methods — its faster!)


Time complexity vs space complexity

Big O notation — time complexity happens with nested function inside another function

0(1) : constant time requirement
	accessing random elements in function

JS DA Day 5

REST - extraction over database. Consistent interface for interacting with web apps

	GET - retrieve resource 
	POST - create new resources
	PUT - update a resource - completely overwrite previous resource
	PATCH -  update a resource  only covering one field
	DELETE - removes resource

majority of what browser does is get request. Think googling something

server side rendering with express — look into on your own time

Full Client Side App
index.html
	loads in client.js

 ——————————> AJAX REST Requests
					Server ———————>
									    Database (Mongo)
						<————————				
					Server
		<——————
Client.js

Rest requests sent as resource/endpoint
Each request has a ‘request body’ in JSON
Everything sent between server and client is JSON files

In TCP get all request in orders you processed them UDP is broadcast so data is thrown and received randomly

TCP keeps signal open until you close it (socket). Once receives a response to close socket will close socket

in terminal one tab node tcpServer.js the other tab curl localhost:3000 should get the following:
GET / HTTP/1.1

User-Agent: curl/7.37.1

Host: localhost:3000

Accept: */*

 disconnected


HTTP command with GET 
user agent either curl or super agent
with curl have to disconnect with super agent has three second disconnect

If connecting to another computer the host will come in as their IP address instead of the localhost

curl and super agent are simple utilities, much more powerful and efficient web browser

NODE is capable of handling lots of small concurent events in server.js file. Callbacks

node is not great at lots of data processing (think for loops) node IS very good at IO

Using lib dir, node is very good at moving through events

check out http server debugger stuff again

status code 400 is error on client side


in URL will have name /greet/yourName
make server recongnise that you are going to/greet
then greet that name (JSON parse)

Other will be to return the time

JS DA Day 6

Superagent cli vs superagent - superagent cli is a command line interface wrapper, superagent is an API

done is the way to tell a test it is going to be Async

making a simple router

npm init to make package.j son

for making a new router homework make it in a way that will be easily accessible on npm

hardlinking- two files that point to the same chunk of the hard drive, if you delete one of them, it will delete both

dumb router
 
(req) —> look for function in routes [req.method][req.url] (req, res)

TravisCI is an continueous integration server
	jenkins 
free for open source projects

have a travis.yaml file
to find the type of yaml file you are looking for google type of stack you are building (node travis yaml)
	looks like this….
language: node_js
node_js:
  - "0.12"
  - "0.11"
  - "0.10"
  - "0.8"
  - "0.6"
  - "iojs"
  - "iojs-v1.0.4"
running your mocha test on travis ci servers. Good way of showing users what your tests are and that they are passing


homework will be to receive a post request, generate a json of that file name. and when they do a get request for that file name it will pipe back to the user

can use router, or raw js

JS DA Day 7

stacks and queues

lots of interview questions will be graph and tree problems

Abstract data types- interface to data structure
	
stack (lifo)- last in first out
	push, pop, (peek - lets you see what comes next)
		used for scoping, reverse, syntax checking and recession

Reverse an array using another array 

var arr 1 = [1,2,3];
var arr 2 = [];
if (arr1.length > 0){
	var i = arr1.pop()
	arr2.push(i)}
else{ 
	return arr2};


must use a push.bind.array in a this.push statement else it will try to bind to the constructor (since arrays are in effect just objects)

check for matching brackets in a string

var string = { fa la]  la}
var array = string.split(‘’).sort();

for(var i = 0; i< array.length; i++){
	for(var j = 1; j <array.length +1; j++){
		if( i === j){
			return true
		} else {return false}
	}
}

Queue — first in first out
	enqueue dequeue (sometimes hasNext)
		
write a constructor for a Queue that hides array 

function Queue {
	this.enqueue = array.push.bind(array);
	this.dequeue = array.shift.bind(array);// must be shift first in first out
	this.hasNext = function(){
		return !!(array.length)
};

Make dequeue 0(1)

dequeue removes the first in an array
function Queue {
	var arr = [1,2,3 ]
	var frontArray = 0

Express
some tutorials made for express 3. will need to be aware when reading tutorial

downside to express - routing is resource intensive (lots o memory)

express supports wildcards in route name
‘ * ‘ is a catch all. If you put it following a route, it will verify any route that matches the start before star to the proper route

useful to use debugger in express req/res blocks 
	will give query streams (req.query)	wiki it

BODY PARSER- allows you to pull in json data and save to req.body

middleware will allow for manipulation, the res.json res.send to end block	

will typically create a router that will be mounted onto app

if you mount a router before other uses, it will not affect lower uses, 

best option = create router, mount router into your path that will have its own scope to keep server clean

JS DA Day 9 (out day 8) these are the two most challenging days. If you want a challenge try implementing OLAF

making a middleware today . else passport is the standard

authentication and authorization today

Authentication system — Creating a user

(username/pwd) —> hash password (never store plain text password)

make JWT (JSON web token) == store user data send back token 

EAT tokens a JWT alternative that can be authenticated on server

Authentication system — existing user
send a basic HTTP authorization
set a header key: authorization
Authorization: 'Basic' base64encoded/username:password

HTTPS is a public/private key system. User and page have public keys that can only be read by specific user

free encryption coursera course (stanford) TLS and 2(dot)0 most common used encryption systems 

BCrypt - hashing version on blowfish encryption algorithm 

don’t write your own encryption. Use some other source, (node encryption or Bcyrpt)

hashing vs encryption
hashing is one directional
encryption can be written and decoded

Salted hash - when you add random data into password so that your hashed password is unique to you computer

will iterate through rounds of salting to generate random hash 

(rainbow table) - if they don’t contain random information per user you can track back the hash to user

initialization vector — encryption version of salt

first thing you need to do is create a user model that can both encrypt and store password 	

Will need to include a secret key library that makes a 32bit encryption code

four errors you could have 
user does not exist
password is not a match/ token present
no basic HTTP
database error

JS DA Day 10

overview of Auth

post username/password — get back token

signing Basic HTTP — get token

if you want to then POST, will need to include the token in header or body

Types of Errors
token does not exist
token can’t be decrypted
user does not exist
database errors

token will be most likely in the header, or if not, in the body

return res.error is needed in error checking, else it will keep going even if user or decryption not true

Be sure all initial decryption check is done on the server side

JS DA Day 11

Linked list slides

(pointer to next item)

value, next data features

Heroku app deployment
init git, create Procfile

Profile specifies commands your app needs to run
web: node server.js 

in package.json set engines = {‘node’ then node version}
	specifies which version on node you will be running

install foreman (npm -g install foreman)
 (np start) to start server
	it should start on their port rather than the one you specified
	in order to change this, create a (.env) file and specify (PORT=####)
		dont commit .env file— Contains information about app key data, external keys
	instead if you need to include external apis, make public .env that contains what those apis will be

be sure you push to github before pushing to heroku

to add to heroku (heroku apps:create)
	will generate its own app-nam unless specified 
	(heroku apps:create name)

to deploy app 
(git push heroku master)

to troubleshoot

(heroku ps)— see if web crashes and (heroku logs) -- will tell you why your server crashed

have to add mongodb to get server to run
	go to heroku.com dashboard, your app
ADD ADD-ONS
	MongoLab (heroku addons:create mongolab:sandbox)

	will need to put a credit card on file before this will work

BE SURE NEVER TO PUSH AWS KEYS TO GITHUB OR HEROKU>> thats how people steal your data and rack up credit card debt

(heroku config)

	setting a second config variable. 
	copy MONGOLAB_URI 

heroku config:set MONGOURL = to copied URI

Be sure to set an APP_SECRET
	secretkey

(npm -g install secretkey)

(nodenv rehash)
(secretkey)

(heroku config: set APP_SECRET=`secretkey`)

backticks kind of like piping in reverse
	else you could run
heroku config: set APP_SECRET=$(secretkey)

run heroku config

everything from /heroku_blahasd: = user
everything :blahasd@ (not including @) is password
(show collections)
(bd.users.find().pretty() )
	will show users

recommendation for app. staging and production
day1 - get code written
day 2 - don’t stress
day 3 - slim down or push to production, deploy
day 4 - create staging to try new feature
day 5- have production working, IF staging is working present that, else stay will simpler app

heroku only takes master branch, in order to take another branch

(git push heroku master:some_branch_name)
	can have detached head issues. be careful with this one

whiteboard question
distance between two variables in array
does not need to be in order
should be in On
to repeats in list
linked list format
head is just a value with next

JS DA Sept 28th

Angular Basics
	modern build practices
		controllers
		services
		directives

	Next week: Authentication (same as first half) build client 

	Last week: Ionic 

Final project : working with a front end team 

working on future projects: have a system of assigning issues and tasks to people
	

Build process for client side — web pack
	webpack will eliminate script tags is html, also eliminate globals and only run the code that you are working on

setting globals — anonymous function iffy
or set window.(function function function) to call code at start of window

javascript, everything goes into global name space

webpack with eliminate global name space unless you specify it

webpack
	must be in ./ blah format  no __dirname

node globals - module.exports, process, buffer, require, __dirname

webpack will only use module.exports, exports, require
	much slimmer than node, no fs or file structure

Look up in repl require, module process

break the browser sandbox — actually running commands off your computer rather than browser
zero day vulnerabilities — how hackers exploit 

app directory — everything front end (js, css, html) will use webpack here
build directory — compiled version of app (express static server)
		DONT EDIT CODE IN BUILD FOLDER — DONT COMMIT BUILD FOLDER

npm install —save gulp webpack-stream
gulp prefers webpack-stream npm package
	build the majority of webpack.config in gulp file

webpack will take in one file, and it will paste in every dependency into that document

webpack will statically serve all client side dependencies… the decendancies in package.son are the server dependencies

npm install angular —save-dev

standard naming convention if it starts with an underscore it is internally used not meant to be called outside the code

for debugging purposes need to get good at recognizing and debugging your own code. May see some webpack issues if bad require statement

lightning talks - 5 min short topic presentation topic of your choosing (i.e. differences between angular 1 and 2; how to upgrade to angular 2) — maybe on one of the REPL functions listed about

MV* model view controller framework — ANGULAR
model - takes care of data from REST server requests
view - what the client interacts with - presentation layer - html/css/functional js
controller - glues the model and view together

angular models are in javascript objects 

angular is a post processor, loads code after page loads

marcy sutton at substanial works on JS tools for accessability (for impaired)

for symantically precise html, find more than div tags, there is most likely a tag for what you are looking for in HTML5

two way data build 

<body data-ng-app>
<h1>{{greeting}}</h1> double curly brackets == execute as javascript
<input type="text" data-ng-model="greeting”> //greeting here is linked to greeting above through angular magic

everything you create is a child of root-scope (two way data binding)

ng-app means that it was built and maintained by angular

gulp watch task for homework have to restart if add new files

modify single resource API add static build

DONT USE ANGULAR AND jQUERY IN SAME APP



CSS REFRESH

Selectors (# , . , * ) ids, classes, all
css-tricks.com
flexboxin5.com
learnxinyminutes.com/docs/css
	flexbox - a less common bootstrap
		put flex-container on <main class=“flex-container”>
		so that your style.css 
			.flex-container{
				code:style
				code:style
				code:style
			 }

eliminates need for float so frequently

sizes: 2em (double size of current font)
	em is roughly 16px
	

if having issues with css, try putting boarders around it, it will give you an idea of how big


flexbox browser capability — can I use

JS DA Sept 29th

$scope(ing)   all scopes saved as objects

—all sub-objects of root scope
	mostly similar to prototypal inheritance 

{{}} == expression

scopes in angular controllers- when they get called create a new call

try to have one controller and multiple directives, more than one controller can have scope issues

the controller is not actually instantiated until the function in called, therefore it will ALWAYS have the same value…. think 1 and 1 vs 1 and 2 example

transclusion


Organization of apps
configuration
deprecation warning

Making a resource like $resources

$http uses $q uses promises 

.then will have two functions
	Success
	Failure

Similar to AJAX however its working reading on the Angularjs $q docs

has shortcuts $http.get, $http.post and the others

cross origin resource sharing (CORS errors) — don’t hardcode localhost:3000 into req

Download Emmet Sublime Plugin

XHR- AJAX request 

discover-devtools.codeschool.com DO IT

if using a show hide especially on a repeat in Angular use an if instead, will not load the whole form onto the DOM

JS DA Sept 30th

testing Angular

not easy to unit test angular
	but we will be using unit testing — hooray!

in browser testing
	have to do it on client side

build your own test harness for mocha/chai
	in browser

will use karma for test runner in Angular — will use Phantomjs - headless browser (browser without UI)
	gives command line reports on browser test

running test in terminal

test harness — example file in JS_DA
	important features, require all scripts in then <script> mocha.setup(‘bdd’) var expect = chai.expect 

then run tests

mocha.run();
</script>

karma not defaulted to work with webpack, will need a work around

jasmine — will be used instead of mocha/chai, works better with angular than mocha/chai

npm install karma karma-jasmine karma-phantomjs-launcher —save-dev

process: build —> throw into karma harness —> send results to terminal
BE SURE TO REMOVE BUNDLE FROM GIT COMMITS

Clare-Monahans-MacBook-Pro:test_harness_angular_0930 clare$ karma init

Which testing framework do you want to use ?
Press tab to list possible options. Enter to move to the next question.
> jasmine

Do you want to use Require.js ?
This will add Require.js plugin.
Press tab to list possible options. Enter to move to the next question.
> no

Do you want to capture any browsers automatically ?
Press tab to list possible options. Enter empty string to move to the next question.
> PhantomJS
> 

What is the location of your source and test files ?
You can use glob patterns, eg. "js/*.js" or "test/**/*Spec.js".
Enter empty string to move to the next question.
> 

Should any of the files included by the previous patterns be excluded ?
You can use glob patterns, eg. "**/*.swp".
Enter empty string to move to the next question.
> 

Do you want Karma to watch all the files and run the tests on change ?
Press tab to list possible options.
> no



do not want Karma watching because the gulp build is doing that for us, be sure to choose phantomJS since no UI

also, be sure to go into  karma.conig.js singleRun:true 

be sure to separate client side builds from webpack builds  (testing folder should have two directories for either of them)

gulp.task(‘servertests’ function() {
	return gulp.src(‘./test/api_test/**/*test.js)
		.pipe(mocha({reporter: ‘nayn’})
		.once(‘error’, function() {
			process.exit();
		}
		.once(‘end’, function() {
			if (this.seq.length === 1 && this.seq[0] === ‘server tests’
				process.exit();
		}.bind(this)
		//found a way to end the tests since cannot run both front and back end
	}

only wanted it to exit that specific gulp task

require server in test file

in karma.conf need to give a file to the bundle

npm install --save-dev angular-mocks

allows you to select which code you are testing (not angular!)

make client test in client dir
	require(__dirname + ‘./notes/

in troubleshooting, use debugger, repl it, 

if reading Angularjs.org look at view source to see actual code

pull in karma to gulpfile (require(‘karma’).Server

building with gulp first allows you to not have to run a webpack before each test change

instead you should be allowed to run gulp testfile in terminal

find way to test async UX stuff as well — do things before calling flushf 

DOWNLOAD NODEMON

also need to download node 0.12.10 for Ionic

npm install gulp-mocha —save-dev allows you to run tests with gulp 

look up glob- regX

JS DA Oct 1

TREES!

linked list, simple form of tree
—data structures composed of nodes, each node has zero or more nodes coming off them!

binary search tree

root —> node —> node —> leaf
  |   (siblings)
  L —> node —> leaf
		(child)

recursive data structure

—useful in parsing

DOM tree
FileSystems tree (root starts at ‘/‘) look up unix file system 

used a lot for searches

balanced search trees- having the same number of nodes to the left/right of root

tree nodes- holds values and references to child nodes (branches)

binary tree node- each node has at most two children 

create constructor that has binary tree node

var BinaryTreeNode = {
	this.value = value;
	this.left = null;
	this.right = null;
}

height of tree defined by distance from root to farthest away leaf

highest tree of n nodes, is n-1
shortest tree of n nodes is logn

depth first, visit nodes children first before siblings

assending or decending… going down to the left first vs right first

left children smaller than parents, right children larger that parents

BST interface = insert, delete, contains, max, min

Create a constructor

var BST() = {
	this.root = null;
}

//frequent job interview questions
BST.prototype.each = function(f, node) {
	node = (node === undefined) ? this.root : node;
	if(!node) return;
	
	this.each(node.left);
	f(node.value)
	this.each(node.right);
}

BST.prototype.contains = function(value, node) {
	node = (node === undefined) ? this.root: node;
	
	if(!node) return false
	if(node.value === value) return true;

	if(value<node.value) return this.contains(value, node.left);
	return this.contains(value, node.right);
}

write a function that takes a binary tree node return true if core sub tree is BST oth fals

	
JS DA Oct 5

lightning talks
	redis - fast database O(1) stored in memory, avoid persistence by saving to drive


Services - core concept of Angular

	when injecting more that 4 things into angular, it should be a code smell. Time to pull out dependancies into service

$scope is a service
$http is a service

example. in notes controller, the failure response is the same for all of the calls, could move out into own service

Services are singletons/factories (designs patterns books — read Addy Osmani Design Patterns )

Factory will be the most common service you make

services are set one time, great for storing globals since they are created one time and cashed at each instantiation 
	if its updated on multiple places, this is not for you… think about the time you use require()

goal for refactors. unit tests still pass while you change your code 
	code — test — refactor — test

testing services— easier than testing Angular

directives - controller, ng-if, edgy-app
	
ways to include directives — ECMA = 
Element- don’t use, it fucks up DOM
Class
coMment
Attribute

Class and Attribute are the most common use of directive inclusion 

directive must return object that must have at least a restrict field (that will have an ECMA)

directive vs service == if there is html content you could use elsewhere its a directive else its a single service 

three ways to pass something in to scope — in dummy_directives scope: {}
	(=) interpreted —think note in notes
	(&) if you are passing a function
	(@) literal sense of the variable

Look up template URLs .html file template

JS DA Oct 6

anything that is a global will end up on window.

Directives — template URL
	
move the greeting ng-model into a template folder that will get bundled into the static server

Transclusion
	ng-transclude

anything you put in transclude will execute as if it was controller level
	ex: will be looking for pane scope on controller not directive level

using a class vs attribute == if using css selectors, easier to use class 

transclusions will create their own scope. It updates the DOM but does not actually bind back to controller, just creates a (sub)scope 

use transclude with function to gain access to text block manipulation 

transclusion is at the heart of the directives we have been building
	will be able to make one element that can either edit OR create note


Function passing with context

using ‘=‘ will allow you to bind back to the controller, creates the note into the database

note: '=',  // will change outline scope

filters example only for desplay purposes. the database will still have the unaltered data


in directives directory

JS DA Oct 7	

Transculsion and Directives are places where you will utilize <div> tags to wrap the tag and make sure it doesn’t bind an incorrect scope

shadow DOM - the dom manipulation rendering  is a slow loading process, JS is extremely fast so are CSS and HTML, but relies on the DOM being built before it can load features
	the shodow DOM is a fake dom in the shadows of the actual dom, instead of loading directly to DOM, render to the shadow dom (headless browser) compare shadow dom to reg DOM to find the min number of changes you have to make to the real DOM to make them match

relation between relation and non relation database querying really strict on SQL

npm install —save-dev angular-route
npm install —save-dev angular-cookies

remember npm save is only for server side non testing dependancies 

will be using #for routes
to route user side data

will be dependency injecting routes into app level (more global that controller and directives)

Try to minimize what you add to app level since it can get busy, however routes should be there

hash is stored at window.location
anything in the browser past a hash is no longer server side, its redirected on Angular side
	google/search/clare/#Iam/an/interesting/human

		server: google/search/clare
		browser: #Iam/an/intersting/human

removing the data-ng-controller is ok because the router will already include it

JS DA Oct 8

Make snippets

<snippet>
<content><![CDATA[
snippet here add $1, up to 9 will put cursor in those places when you tab
]]></content>
<!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
Unblock this one<!-- <tabTrigger>hello</tabTrigger> -->
<!-- Optional: Set a scope to limit where the snippet will trigger -->
Unblock this one set to source.javascript<!-- <scope>source.python</scope> -->
</snippet>

save as name.sublime-snippet

also useful is command-p to do a fuzzy search for file, add :line# to go to that line


JS DA Oct 12

JWT encoding on the client side, Tyler is not a fan bc not encrypted well
	
Lightning talks
RegExp
Browerfy
CSRF -cross stream? r? fraud

Ionic- for prototyping
	includes CSS/JS/HTML
		AngularJS
		backend (Cordova or phone gap)
			turns it into native code 

setup includes webpack and build process
	emulating Android	
	running on a real life phone

BUILDING A FAKE FONE
android avd — to select your device to program on 
	Device: Galaxy Nexus and Nexus X 
	target: API Level 23
	CPU/ABI: ARM
	adding skin/cameras will slow down simulation. Use at own risk

then run android avd in term to access that ‘phony phone’

also downloaded ionic and cordova 
	to begin a template 
	Clare-Monahans-MacBook-Pro:JS_DA clare$ ionic start sea-d49-notes-ionic blank
	
bower.json — sass dependancies

ionic.project — similar to package.json (generates config.xml)

scss - contains all SASS for app —> where you will modify styling

www — where you spend all your time. has file names and framework 

Clare-Monahans-MacBook-Pro:controllers clare$ ionic platform add android 

Clare-Monahans-MacBook-Pro:controllers clare$ ionic build android 

npm install (to get all gulp dependancies)

npm install —save-dev webpack-stream

will be using this. instead of $scope in cordova bc angular scopes get messed up 
hioh

JS DA Oct 13


BE SURE .ENV files IN GITIGNORE

echo “platforms” >> .gitignore  (to move to gitignore)
dont commit build, plugins

Cross origin resource sharing (CORS) :)
	
lo - loopback (like localhost)

Clare-Monahans-MacBook-Pro:sea-d49-notes-ionic clare$ ifconfig

will give you the IPv4

to know what to put for something `os.networkInterfaces().something[0].address` pull up a node repl and write`require('os').networkInterfaces()` and find which one has a internal: false

fyi webpack-env can cause all kinds of terminal issues

JS DA Oct 14

remember

make hooks/before_build/

Clare-Monahans-MacBook-Pro:before_build clare$ chmod +x gulp_build.sh
after building the gulp_build.sh file

command line calls (must be one each call)
	ionic plugin add phonegap-plugin-push
	ionic add ngCordova
	ionic add ionic-service-core
	ionic add ionic-service-push
	ironic add angular-websocket

IF IT IS IN ALL CAPS — that means its a constant that is not changing throughout the app (SERVER_ADDRESS)

JS DA Oct 15

Structural programming language to learn next
	welcome to SICP 
	Haskel Lisp, Scala learn yourself
	Bash
	said/gawk
	Ruby/Python

Jade—
	Server side HTML rendering (sometimes)
		Hogan.js (twitter)
		EJS (ERB)
		JADE!
	preprocess syntax -SASS/LESS
	
white space delineated (white space matters)
	no closing tags
	make children by indentation

header
h1 Heading  ====

<header></header>
<h1>heading</h1>

vs

header
	h1 Heading ====

<header>
	<h1>Heading</h1>
</header>

don’t need to track closing tags

useful for making DRY static applications - extends acts as a module.exports
Dont use Angular with Jade === slows everything down




