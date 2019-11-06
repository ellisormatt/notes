## starting a server
    ```
    const express = require('express');
    const app = express();
    app.listen();
    ```
    - import and invoke the *express* function
- tell the server where to listen for new requests using app.listen()
    ```js
    const PORT = 4001;
    app.listen(PORT,()=>{
        console.log(`the server is listening on port ${PORT}`);
    });

- to tell the server how to deal with requests, we register a series of routes
    - routes define the control flow for requests based on the requests path and HTTP verb
    ```
    localhost:4001/monsters
    ```
    - the path is the portion after the hostname and port number: '/monsters'
- express uses app.get() to register routes to match GET requests
    - express routes usually take two arguments, a path and a callback function to handle the request and send a response
    ```js
    const moods = [{ mood: 'excited about express!'}, { mood: 'route-tastic!' }];
    app.get('/moods', (req, res, next) => {
        // Here we would send back the moods array in response
    });
    ```
    - will match any GET requests to '/moods' and the callback function, passing in two objects as the first two arguments
    - these objects represent the request sent to the server and the response that the Express server should eventually send to the client
    - if no routes are matched on a client request, Express server responds by sending a 404
## sending a response
- express servers send responses usiung the .send() method on the response object
    - .send() will take any input and include it in the body
    ```js
    const monsters = [{ type: 'werewolf' }, { type: 'hydra' }, { type:'chupacabra' }];
    app.get('/monsters', (req, res, next) => {
        res.send(monsters);
    });
    ```
    - in this example, a GET /monsters request will match the route
    - express will call the callback function and the res.send() method will send back an array of monsters
    - in addition to .send(), .json() can be used to explicitly send JSON-formatted responses
        - .json() sends any JavaScript object passed into it

## matching route paths

<img src="https://s3.amazonaws.com/codecademy-content/courses/learn-express-routes/express_yourself_diagram_1.svg" alt="Diagram of how Express matches route paths. Both the `action` and the `path` must match to get the correct response from the server. " class="fit-full francine-image">

- express tries to match requests by route
- express searches through routes in the order that they are registered in your code

## getting a single expression

- routes are more powerful when they can be used dynamically
    - express provides this with named route parameters
- parameters are route path segments that begin with **:** in their express route definitions
    - they act as wildcards
        - ex: /monsters/:id matches /monsters/1 and /monsters/45
- express parses any parameters, extracts their actual values, attaches them as an object to the request object: req.params
    - this object's keys are any parameter names in the route, and each key's value is the actual value of that field per request
    ```js
    const monsters = { hydra: { height: 3, age: 4 }, dragon: { height: 200, age: 350 } };
    // GET /monsters/hydra
    app.get('/monsters/:name', (req, res, next) => {
        console.log(req.params) // { name: 'hydra' };
        res.send(monsters[req.params.name]);
    });
    ```
    - above, a .get() route is defined to match /monsters/:name
    - when a GET request arrived for /monsters/hydra, the callback is called
    - inside the callback, req.params is an object with the key *name* and the value *hydra* which was present in the actual request path

## setting status codes
- express allows us to set the status code on responses before they are sent
- response codes provide information to clients about how their requests were handled
- the res object has a .status() method to allow us to set the status code, and other methods like .send() can be chained from it
    ```js
    const monsterStoreInventory = { fenrirs: 4, banshees: 1, jerseyDevils: 4, krakens: 3 };
    app.get('/monsters-inventory/:name', (req, res, next) => {
        const monsterInventory = monsterStoreInventory[req.params.name];
        if (monsterInventory) {
            res.send(monsterInventory);
        } else {
            res.status(404).send('Monster not found');
        }
    });
    ```
    - in this example, we implemented a route to retrieve inventory levels from a Monster Store
    - inventory levels are kept in the monsterStoreInventory variable
    - when a request arrives for /monsters-inventory/mothMen, the route matches and so the callback is invoked
    - req.params.name will be equal to 'mothMen' and so our program accesses monsterStoreInventory['mothMen']
    - since there are no mothMen in our inventory, res.status() sets a 404 status code on the response and .send() sends the response

## using queries
- query strings appear at the end of a path and they are indicated with a ? character
    - ex: /monsters/1?name=chimera&age=1
        - query string is *name=chimera&age=1*
        - path is */monsters/1/*
- query strings do not count as part of the route path
    - instead, Express parses them into an object and attaches it to the request body as *req.query*
    - they key:value relationship is indicated by the **=** character in the above example route
    - the req.query object would be { name: 'chimera', age: '1' }
    ```js
    const monsters = { '1': { name: 'cerberus', age: '4'  } };
    // PUT /monsters/1?name=chimera&age=1
    app.put('/monsters/:id', (req, res, next) => {
        const monsterUpdates = req.query;
        monsters[req.params.id] = monsterUpdates;
        res.send(monsters[req.params.id]);
    });
    ```
    - here we have a route for updating monsters by ID
    - when a PUT /monsters/1?name=chimera&age=1 request arrives, our callback function is called and we create a monsterUpdates variable to store req.query
    - since req.params.id is '1', we replace monsters['1']'s value with monsterUpdates
    - finally, express sends back the new monsters['1']
- when updating, many servers send back the updated resource after the updates are applied so that the client has the same version of the resource as the server

## creating an expression
- POST is the HTTP verb used for creating new resources
- 
---------------------------------

## summary

- routes usually take two arguments, a path and a callback function to handle the request and send a response

- app.get()
    - registers routes to match GET requests
    ```js
    app.get('/path',(req,res,next)=>{/*some things*/});
    ```
    - responds to GET requests to '/path'

- express responds using the .send() method on the response object
- express parses parameters in reqeusts and attaches the values as an object to the request object **req.params**
    - the object's keys are any parameter names, with key values being the actual value of the field 
    ```js
    //GET /monsters/hydra
    app.get('/monsters/:name', (req,res,next)=>{
        console.log(req.params); // {name: 'hydra'}
    });
    ```
- the *res* object has a .status() method to allow us to set the status code, can chain other methods like .send() to it
- query strings
    - **/monsters/1?name=chimera&age=1**
    - query string is name=chimera&age=1
    - path is /monsters/1/
    - express attaches the query string as an object to the request as req.query
    - above, req.query would be **{name:'chimera',age:'1'}**
    