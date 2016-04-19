# MeanPeriod5
### Question 1: Name attributes of HTTP protocol makes it difficult to use for real time systems?
> To be added...


### Question 2: Explain polling and long-polling strategies, their pros and cons?
#### Short Polling
When a client makes an HTTP request to a server the server creates a response and sends that back immediatly, this is how HTTP has worked for many years this also means that creating real time applications is not possible.

##### Pro's 
Simple
Not server side consuming

##### Con's
Not immediate notification when server gets new data

#### Long Polling
To overcome this problem, developers has to use another technique called long polling. In this, the client makes an HTTP request to the server but the server does not respond immediatly but waits until new data is avaible and then responds. When the client gets a response it immediatly creates a new request and the same pattern repeats again and again creating an "illusion" of real time.

##### Pro's 
Immediate response from server

##### Con's
Complex
Server side consuming

### Question 3: What is HTTP streaming, SSE (Server sent events)?
Here a client "subscribes" to a stream of server responses. This means that the client sends a single request to the server and then the server can respond with multiple reponses.  
SSE is not supported by IE or Edge yet, but is being implemented at some point.


### Question 4: What is WebSocket protocol, how is it different from HTTP communication, what advantages it has over HTTP?
The Websocket protocol is a new way to handle real time responses. It allows for Full-Duplex communication over a single TCP connection. This means that data can both be sent and recieved at the same time, and one doesn't have to wait for the other.  
This means that the Websocket protocol is much faster than HTTP because you only make one handshake at the start of the exchange of data.


### Question 5: Explain what the WebSocket Protocol brings to the Web-world?
It brings TCP sockets that we know from Java to the world of web-development, making actual realtime transactions possible. And not using some phony method like long-polling or http streaming.


### Question 6: Explain and demonstrate the process of WebSocket communication - From connecting client to server, through sending messages, to closing connection?
> To be added...


### Question 7: What's the advantage of using libraries like Socket.IO, Sock.JS, WS, over pure WebSocket libraries in the backend and standard APIs on frontend? Which problems do they solve?
> To be added...


### Question 8: What is Backend as a Service, Database as a Service, why would you consider using Firebase in your projects?
> To be added...


### Question 9: Explain the pros & cons of using a Backend as a Service Provider like Firebase?
> To be added...

### Question 10: Explain and demonstrate “three-way data binding” using Firebase and Angular?
> To be added...

### Question 11: Explain and demonstrate the difference between the simple chat system in your own WebSocket + Node.js backend vs. Firebase?
> To be added...

