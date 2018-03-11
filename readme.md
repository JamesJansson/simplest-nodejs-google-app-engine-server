# Instructions for running this server
1) Install [NodeJS](https://nodejs.org/)
2) Download or clone this repository
3) Open the NodeJS Terminal. Run `npm install` to add the needed ExpressJS files into the node_modules folder
4) Run `node app.js`
5) Open [localhost:8080](http://localhost:8080/) in your browser. You should see "Hello, world!" displayed.

# How app.js works
~~~
'use strict';
~~~
Forces the app to enter [strict mode](https://www.w3schools.com/js/js_strict.asp) on this file, to throw silent errors, such as assigning values to undeclared variables. 

~~~
var express = require('express');
~~~
Requires the [ExpressJS](https://expressjs.com/) module. When this app was originally created, we used `npm install express --save` to add express to the project and put instructions into `package.json` telling npm how to install express when you run `npm install`.


~~~
var app = express();
~~~
Creates a new instance of ExpressJS called `app`.

~~~
app.get
~~~
Takes two arguments. Firstly, it takes a string which represents the route. In this case, we set it to `'/'` because we want this route to be displayed when a user goes to `http://localhost:8080/`. 

The second argument is the function that determines what to do when the browser goes to the route `'/'`. It takes two arguments:
* `req`: Which contains the information that comes from the request, such as parameters in the URL or data sent through a `POST` request, as well as other information ExpressJS collects about this request.
* `res`: Methods that determine how the response is sent back. 

In our function we have the following line:
~~~
res.status(200).send('Hello, world!');
~~~
This does two things. Firstly, it sets the status of the request. Here we've set it to 200, meaning everything is OK. There are other status codes, such as 404 which indicate 'Not found'. The second part is sending the data back. In this case, we're sending back plain text of "Hello, world!".

~~~
var server = app.listen(process.env.PORT || '8080' , function () {
    console.log('App listening on port %s', server.address().port);
});
~~~
Tells the server to listen either on `process.env.PORT ` if it is set (useful if you plan to upload it to a hosting environment that sets its own ports), or on 8080. Once that is done, it tells the user that the server is running and which port it is running on. 

# How to create this from scratch
1) [Create a new repository on GitHub](https://github.com/new).
2) Clone to your local computer.
3) Use NPM to create the package.json file. Navigate your terminal the the project folder, run the following and enter the details as instructed.
~~~
npm init
~~~
![Running npm init](/tutorial/img/npm-init.png)
4) Create `.gitignore` file, add the line `node_modules`
5) Run 
~~~ 
npm install express --save 
~~~
6) Create app.js file