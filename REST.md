# REST

## separation of client and server
- with the REST architectural style, implementation of client and server can happen independently of one another
    - code on client and server can change any time without affecting the other
    - by using a REST interface, clients hit the same REST endpoints, perform the same actions, and receive the same responses

## statelessness
- REST compliant systems are stateless, meaning the server does not need to know anything about what state the client is in and vice versa
- server and client can understand any message received even without seeing previous messages
- REST systems interact through standard operations on resources, they do not rely on the implementation of interfaces

# Communication between client and server
- in REST architecture, clients send requests to retrieve or modify resources and servers send responses to those requests

## making requests
- REST requires that a client make a request to the server in order to retrieve or modify data on the server
- a request generally consists of:
    - an HTTP verb, describes what kind of operation to perform
    - a *header* which allows the client to pass along info about the request
    - a path to a resource
    - an optional message body containing data

## HTTP verbs
- 4 basic HTTP verbs:
    - GET - retrieve a specific resource (by ID) or a collection of resources
    - POST - create a new resource
    - PUT - update a specific resource (by ID)
    - DELETE - remove a specific resource by ID

## headers and accept parameters
- in the header of the request, client sends the type of content it is able to receive from the server, this is called the **accept** field
    - ensures that the server does not send data that cannot be understood or processed by the client
    - options for types of content are MIME (multipurpose internet mail extensions) 
    - MIME types consist of a *type* and a *subtype*, separated by a slash (/)
        - ex: a text file containing HTML would be specified with the type *text/html*
        - if this file contained CSS instead, it would be specified as *text/css*
        - generic text file would be *text/plain*

## paths
- requests must contain a path to a resource that the operation should be performed on
    - ex: fashionboutique.com/customers/223/orders/12
    - accessing order with id 12 for customer with id 223
- paths should contain the information necessary to locate a resource with the degree of specificity needed

# Sending Responses

## Content Types
- when the server sends a data payload to the client, the server must include a content-type header in the response
    - content-types are MIME Types
    - content-type sent by the server should be one of the options that the client specified in the accept field of the request
    ```
    HTTP/1.1 200 (OK)
    Content-Type: text/html
    ```
    - indicates that the content requested is being returned with content-type of text/html

## response codes
- responses from the server contain status codes to alert the client to information about the success of the operation
    ```
    200 (OK)	This is the standard response for successful HTTP requests.
    201 (CREATED)	This is the standard response for an HTTP request that resulted in an item being successfully created.
    204 (NO CONTENT)	This is the standard response for successful HTTP requests, where nothing is being returned in the response body.
    400 (BAD REQUEST)	The request cannot be processed because of bad request syntax, excessive size, or another client error.
    403 (FORBIDDEN)	The client does not have permission to access this resource.
    404 (NOT FOUND)	The resource could not be found at this time. It is possible it was deleted, or does not exist yet.
    500 (INTERNAL SERVER ERROR)	The generic answer for an unexpected failure if there is no more specific information available.
    ```
- for each HTTP verb, there are expected status codes a server sdhould return upon success:
    ```
    GET — return 200 (OK)
    POST — return 201 (CREATED)
    PUT — return 200 (OK)
    DELETE — return 204 (NO CONTENT) If the operation fails, return the most specific status code possible corresponding to the problem that was encountered.
    ```
## Examples
- in this example an application allows you to view, create, edit and delete customers and orders
- the HTTP API allows a client to perform these functions:

- to view all customers
    ```
    GET http://fashionboutique.com/customers
    Accept: application/json
    ```
    - response headers look like:
    ```
    Status Code: 200 (OK)
    Content-type: application/json
    ```
    - followed by *customers* data requested in application/json format
- create a new customer by posting data:
    ```
    POST http://fashionboutique.com/customers
    Body:
    {
        “customer”: {
            “name” = “Scylla Buss”
            “email” = “scylla.buss@codecademy.org”
        }               
    }
    ```
    - server then generates an ID for that object and returns it back to the client with a header like:
    ```
    201 (CREATED)
    Content-type: application/json
    ```
- to view a single customer, we GET it by specifying the customer's ID
    ```
    GET http://fashionboutique.com/customers/123
    Accept: application/json
    ```
    - response looks like
    ```
    Status Code: 200 (OK)
    Content-type: application/json
    ```
    - followed by data for the customer resource with an id 23 in application/json format
- we can update the customer by PUTting the new data:
    ```
    PUT http://fashionboutique.com/customers/123
    Body:
    {
        “customer”: {
            “name” = “Scylla Buss”
            “email” = “scyllabuss1@codecademy.com”
        }
    }
    ```
- we can also delete that customer by specifying its id
    ```
    DELETE http://fashionboutique.com/customers/123
    ```
