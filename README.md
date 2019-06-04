<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [SPARouter][1]
-   [Installation][2]
-   [Basic Usage][3]
    -   [Examples][4]
-   [Query Parameters][5]
    -   [Example][6]
-   [API][7]

## SPARouter

SPARouter is a very light-weight javascript plugin basically for routing front-end for single page applications.
SPARouter allows you to create routes in your front-end whether it is a Single Page Application or not
and pass function you would  want to execute if these routes are matched.

## Installation

You can install SPARouter by hosting it locally or by cdn

-   via npm  
    `npm install @kodnificent/sparouter`
-   via cdn  
    Include this code just before the closing head tag of your html page  

**For develpment use only**  
`<script src="https://unpkg.com/@kodnificent/sparouter@1.1.0/dist/sparouter.js"></script>`  

**For production use**  
`<script src="https://unpkg.com/@kodnificent/sparouter@1.1.0/dist/sparouter.min.js"></script>`

## Basic Usage

Use SPARouter through these easy steps.

-   first create a new instance of the `SPARouter` class by passing options to it.  
-   Call the `router.get()` method for each route and add it's callback function to it.
-   Call `router.notFoundHandler()` to add a callback function it no route was matched. i.e 404 handler
-   Finally call the `router.init()` to initialize the router.

### Examples

```javascript
import SPARouter from "@kodnificent/sparouter"; // if you are hosting locally
const options = {
historyMode : true // set this to true if you use the HTML5 history mode API
}
const router = new SPARouter(options);

router.get("/", function(req, router){

console.log(`Welcome to my home page! The request url is ${req.url}`);
//outputs: Welcome to my home page! The request url is /

}).setName("home");

router.get("/user/{username}", function(req, router){

console.log(`Showing profile for ${req.param.username}. To go back home click <a href="${router.pathFor("home")}">here</a>`);
// if url is /user/victor
//ouputs: Showing profile for victor. To go back home click <a href="/">here</a> 

}).setName("user-profile");

router.notFoundHandler(function(){

console.log("oops! the page you are looking for is probably eaten by a snake");
// if user navigates to /wrong-page
//outputs: oops! the page you are looking for is probably eaten by a snake

});
router.init();
```
## Query Parameters
From version 1.1.0, you can now utilize the router.query object which stores the url search query params.  
The router.query object can be accessed from outside the callback function or inside it.  

### Example
```javascript

// let's assume the user navigated to http://mysite.com/search-page?q=book%20store&books=harry%potter,wizard%20%of%20oz
router.get('/search-page', function(req, router){
     router.query.get('q'); // outputs: book store
     router.query.has('books'); // outputs: true
     router.query.getAll('books'); // outputs: ["harry porter", "wizard of oz"]
});
```

## API

The full API documentation can be found [here][8].

[1]: #sparouter

[2]: #installation

[3]: #basic-usage

[4]: #examples

[5]: #query-parameters

[6]: #example

[7]: #api

[8]: API.md
