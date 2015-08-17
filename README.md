# Chatterbox-Server

This assignment constitutes part II of your multi-sprint journey exploring
client-server architecture. In part I, you built the chatterbox client-side
app, and configured it to communicate with a remote Parse server that we had
built for you. Today, you'll rip out the Parse server, and replace it with
a local one you'll build using Node.js.

In this assignment, you'll use [Node.js](http://nodejs.org) to implement a
simple chat server. Users should be able to connect to your Node server with a
web browser, choose a username, send messages, and see the messages sent by all
the other users connected to the same server.

## What's in this repo

* `server/server/basic-server.js` is a very-well-documented bare-bones HTTP
  server. Its comments include instructions on how to run it.
* `server/server/request-handler.js` is a nearly-empty file where you'll do
  your work.
* `server/spec/` has the [Mocha](http://mochajs.org/)
  specs that you will use and expand upon in creating your server.

## Getting Started

You built your chatterbox-client implementation in different pairs, so your first
order of business should be deciding whose chatterbox-client code is the 
cleanest and easiest to understand. Once you've agreed, copy the code from 
that repo into this new repo to get started. 

You should try to use your own chatterbox-client code (or your pairs) for this 
sprint, but if your solution is severely lacking in some irreparable way, you 
can use the provided solution to chatterbox-client instead.

### Installing Node

## Node

Node is already installed on the workstations, but if you want to install it on
your personal computer, it's best to use a utility that allows you to run
specific versions easily. There are several out there, but the most
straightforward one is called "n".

- You will need `npm`, which comes with node to install `n`, so you can first
install node through `brew` so that you get `npm`, like so:

``` bash
brew install node
```

- Now, install node using [n](https://github.com/tj/n), like so:

``` bash
npm install -g n
n stable
```

- Override the `node` installed by `brew` with

``` bash
n stable
```

- Uninstall the version of `node` you installed with `brew` so
that only the `n` version remains:

``` bash
brew uninstall node
```

## Modules

Read this excellent article written by HR alumnus Cho Kim,
[Understanding Module.exports And Exports In Node.js](http://www.sitepoint.com/understanding-module-exports-exports-node-js/)
to learn about node's module system.

## Debugging Node

Use node-inspector. Refer to the [project readme](https://github.com/node-inspector/node-inspector)
to get set up.

## Refreshing changes with node servers

If you're running your node server, and then make changes to your server files,
you'll have to stop the server (ctrl + c) and then restart it (`node
my_server_file_name.js`). This gets tedious very quickly.

To avoid this, you should check out [nodemon](https://github.com/remy/nodemon).
It's a tool that will watch your server files and automatically refresh them so you
don't have to. Sweeeeet.

## About stubs

You'll notice some [stubs](http://en.wikipedia.org/wiki/Test_stub) in this
repo. When you're working from stubs, you should also know what class they're
stubbing out, and refer to the docs for that class.

Do not make use of stub properties that begin with underscores. As a
convention, when javascript devs prefix object properties with an underscore, it
usually means "you probably shouldn't directly manipulate this." In this case,
if you use those properties of the stubs, you'll find that they don't exist on
real request and response objects.

## Package Managers

In part I, you used bower to install and keep track of the tools your
client-side code requires. Today, you'll add another popular package manager to
the mix called **npm** to install and keep track of the tools your dev
environment and server-side code requires.

### npm

Instead of manually downloading all your server-side dependencies to a 'lib'
folder that you track with git, You'll use npm to install and manage
everything!

> npm (faux abbreviation for Node Package Modules) is the official package
> manager for Node.js. As of Node.js version 0.6.3, npm is bundled and
> installed automatically with the environment. npm runs through the command
> line.

> According to its author, "npm" is __not__ an abbreviation for "Node
> Package Modules" or "Node Package Manager". It is a recursive bacronymic
> abbreviation for "npm is not an acronym". (If it was "ninaa", then it would
> be an acronym, and thus incorrectly named.)

There are a few ways to use npm to manage packages:

### Local Installation

When you install a project dependency (like express) into your projects
'node-modules' folder it's called a 'local' install. Modules that are installed
locally must be used/imported via `require` statements in your js files.

``` bash
npm install --save underscore
```

### global installation

Some npm packages derive their usefulness through usage in a local shell
environment, such as _nodemon_. In these cases you will need to install the
package globally by utilizing the `-g` flag. You cannot `require` globally
installed packages.

``` bash
npm install -g nodemon
```

By default, libraries found in globally installed packages cannot be accessed
through `require` statements. In the case where you want to use a package that
has both a JavaScript library and a command line interface, it is best to
install the package both _globally_ and _locally_.

### package.json

There is one file in this repo that will control/affect the behavior of npm:
`package.json`, which defines our project's dependencies. Upon initially
cloning the repo, be sure to run `npm install` to install the necessary
packages as defined in your `package.json` file.

When installing a new dependency, you should use the `--save` flag, which
causes npm to automatically add that dependency to your `package.json` file.

## Basic requirements:

- Continue to use bower to install (and keep track of) all the client-side
  libraries you use as you work through this sprint.
- Use npm to install (and keep track of) all the server-side libraries you use
  as you work through this sprint.
- [ ] Learn how to use Node to start an HTTP server and how to connect to that
  server with a web browser. (Source code for a bare-bones HTTP server is
  included in the file `server/basic-server.js`.)
- [ ] Learn how to use export and require. Write a proper request handling
  function in the file `server/request-handler.js`. Use export to make this
  function available, and use require to import the function into
  `server/basic-server.js` and use it there.
- [ ] Make your Node server implement the URLs you used for your chat client
  (eg `/classes/messages`).
- [ ] Modify your chat-client code to connect to your Node server instead of
  connecting to Parse. (http://127.0.0.1:3000/ instead of
  https://api.parse.com/1/). Start the server and try out the client!
- [ ] Make all the Mocha tests pass.
    - Before running Mocha tests for your Node server, you must run `npm install`.
    - Run the tests using `npm test` from the main directory.
    - The tests in `server/spec/ServerSpec.js` expect the `handleRequest` function
      in `server/request-handler.js` to be defined.

##### A Note About Options Requests

- You should learn about [OPTIONS requests](http://zacstewart.com/2012/04/14/http-options-method.html).
  They are a type of request just like 'GET', or 'POST'. But these are
  automatically sent whenever there's a cross-domain request (which is
  often.) Think about options requests as a way for a site to 'check' if it's
  allowed to do what it's about to do. In this example, am I (the client)
  allowed to make this cross-domain request?' More generally, it's, 'what
  *options* are allowed to me for this resource?'

- __tl;dr__: You'll need to make sure you're handling options requests in your
  router, and sending back appropriate headers, or else ain't nothing gone work .


## Extra credit:

- [ ] Make your Node server serve up the html and js files for the chat client
  page at http://127.0.0.1:3000/. Run the client by visiting that URL in your
  browser instead of opening the file.
- [ ] Have the server store the message log in a file so that the messages are
  saved even after you stop and restart the node server.
- [ ] [Express.js](http://expressjs.com/) repackages Node.js' API into a clean
  and easy to use interface. Refactor your server to use Express and marvel at
  how much nicer your code looks now.
- [ ] Summarize the chain of events between basic-server's
  `http.createServer(...)` and the function call to `requestListener`.
  * Throughout your expedition, record your notes for later publication as a
    blog post.
  * Start from [Node's HTTP module](https://github.com/joyent/node/blob/master/lib/http.js).
    List/summarize the method calls that happen, skipping over boring steps
    when possible, and aiming for conceptual completeness and simplicity.
  * Things will get increasingly more "low-level" -- closer to bare networking
    concepts and system calls to non-javascript code. Make a judgement calls
    about when to skip onwards. Beeline for something complete, but very, very
    simple, and fill in more details later. Watch out for deep rabbit-holes.

## Relevant documentation

* [Node module system - how to export and require](http://nodejs.org/api/modules.html)
* [http Node module](http://nodejs.org/api/http.html)
* [Response docs](http://nodejs.org/api/http.html#http_class_http_serverresponse)
* [Request docs](http://nodejs.org/api/http.html#http_http_incomingmessage)
* [fs Node module](http://nodejs.org/api/fs.html)
* [Readable Stream](http://nodejs.org/api/stream.html#stream_readable_stream)
* [querystring Node module](http://nodejs.org/api/querystring.html)
* [Handling POST data in Node](http://blog.frankgrimm.net/2010/11/howto-access-http-message-body-post-data-in-node-js/)
* [HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
* [HTTP headers fields](http://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
* [Same Origin Policy and CORS](http://en.wikipedia.org/wiki/Same_origin_policy)
* [Mocha](http://visionmedia.github.io/mocha/)
* [How-to-handle-post-request-in-node-js](http://stackoverflow.com/questions/15427220/how-to-handle-post-request-in-node-js)
* [options requests](http://zacstewart.com/2012/04/14/http-options-method.html)

