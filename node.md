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
    