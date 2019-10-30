# NODE

## process
- node has a global *process* object with methods and info about the current process
- the process.env property is an object which stores and controls info about the environment in which the process is currently running
    - ex: process.env contains PWD property which holds a string with the directory in which the current process is located
    - use case: a web app in development might perform different tasks than when it is live to users
        - could store this info on process.env
        - could add a property to process.env with the key NODE_ENV and a value of *production* or *development*
        ```js
        if (process.env.NODE_ENV === 'development'){
            console.log('Testing! Testing! Does everything work?');
        }
        ```
    - process.memoryUsage() returns info on CPU demands of the current process

## core and local modules
- modularity is when code is organized into separate files and combines through *requiring* them where needed using the require() function
- Node has several modules included within the environment to efficiently perform common tasks, known as *core* modules
    - these are defined within Node.js's source and are located in the lib/ folder
    - these are required by passing a string with the name of the module into the require() function:
    ```js
    // Require in the 'events' core module:
    let events = require('events');
    ```
- we can use the same require() function to require modules of our own creation
    - the require() function will first check to see if its argument is a core module, if not it will move on to different attempts to locate it
    ```js
    // dog.js
    module.exports = class Dog {
        constructor(name) {
            this.name = name;
        }
        praise() {
            return `Good dog, ${this.name}!`;
        }
    };
    ```
    - module.exports is an object that holds everything in that file that is available to be required into a different file
    ```js
    // app.js
    let Dog = require('./dog.js');
    const tadpole = new Dog('Tadpole');
    console.log(tadpole.praise());
    ```
## NPM
- NPM is an online registry of software shared by other devs
- nodemon monitors your code for changes and restarts an application when it detects changes

## event driven architecture
- in web apps, we need to write logic to handle situations without knowing exactly when they will occur
    - ex: listening for a click event without knowing when it will trigger
- node was created with the same principles to the back-end environment
- node provides an EventEmitter class which we can access by requiring the *events* core module
    ```js
    // Require in the 'events' core module
    let events = require('events');
    // Create an instance of the EventEmitter class
    let myEmitter = new events.EventEmitter();
    ```
    - each event emitter instance has an **.on()** method which assigns a listener callback function to a named event
        - the .on() method takes as its first argument the name of the event as a string and as a second argument the listener callback function
    - each event emitter instance also has an **.emit()** method which announces a named event has occurred
        - the .emit() method takes as its first argument the name of the event as a string and as its second argument, the data that should be passed into the listener callback function
    ```js
    let newUserListener = (data) => {
    console.log(`We have a new user: ${data}.`);
    };

    // Assign the newUserListener function as the listener callback for 'new user' events
    myEmitter.on('new user', newUserListener)

    // Emit a 'new user' event
    myEmitter.emit('new user', 'Lily Pad') //newUserListener will be invoked with 'Lily Pad'
    ```

## user input/output
- in Node, console.log() method is a 'thin wrapper' on the *.stdout.write()* method of the *process* object
- in Node, we can also receive input from a user through the terminal using the *stdin.on()* method on the *process* object
    ```js
    process.stdin.on('data', (userInput) => {
    let input = userInput.toString()
    console.log(input)
    });
    ```
    - here we are able to use *.on()* because process.stdin is an instance of EventEmitter
    - when a user enters text into the terminal and hits enter, a 'data' event will be fired and our listener callback will be invoked
    - the userInput we receive is an instance of the Node Buffer class, so we convert to string before printing

## Errors
- many asynchronous node APIs use *error-first callback functions*
    - these are callback functions with an error as the first expected argument and data as the second argument
        - if the asynchronous task results in an error, it will be passed in as the first argument to the callback function
        - if no error was thrown, the first argument will be *undefined*
    ```js
    const errorFirstCallback = (err, data)  => {
    if (err) {
        console.log(`There WAS an error: ${err}`);
    } else {
        // err was falsy
        console.log(`There was NO error. Event data: ${data}`);
        }
    }
    ```

## filesystem
- when running js code on a browser it is important for a script to have only limited access to a user's filesystem
    - technique known as *sandboxing*
- Node back end is less restricted
- Node fs core module is an API for interacting with the file system
    - each method available through the fs module has a synchronous version and an asynchronous version
    - one method available on the fs core module is the .readFile() method, which reads data from a provided file:
    ```js
    const fs = require('fs');
    let readDataCallback = (err, data) => {
        if (err) {
            console.log(`Something went wrong: ${err}`);
        } else {
            console.log(`Provided file contained: ${data}`);
        }
    };
    fs.readFile('./file.txt', 'utf-8', readDataCallback);
    ```
    - fs.readFile('filepath/name.txt','encoding',callbackFunction);
        - encoding UTF-8
    
## readable streams
- streaming data involves processing data sequentially, piece by piece
- this is preferrable because you dont need enough RAM to process all the data at once, nor do you need all data up front to begin processing
    - ex: reading files line by line
    - to read line by line we can use .createInterface() from the readline core module
    - .createInterface() returns an EventEmitter set up to emit 'line' events
    ```js
    const readline = require('readline');
    const fs = require('fs');

    const myInterface = readline.createInterface({
        input: fs.createReadStream('text.txt')
    });

    myInterface.on('line', (fileLine) => {
        console.log(`The line read: ${fileLine}`);
    });
    ```
    - assign myInterface the returned value from invoking *readline.createInterface()* with an object containing our designated input
    - set our *input* to fs.createReadStream('text.txt') which will create a stream from the text.txt file
    - next assign a listener callback to execute when *line* events are emitted
        - *line* events are emitted after each line from the file is read
    - the listener callback will log to console 'the line read: [fileLine]'
        - where [fileLine] is the line just read

## writable streams
- we can create a writable stream to a file using the *fs.createWriteStream()* method:
    ```js
    const fs = require('fs')
    const fileStream = fs.createWriteStream('output.txt');
    fileStream.write('This is the first line!'); 
    fileStream.write('This is the second line!');
    fileStream.end();
    ```

## HTTP module
- http module contains functions which simplify interacting with HTTP and streamline receiving and responding to requests
- the http.createServer() method returns an instance of an http.server
    - an http.server has a method .listen() which causes the server to listen for incoming connections
    - when we run http.createServer() we pass in a custom callback function
    - this callback function will be triggered once the server is listening and receives a request
    - breakdown:
        - the function expects two args: a request object and a response object
        - each time a request to the server is made, Node will invoke the provided *requestListener* callback function, passing in the request and response objects of the incoming request
        - request and response objects come with a number of properties and methods of their own, and within the requestListener function, we can access information about the request via the request object passed in
        - the *requestListener* is responsible for setting the response header and body
        - the *requestListener* must signal that the interaction is complete by calling the *response.end()* method

    ```js
    const http = require('http');
    let requestListener = (request, response) => {
        response.writeHead(200, {'Content-Type': 'text/plain' });
        response.write('Hello World!\n');
        response.end();
    };
    const server = http.createServer(requestListener);
    server.listen(3000);

    ```

    - required the http core module
    - created a *server* veriable assigned to the return value of the http.createServer() method
    - invoked http.createServer() with our requestListener callback
        - similar to running the .on() of an EventEmitter
        - the requestListener will execute whenever an HTTP request is sent to the server on the connected port
    - within requestListener callback, make changes to the response object, *response*, so that is can send the appropriate information to the client sending the request
        - status code 200 means no errors were encountered
        - header communicates that the file type is text, rather than something like audio or compressed data
    - last line starts the server with port 3000
