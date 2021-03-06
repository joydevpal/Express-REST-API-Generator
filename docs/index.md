# Express REST API Generator

[![Build Status](https://travis-ci.org/iolufemi/Express-REST-API-Generator.svg?branch=dev)](https://travis-ci.org/iolufemi/Express-REST-API-Generator)  [![codecov](https://codecov.io/gh/iolufemi/Express-REST-API-Generator/branch/master/graph/badge.svg)](https://codecov.io/gh/iolufemi/Express-REST-API-Generator) [![Documentation Status](https://readthedocs.org/projects/api-template/badge/?version=latest)](http://api-template.readthedocs.io/en/latest/?badge=latest)

Express REST API Generator is an Express Based API skeleton. A template for starting projects with express as an API. This project can be used for creating a RESTful API using Node JS, Express as the framework, Mongoose to interact with a MongoDB instance and Sequelize for support of SQL compatible databases. Mocha is also used for running unit tests in the project.

The resulting API from this project is a JSON REST API which will respond to requests over HTTP. REST Clients can, therefore, connect to the resulting REST server.

## What is API?

In computer programming, an application programming interface (API) is a set of clearly defined methods of communication between various software components. A good API makes it easier to develop a computer program by providing all the building blocks, which are then put together by the programmer. An API may be for a web-based system, operating system, database system, computer hardware or software library. Just as a graphical user interface makes it easier for people to use programs, application programming interfaces make it easier for developers to use certain technologies in building applications. - [Wikipedia](https://en.wikipedia.org/wiki/Application_programming_interface)

## What is REST?

Representational state transfer (REST) or RESTful web services is a way of providing interoperability between computer systems on the Internet. REST-compliant Web services allow requesting systems to access and manipulate textual representations of Web resources using a uniform and predefined set of stateless operations. - [Wikipedia](https://en.wikipedia.org/wiki/Representational_state_transfer)

> NOTE: The use of this project requires that you have a basic knowledge of using express in building a REST API. If you are a newbie, here are some awesome tutorials to get you started.

- [Build Node.js RESTful APIs in 10 Minutes](https://www.codementor.io/olatundegaruba/nodejs-restful-apis-in-10-minutes-q0sgsfhbd)
- [Easily Develop Node.js and MongoDB Apps with Mongoose](https://scotch.io/tutorials/using-mongoosejs-in-node-js-and-mongodb-applications)
- [Build a RESTful API Using Node and Express 4](https://scotch.io/tutorials/build-a-restful-api-using-node-and-express-4)

## Why use Express REST API Generator?

1. To enable you to develop REST APIs in the fastest way possible.
2. To encourage endpoint versioning.
3. To encourage unit testing and make it super easy to get started with writing unit tests by generating basic unit tests for generated components. 
4. To enforce best practice in writing javascript apps by using lint.
5. To encourage good code file structure that can be easily followed by other team members, especially new team members.
6. To make it easy to build secure APIs with the ability to communicate with the frontend in an encrypted fashion.
7. To encourage backing up of deleted data.
8. To encourage logging API requests and responses for audit purposes.
9. To encourage proper Error handling and logging.
10. To encourage a uniform API response format across teams.
11. To make it easy to write asynchronous logic and applications using the inbuilt distributed job queue.

## Installation

To start your project with Express REST API Generator, clone the repository from GitHub and install the dependencies.

```
$ git clone https://github.com/iolufemi/Express-REST-API-Generator.git ./yourProjectName 
$ cd yourProjectName
$ npm install
$ npm install -g mocha gulp
```

Then generate your first API endpoint

```
$ gulp service --name yourFirstEndpoint // This command will create a CRUD endpoint for yourFirstEndpoint.
```

With the `gulp service` command, you have the option of using either Mongo DB, an SQL compatible DB or using an API generated by this Express Generator as a database model. To use an API as a database you can pass the `baseurl` and the `endpoint` option for the API to the `gulp service `; for an SQL compatible db, pass the `sql` option. See an example below

### Using an API as a DB

```
$ gulp service --name yourEndpointWithAPIAsDB --baseurl http://localhost:8080 --endpoint users
```

### Using an SQL compatible database

```
$ gulp service --name yourEndpointWITHSQL --sql
```

> Note: You can use -n instead of --name, -b instead of --baseurl, -e instead of --endpoint

Try out your new endpoint.

Start the app

```
$ npm start
```
by default, the app will start on `POST 8080`

You can change the PORT by adding a `PORT` environment variable. 
eg.

```
$ PORT=6000 npm start
```
now the app will start on `PORT 6000`

To start the app for development, run

```
$ gulp
```
This will automatically restart your app whenever a change is detected.

You will now be able to access CRUD (create, read, update and delete) endpoints 

`[POST] http://localhost:8080/yourFirstEndpoint` Create yourFirstEndpoint resources
`[GET] http://localhost:8080/yourFirstEndpoint` Get yourFirstEndpoint resources. Supports limits, sorting, pagination, select (projection), search and date range
`[GET] http://localhost:8080/yourFirstEndpoint/:id` Get a yourFirstEndpoint resource
`[PUT] http://localhost:8080/yourFirstEndpoint` Update yourFirstEndpoint resources
`[PATCH] http://localhost:8080/yourFirstEndpoint/:id` Update one yourFirstEndpoint resource
`[DELETE] http://localhost:8080/yourFirstEndpoint?key=value` Delete yourFirstEndpoint resources
`[DELETE] http://localhost:8080/yourFirstEndpoint/:id` Delete one yourFirstEndpoint resource
`[POST] http://localhost:8080/yourFirstEndpoint/:id/restore` Restore a previously deleted yourFirstEndpoint resource

> Note: For every `POST` API calls you need to send an `x-tag` value in the header. This value is used for secure communication between the server and client. It is used for AES encrytion when secure mode is enabled. To get a valid `x-tag` call the `[GET] /initialize` endpoint.   

## Some asynchronous goodness

Start the clock (You should only have a single instance of this at all times.)

```
$ npm run clock
```
The clock is similar to a crontab. It dispatches tasks to available workers at a predefined interval.

To define a clock, look for the `clock` collection in the MongoDB you connected to the `LOG_MONGOLAB_URL` environment variable, and create a record similar to the below

```json
{ 
    "crontab" : "* * * * *", 
    "name" : "Task Name", 
    "job" : "theJobAsDefinedInTheWorkerFile", 
    "enabled" : true
}
```

> NOTE: Whenever you change the value of a clock on the DB, you need to restart the clock. (Still looking for the best way to make this automatic)

Start the workers 

```
$ npm run workers
```
A worker runs tasks or processes in the background. It is useful for running long running processes and background tasks.

See `/services/queue/jobs` for sample tasks and `/services/queue/workers` for how to setup worker processes.

## Versioning your API endpoints

You can create multiple versions of your API endpoints by simply adding the version number to your route file name. eg. `users.v1.js` will put a version of the users resources on the `/v1/users` endpoint. users.v2.js will put a version of the users resources on the `/v2/users` endpoint. The latest version of the resources will always be available at the `/users` endpoint.

> NOTE: This project will automatically load route files found in the routes folder.

## File Structure

- config
- controllers
- models
- routes
- services
- templates
- test

## Getting support, Reporting Bugs and Issues

If you need support or want to report a bug, please log an issue [here](https://github.com/iolufemi/Express-REST-API-Generator/issues)

## Running Unit Tests

All generated endpoints come with complete test suits, we encourage you to update the tests as you extend the logic

```
$ npm test
```

## How to contribute

View how to contribute [here](https://github.com/iolufemi/Express-REST-API-Generator/blob/master/CONTRIBUTING.md)

## Code of Conduct

View the code of conduct [here](https://github.com/iolufemi/Express-REST-API-Generator/blob/master/CODE_OF_CONDUCT.md)

## Contributors

- [Olufemi Olanipekun](https://github.com/iolufemi)

## FAQs
