![cf](https://i.imgur.com/7v5ASc8.png) lab 16 express authorization
======

# To Submit this Assignment
  * fork this repository
  * write all of your code in a directory named `lab-` + `<your name>` **e.g.** `lab-duncan`
  * push to your repository
  * submit a pull request to this repository
  * submit a link to your PR in canvas
  * write a question and observation on canvas

# Build Tool Instructions
* create a package.json that lists all dependencies and developer dependencies
* include an .eslintrc
* include a .gitignore
 * **add the string `db` to a new line in your gitignore file so that you dont include the db directory monogd is storeing its files in!**
* create a gulpfile
 * have a lint task for running eslint
 * have a test task for running mocha
 * have a nodemon task that restarts your server any time a change has been bade to your **.js** files
 * have a default task for running the lint and mocha tasks

# Directions
* Create these directories to organize your code: 
 * db - use the command `mongod --dbpath ./db` to start mongod using this directory
 * lib
 * model
 * route
 * test
* Create a HTTP Server using `express`
* Use the `http-errors` npm  module with the new`error-response` middleware from lecture
* Create a **User Model** using mongoose with the properties `username`, `password`
 * The users must have a unique username 
 * The user must never store the password as plain text (hash the password)
 * The user must have a method for genorating a token from the user `_id` 
* Create a Basic Auth Middleware for parsing basic auth headers
* use the `body-parser` express middleware on the `POST` and `PUT` routes
* use the npm `debug` module to log the functions being executed in your app
* using the express `Router` create an auth router with routes for **signup** and **signin**
* Your server should depend on the environment variables
 * `DEBUG` - for turing on logging
 * `APP_SECRET` - for signing and verify tokens
 * `PORT` - for setting the port your server will listen on
 * `MONGODB_URI` - for setting the URI that mongoose will conect to

## Server Endpoints
### `/api/signup`
* `POST` request
 * the client should pass the username and passord in the body of the request
 * the server should respond with a token genoratorated using jsonwebtoken and the users `_id`
 * the server should respond with a 400 Bad Request to failed request

### `/api/signin`
* `GET` request 
 * the client should pass the username and password to the server using a _Basic_ auth header
 * the server should respond with a token to authenticated users
 * the server should respond with a 401 Unauthorized to non authenticated users

## Tests 
* your tests should start your server when they begin and stop your server when they finish
* write a test to ensure that your api returns a status code of 404 for routes that have not been registered
* `/api/signup`
 * `POST` - test 400, responds with the `http-errors` 401 name, for if no `body provided` or `invalid body`
 * `POST` - test 200, response body like `<token>` for a post request with a valid body
* `/api/signin`
 * `GET` - test 401, responds with the `http-errors` 401 name, if the users could not be authenticated
 * `GET` - test 200, response body like `<token>` for a request with a valid basic auth header

#Bonus
* Have your token be generated with an `idd` equal to a random unique hash rather than the user's `_id`
