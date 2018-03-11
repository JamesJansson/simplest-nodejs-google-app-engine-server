# Instructions for running this server locally
1) Install [NodeJS](https://nodejs.org/)
2) Download or clone this repository
3) Open the NodeJS Terminal. Run `npm install` to add the needed ExpressJS files into the node_modules folder
4) Run `node app.js`
5) Open [localhost:8080](http://localhost:8080/) in your browser. You should see "Hello, world!" displayed. You are now running a local server. 

# Instructions for running this server on Google App Engine
After doing the above:

6) [Set up Google Cloud Platform](https://cloud.google.com/)

7) Create a new project
![Create a project](/tutorial/img/gcp12.png)

8) Name the project

![Name the project](/tutorial/img/gcp3.png)

9) Make sure the project is selected
![Select the project](/tutorial/img/gcp4.png)

10) Install the [Google Cloud SDK](https://cloud.google.com/sdk/)

11) Run the following command 
~~~
gcloud init
~~~
Create a new configuration. It can have any name. 

12) Log in to your Google account.

13) Select the project that you create above.

14) Select the region

15) Choose a region that the server will be hosted in

16) Run the following command
~~~
gcloud app deploy
~~~

17) Wait for the app to deploy. 

18) Visit the address that is displayed when the deploy command finishes.
~~~
Deployed service [default] to [https://test-project-197703.appspot.com]
~~~

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

## Make the changes needed to upload it to the Google Cloud Platform

7) Add the following to the app.yaml file
~~~
runtime: nodejs
env: flex
~~~
Note: a lot of tutorials on the internet (including [this video](https://www.youtube.com/watch?v=n4svrNcAkJg) that inspired this project) use `vm: true` which is no longer supported. We use `env: flex` instead.

8) Add a 'start' command into the `scripts` object in package.json `"start": "node app.js"`
~~~
"scripts": {
    "start": "node app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
},
~~~
This command tells the server what to do on start. 