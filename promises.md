- promises are objects that represent the eventual outcome of an asynchronous operation
- can exist in one of three states
    - pending: initial state, operation not completed yet
    - fulfilled: operation completed successfully and promise now has a resolved value
    - rejected: operation failed and the promise has a reason for the failure
        - reason is usually an error of some kind
- we refer to a promise  as settled if it is no longer pending - it is either fulfilled or rejected


- to create a promise, use the *new* keywords and the *Promise* constructor method:
    ```js
    const executorFunction = (resolve,reject) => {};
    const myPromise = new Promise(executorFunction);
    ```
- the *Promise* constructor takes a function parameter called the *executor function* which runs automatically when the constructor is called, usually starts an asynchronous operation and dictates how the promise should be settled
- the executor function has two function parameters, referred to as the *resolve()* and *reject()* functions
    - these are not defined by the programmer
    - *resolve* is a function with one argument, when invoked it changes promise's status from *pending* to *fulfilled* 
        - then, the promise's resolved value will be set to the argument passed into *resolve()*
    - *reject* is a function that takes a reason or error as an argument, when invoked it will change status to *rejected*
        - then, the promise's rejection reason will be set to the argument passed into *reject()*
    ```js
    const executorFunction = (resolve, reject) => {
        if (someCondition) {
            resolve('I resolved!');
        } else {
            reject('I rejected!'); 
        }
    }
    const myFirstPromise = new Promise(executorFunction);
    ```

- to handle a successful promise, one that was resolved, we invoke *.then()* on the promise, passing in a success handler callback function:
    ```js
    const prom = new Promise((resolve, reject) => {
        resolve('Yay!');
    });

    const handleSuccess = (resolvedValue) => {
    console.log(resolvedValue);
    };

    prom.then(handleSuccess); // Prints: 'Yay!'
    ```
- with typical promise consumption, we won't know whether a promise will resolve or reject, so we'll need to provide the logic for either case
- we can pass both an *onFulfilled* and *onRejected* callback to *.then()*
    ```js
    let prom = new Promise((resolve, reject) => {
        let num = Math.random();
        if (num < .5 ){
            resolve('Yay!');
        } else {
            reject('Ohhh noooo!');
        }
    });

    const handleSuccess = (resolvedValue) => {
    console.log(resolvedValue);
    };

    const handleFailure = (rejectionReason) => {
    console.log(rejectionReason);
    };

    prom.then(handleSuccess, handleFailure);
    ```
- *.then()* will return a promise with the same settled value as the promise it was called on if no appropriate handler was provide
    - this allows us to separate our resolved logic from rejected logic
    - instead of passing both handlers into one *.then()*, we can chain a second *.then()* with a success handler and both cases will be handled
    ```js
    prom
        .then((resolvedValue) => {
            console.log(resolvedValue);
        })
        .then(null, (rejectionReason) => {
            console.log(rejectionReason);
        });
    ```
- to make this more readable, we can use *.catch()* to handle rejection logic
    - the *.catch()* function takes only one argument, *onRejected*
    - tin the case of a rejected promise, this failure handler will be invoked with the reason for rejection
    - using *catch()* accomplishes the same thing as using a *.then()* with only a failure handler
    ```js
    prom
        .then((resolvedValue) => {
            console.log(resolvedValue);
        })
        .catch((rejectionReason) => {
            console.log(rejectionReason);
        });
    ```

- *concurrency* is the process of multiple asynchronous operations happening together
    - we can do this with *Promise.all()*
    - *Promise.all()* accepts an array of promises as its argument and returns a single promise
    - that promise will settle in one of two ways:
        - if every promise in the argument array resolves, the single promise returned from *Promise.all()* will resolve with an array containing the resolve value from each promise in the argument array
        - if any promise from the argument array rejects, the single promise returned will immediately reject with the reason that promise rejected, behavior known as *failing fast*
    ```js
    let myPromises = Promise.all([returnsPromOne(), returnsPromTwo(), returnsPromThree()]);

    myPromises
    .then((arrayOfValues) => {
        console.log(arrayOfValues);
    })
    .catch((rejectionReason) => {
        console.log(rejectionReason);
    });
