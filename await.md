- the *async* keyword is used to write functions that handle asynchronous actions
    - we wrap our asynchronous logic inside a function prepended with the *async* keyword, then invoke that function
    ```jsa
    async function myFunc() {
        // Function body here
    };

    myFunc();
    ```
- async functions always return a promise, so we can still use normal promise syntax like *.then()* and *.catch*
- async functions will return in one of three ways
    - if no return value from function, it will return a promise with a resolved value of *undefined*
    - if returns a non-promise value, it will return a promise resolved to that value
    - if a promise is returned, it will simply return that promise
- await can only be used inside an async function, is is an operator: it returns the resolved value of a promise
- await halts or pauses the execution of our async function until a given promise is resolved
- in the example below, *myPromise()* is a function that returns a promise which will resolve to the string "I am resolved now!"
    ```js
    async function asyncFuncExample(){
        let resolvedValue = await myPromise();
        console.log(resolvedValue);
    }

    asyncFuncExample(); // Prints: I am resolved now!
    ```
    - within our async function, asyncFuncExample(), we use await to halt our execution until myPromise() is resolved and assign its resolved value to the variable resolvedValue. then, we log resolvedValue to the console.
        - we are able to handle the logic for a promise in a way that reads like synchronous code
- handling dependent promises
    - with traditional promise syntax:
    ```js
    function nativePromiseVersion() {
        returnsFirstPromise()
        .then((firstValue) => {
            console.log(firstValue);
            return returnsSecondPromise(firstValue);
        })
        .then((secondValue) => {
            console.log(secondValue);
        });
    }
    ```
    - with using an async function to accomplish the same thing
    ```js
    async function asyncAwaitVersion() {
        let firstValue = await returnsFirstPromise();
        console.log(firstValue);
        let secondValue = await returnsSecondPromise(firstValue);
        console.log(secondValue);
    }
- handling errors
    - with async...await, we use try...catch statements for error handling
    - allows us to catch both synchronous and asynchronous errors
    ```js
    async function usingTryCatch() {
    try {
        let resolveValue = await asyncFunction('thing that will fail');
        let secondValue = await secondAsyncFunction(resolveValue);
    } catch (err) {
        // Catches any errors in the try block
        console.log(err);
        }
    }

    usingTryCatch();
    ```
- not all of these promises need to be handled as if they are dependent on one another:
    ```js
    async function waiting() {
        const firstValue = await firstAsyncThing();
        const secondValue = await secondAsyncThing();
    console.log(firstValue, secondValue);
    }

    async function concurrent() {
        const firstPromise = firstAsyncThing();
        const secondPromise = secondAsyncThing();
    console.log(await firstPromise, await secondPromise);
    }
    ```
    - in the *waiting()* function, we pause our function until the first promise resolved, then we construct the second promise
    - in the *concurrent()* function, both promises are constructed without using *await*
        - we then await each of the resolutions to print them to console
        - with the *concurrent()* function, both promises' asynchronous operations can be run simultaneously

- another way to use concurrency when we have multiple promises which can be executed simultaneously is to *await* a *Promise.all()*
    - we can pass an array of promises as the argument to *Promise.all()* and it will return a single promise
        - this promise will resolve when all promises in the argument array have resolved
        - the promise's resolve value will be an array containing the resolved values of each promise from the argument array
    ```js
    async function asyncPromAll() {
        const resultArray = await Promise.all([asyncTask1(), asyncTask2(), asyncTask3(), asyncTask4()]);
        for (let i = 0; i<resultArray.length; i++){
            console.log(resultArray[i]); 
        }
    }
    ```
    - Promise.all() also fails fast