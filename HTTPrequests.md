## GET requests
- we use GET to retrieve data from a source

<img src="https://s3.amazonaws.com/codecademy-content/courses/intermediate-javascript-requests/diagrams/XHR+GET+transparent.svg" class="fit-full francine-image">

## POST requests
- sends info to an API in order to get the service on the other end to process and return some info

<img src="https://s3.amazonaws.com/codecademy-content/courses/intermediate-javascript-requests/diagrams/XHR+POST+transparent.svg" class="fit-full francine-image">


## FETCH requests
- the fetch() function:
    - creates a request object that contains relevant info that an API needs
    - sends the request object to the API endpoint
    - returns a promise that ultimately resolves to a response object, which contains the status of the promise with info that the API sent back

<img src="https://s3.amazonaws.com/codecademy-content/courses/intermediate-javascript-requests/diagrams/fetch+GET+transparent.svg" class="fit-full francine-image">

## fetch() POST requests
- initial call takes two arguments: endpoint and an object containing info needed for the POST request

<img src="https://s3.amazonaws.com/codecademy-content/courses/intermediate-javascript-requests/diagrams/fetch+POST+transparent.svg" class="fit-full francine-image">

## async GET requests
- key points:
    - using an async function will return a promise
    - await can only be used in an async function
        - await alows a program to run while waiting for a promise to resolve
    - in a try...catch statement, code in the try block will be run and in the event of an exception/error, the code in the catch statement will run

<img src="https://s3.amazonaws.com/codecademy-content/courses/intermediate-javascript-requests/diagrams/async+await+GET+transparent.svg" class="fit-full francine-image">


## async POST requests

<img src="https://s3.amazonaws.com/codecademy-content/courses/intermediate-javascript-requests/diagrams/async+await+POST+transparent.svg" class="fit-full francine-image">