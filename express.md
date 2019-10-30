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
- 