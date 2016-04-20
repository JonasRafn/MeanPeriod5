# MeanPeriod5
### Question 1: Name attributes of HTTP protocol makes it difficult to use for real time systems?
The HTTP protocol has some limitations which makes it difficult to use for real time systems. First of all whenever you make a request, say to download html, or an image, a port/socket is opened, data is transferred, and then it is closed.

The opening and closing creates overhead, and for certain applications, especially for real time systems which require real time interactions this just doesn’t work.

Another limitation with HTTP is that it is a “pull” paradigm. The browser will request or pull information from servers, but the server can't push data to the browser when it wants to. This means that browsers will have to poll the server for new information by repeating requests every so often, to see if there is any new data.


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
When a connection through a websocket is opened it all start with a "Handshake" the same principle as when using token authentication. After the handshake the connection is now open, and the client can sends messages to the server and the other way around, as many times as needed. When the transactions is over, either the client or the server closes the connection.

![](https://www.pubnub.com/static/images/get-started/websockets_guides.png)


### Question 7: What's the advantage of using libraries like Socket.IO, Sock.JS, WS, over pure WebSocket libraries in the backend and standard APIs on frontend? Which problems do they solve?
* Easier to use, maintained
* Crossbrowser compatability is already developed for it
* Fallbacks to other technologies if client browser is not compatible


### Question 8: What is Backend as a Service, Database as a Service, why would you consider using Firebase in your projects?
Backend as a Service (BaaS), is cloud based infrastructure for mobile and web apps. Its simply cloud computing for developers to make easy scalable applications for mobile and web.  

DataBase as a Service (DBaaS) is a cloud based database approach, to create scalable and felxible data storage in the cloud. 

FireBase is not any ordinary DBaaS, it's a real-time scalable backend that provides the tools to quickly build applications for millions of users. 


### Question 9: Explain the pros & cons of using a Backend as a Service Provider like Firebase?
#### pro's 
* Scalable
* Flexible
* Easy to use
* Possibility for Authentication
* Possibility for hosting
#### con's
* Lack of control over network performance issues, such as unacceptable latency 
* "Pay per view", pay for the bandwidth you use

### Question 10: Explain and demonstrate "three-way data binding" using Firebase and Angular?
When using AngularJS the scope of our controller and view stay synced creating a 2-way databinding (ng-model). Using firebase as a backend makes it possible to create 3-way databinding. We can bind the datamodel of our AngularJS app and a FireBase location like "https://xxx.firebaseio.com/users", this way whenever the model on FireBase changes the updates are automatically pushed to the front-end and the other way round.

Refer to [Thinkster tutorial]

### Question 11: Explain and demonstrate the difference between the simple chat system in your own WebSocket + Node.js backend vs. Firebase?
In AngularJS you have to create a connection to the client, and everytime a message is sent you need to add that to a local scope variable and call ``` $scope.$apply ``` to make sure AngularJS updates the scope.  
See [SimpleChat]

Where as in Firebase you only need a few lines of code, and that small app is even scalable from the beginning. 
```javascript
var ref = new Firebase("https://xxx.firebaseio.com/");
var messagesRef = ref.child('messages');

scope.messages = $firebaseArray(messagesRef);

scope.sendMessage = function() {
  scope.messages.$add({
    body: scope.messageInput
  });
  scope.messageInput = '';
};
```

[Thinkster tutorial]: <https://github.com/JonasRafn>
[SimpleChat]:<https://github.com/JonasRafn/SimpleChatSocket>