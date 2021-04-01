# Web Application & Software Architecture

## Different Tiers in Software Architecture
### Single Tier Applications
A single-tier application is an application where the user interface, backend business logic & the database all reside in the same machine.

Typical examples of single-tier applications are desktop applications like MS Office, PC Games or an image editing software like Gimp.

### Two Tier Applications
A Two-tier application involves a client and a server. The client would contain the user interface & the business logic in one machine. And the backend server would be the database running on a different machine. The database server is hosted by the business & has control over it.

### Three Tier Applications
Three-tier applications are pretty popular & largely used in the industry. Almost all of the simple websites like blogs, news websites etc. are part of this category.

So, if we take the example of a simple blog, the user interface would be written using Html, JavaScript, CSS, the backend application logic would run on a server like Apache & the database would be MySQL. A three-tier architecture works best for simple use cases.

### N-Tier Application
An application which has more than three components involved, these components could be:
* Cache
* Message queues for asynchronous behaviour
* Load balancers
* Search servers for searching through massive amounts of data
* Components involved in processing massive amounts of data
* Components running heterogeneous tech commonly known as web services etc.

All the social applications like Instagram, Facebook, large scale industry services like Uber, Airbnb, online massive multiplayer games like Pokemon Go, applications with fancy features are n-tier applications.

## Web Architecture

### Web Sockets
A Web Socket connection is ideally preferred when we need a persistent bi-directional low latency data flow from the client to server & back.

Typical use-cases of these are messaging, chat applications, real-time social streams & browser-based massive multiplayer games which have quite a number of read writes in comparison to a regular web app.

With Web Sockets, we can keep the client-server connection open as long as we want.

Have bi-directional data? Go ahead with Web Sockets. One more thing, Web Sockets tech doesn’t work over HTTP. It runs over TCP. The server & the client should both support web sockets or else it won’t work.

### Client-Side Vs Server-Side Rendering
When a user requests a web page from the server & the browser receives the response. It has to render the response on the window in the form of an HTML page.

To avoid all this rendering time on the client, developers often render the UI on the server, generate HTML there & directly send the HTML page to the UI.

This technique is known as the Server-side rendering. It ensures faster rendering of the UI, averting the UI loading time in the browser window since the page is already created & the browser doesn’t have to do much assembling & rendering work.

The server-side rendering approach is perfect for delivering static content, such as WordPress blogs. It’s also good for SEO as the crawlers can easily read the generated content.

However, the modern websites are highly dependent on Ajax. In such websites, content for a particular module or a section of a page has to be fetched & rendered on the fly.

Client-side rendering works best for modern dynamic Ajax-based websites.

Though we can leverage a hybrid approach, to get the most out of both techniques. We can use server-side rendering for the home page & for the other static content on our website & use client-side rendering for the dynamic pages.

## Scalability
Scalability means the ability of the application to handle & withstand increased workload without sacrificing the latency.

For instance, if your app takes x seconds to respond to a user request. It should take the same x seconds to respond to each of the million concurrent user requests on your app.

### Vertical scaling
Vertical scaling means adding more power to your server. Let’s say your app is hosted by a server with 16 Gigs of RAM. To handle the increased load you increase the RAM to 32 Gigs. You have vertically scaled the server.

Ideally, when the traffic starts to build upon your app the first step should be to scale vertically. Vertical scaling is also called scaling up.

In this type of scaling we increase the power of the hardware running the app. This is the simplest way to scale since it doesn’t require any code refactoring, not making any complex configurations and stuff. 

But there is only so much we can do when scaling vertically. There is a limit to the capacity we can augment for a single server.

### Horizontal scaling
Horizontal scaling, also known as scaling out, means adding more hardware to the existing hardware resource pool. This increases the computational power of the system as a whole.

Now the increased traffic influx can be easily dealt with the increased computational capacity & there is literally no limit to how much we can scale horizontally assuming we have infinite resources. We can keep adding servers after servers, setting up data centres after data centres.

Horizontal scaling also provides us with the ability to dynamically scale in real-time as the traffic on our website increases & decreases over a period of time as opposed to vertical scaling which requires pre-planning & a stipulated time to be pulled off.

### Which appoarch is for you?
If your app is a utility or a tool which is expected to receive minimal consistent traffic, it may not be mission-critical. For instance, an internal tool of an organization or something similar.

Why bother hosting it in a distributed environment? A single server is enough to manage the traffic, go ahead with vertical scaling when you know that the traffic load would not increase significantly.

If your app is a public-facing social app like a social network, a fitness app or something similar, then the traffic is expected to spike exponentially in the near future. Both high availability & horizontal scalability is important to you.

Build to deploy it on the cloud & always have horizontal scalability in mind right from the start.

### Primary Bottlenecks

#### Database
Just like the workload scalability, the database needs to be scaled well.

Make wise use of database partitioning, sharding, use multiple database servers to make the module efficient.

#### Application Architecture
A common architectural mistake is not using asynchronous processes & modules where ever required rather all the processes are scheduled sequentially.

For instance, if a user uploads a document on the portal, tasks such as sending a confirmation email to the user, sending a notification to all of the subscribers/listeners to the upload event should be done asynchronously.

These tasks should be forwarded to a messaging server as opposed to doing it all sequentially & making the user wait for everything.

#### Not using Caching
Caching can be deployed at several layers of the application & it speeds up the response time by notches. It intercepts all the requests going to the database, reducing the overall load on it.

Use caching exhaustively throughout the application to speed up things significantly.

#### Picking right Database
Picking the right database technology is vital for businesses. Need transactions & strong consistency? Pick a Relational Database. If you can do without strong consistency rather need horizontal scalability on the fly pick a NoSQL database.

Trying to pull off things with a not so suitable tech always has a profound impact on the latency of the entire application in negative ways.

#### Bad Code
* Using unnecessary loops, nested loops.
* Writing tightly coupled code.
* Not paying attention to the Big-O complexity while writing the code. Be ready to do a lot of firefighting in production.

## Load Balancing
Load balancers distribute heavy traffic load across the servers running in the cluster based on several different algorithms. This averts the risks of convergence of all the traffic on the service to a single or a few machines in the cluster.

Load balancers can also be setup to efficiently manage traffic directed towards any component of the application be it the backend application server, database component, message queue or any other. This is done to uniformly spread the request load across the machines in the clusters powering that respective component.

Ideally, a load balancer maintains a list of machines that are up and running in the cluster in real-time & the user requests are forwarded to only those machines that are in service. If a machine goes down it is removed from the list.

## Monolithic Architecture
An application has a monolithic architecture if it contains the entire application code in a single codebase.

Monolithic applications are simple to develop, test, deploy, monitor and manage since everything resides in one repository.

There is no complexity of handling different components, making them work in conjunction with each other, monitoring several different components & stuff. Things are simple.

Continuous deployment is a pain in case of monolithic applications as even a minor code change in a layer needs a re-deployment of the entire application.

The downside of this is that we need a thorough regression testing of the entire application after the deployment is done as the layers are tightly coupled with each other. A change in one layer impacts other layers significantly.

Building complex applications with a monolithic architecture is tricky as using heterogeneous technologies is difficult in a single codebase due to the compatibility issues.

Generally, monolithic applications are not cloud-ready as they hold state in the static variables. An application to be cloud-native, to work smoothly & to be consistent on the cloud has to be distributed and stateless.

Monolithic applications fit best for use cases where the requirements are pretty simple, the app is expected to handle a limited amount of traffic. One example of this is an internal tax calculation app of an organization or a similar open public tool.

These are the use cases where the business is certain that there won’t be an exponential growth in the user base and the traffic over time.

## Microservice Architecture
In a microservices architecture, different features/tasks are split into separate respective modules/codebases which work in conjunction with each other forming a large service as a whole.

This particular architecture facilitates easier & cleaner app maintenance, feature development, testing & deployment in comparison to a monolithic architecture.

Also, since the project is large, it is expected to be managed by several different teams. When modules are separate, they can be assigned to respective teams with minimum fuss, smoothening out the development process.

And did I bring up scalability? To scale, we need to split things up. We need to scale out when we can’t scale up further. Microservices architecture is inherently designed to scale.

Since microservices is a loosely coupled architecture, there is no single point of failure. Even if a few of the services go down, the application as a whole is still up.

Every component interacts with each other via a REST API Gateway interface. The components can leverage the polyglot persistence architecture & other heterogeneous technologies together like Java, Python, Ruby, NodeJS etc.

Polyglot persistence is using multiple databases types like SQL, NoSQL together in an architecture. 

Microservices is a distributed environment, where there are so many nodes running together. Managing & monitoring them gets complex.

The microservice architecture fits best for complex use cases and for apps which expect traffic to increase exponentially in future like a fancy social network application.

A typical social networking application has various components such as messaging, real-time chat, LIVE video streaming, image uploads, Like, Share feature etc.

## Databases
### Structured Data
There is no need to run any sort of data preparation logic on structured data before processing it. Direct interaction can be done with this kind of data.

An example of structured data would be the personal details of a customer stored in a database row. The customer id would be of integer type, the name would be of String type with a certain character limit etc.

So, with structured data, we know what we are dealing with. Since the customer name is of String type, without much worry of errors or exceptions, we can run String operations on it.

Structured data is generally managed by a query language such as SQL (Structured query language).

### Unstructured Data 
Unstructured data has no definite structure. It is generally the heterogeneous type of data comprising of text, image files, video, multimedia files, pdfs, Blob objects, word documents, machine-generated data etc.

This kind of data is often encountered in data analytics. Here the data streams in from multiple sources such as IoT devices, social networks, web portals, industry sensors etc. into the analytics systems.

We cannot just directly process unstructured data. The initial data is pretty raw, we have to make it flow through a data preparation stage which segregates it based on some business logic & then runs the analytics algorithms on it.

### Semi-structured Data

Semi-structured data is a mix of structured & unstructured data. Semi-structured data is often stored in data transport formats such as XML or JSON and is handled as per the business requirements.

### Relational Database
This is the most common & widely used type of database in the industry. A relational database saves data containing relationships. One to One, One to Many, Many to Many, Many to One etc. It has a relational data model. SQL is the primary data query language used to interact with relational databases.

MySQL is the most popular example of a relational database. 

If you are writing a stock trading, banking or a Finance-based app or you need to store a lot of relationships, for instance, when writing a social network like Facebook. Then you should pick a relational database.

### NoSQL Databases
As the name implies NoSQL databases have no SQL, they are more like JSON-based databases built for Web 2.0

They are built for high frequency read & writes, typically required in social applications like Twitter, LIVE real-time sports apps, online massive multi-player games etc.

Scaling relational databases is something which is not trivial. They have to be Sharded or Replicated to make them run smoothly on a cluster. In short, this requires careful thought and human intervention.

On the contrary, NoSQL databases have the ability to add new server nodes on the fly & continue the work, without any human intervention, just with a snap of the fingers.

### When to pick NoSQL
Look towards NoSQL databases when you need to scale fast. And when do you generally need to scale fast?

When there are a large number of read-write operations on your website & when dealing with a large amount of data, NoSQL databases fit best in these scenarios. Since they have the ability to add nodes on the fly, they can handle more concurrent traffic & big amount of data with minimal latency.

The second cue is during the initial phases of development when you are not sure about the data model, the database design, things are expected to change at a rapid pace. NoSQL databases offer us more flexibility.

### Document Orientated Databases
Document Oriented databases are the main types of NoSQL databases. They store data in a document-oriented model in independent documents. The data is generally semi-structured & stored in a JSON-like format.

Some of the popular document-oriented stores used in the industry are MongoDB, CouchDB, OrientDB, Google Cloud Datastore, Amazon Document DB.

If you are working with semi-structured data, need a flexible schema which would change often. You ain’t sure about the database schema when you start writing the app. There is a possibility that things might change over time. You are in need of something flexible which you could change over time with minimum fuss. Pick a Document-Oriented data store.

### Graph Database
Graph databases are also a part of the NoSQL database family. They store data in nodes/vertices and edges in the form of relationships.

Each Node in a graph database represents an entity. It can be a person, a place, a business etc. And the Edge represents the relationship between the entities.

Primarily, two reasons. The first is visualization. Think of that pinned board in the thriller detective movies where the pins are pinned on a board over several images connected via threads. It does help in visualizing how the entities are related & how things fit together. Right?

The second reason is the low latency. In graph databases, the relationships are stored a bit differently from how the relational databases store relationships.

Graph databases are faster as the relationships in them are not calculated at the query time, as it happens with the help of joins in the relational databases. Rather the relationships here are persisted in the data store in the form of edges and we just have to fetch them. No need to run any sort of computation at the query time.

A good real-life example of an application which would fit a graph database is Google Maps. Nodes represent the cities and the Edges represent the connection between them.

Now, if I have to look for roads between different cities, I don’t need joins to figure out the relationship between the cities when I run the query. I just need to fetch the edges which are already stored in the database.

Ideal use cases of graph databases are building social, knowledge, network graphs. Writing AI-based apps, recommendation engines, fraud analysis app, storing genetic data etc.

### Key Value Database
Key-value databases also are a part of the NoSQL family. These databases use a simple key-value method to store and quickly fetch the data with minimum latency.

A primary use case of a Key-value database is to implement caching in applications due to the minimum latency they ensure.

The Key serves as a unique identifier and has a value associated with it. The value can be as simple as a block of text & can be as complex as an object graph.

The data in Key-value databases can be fetched in constant time O(1), there is no query language required to fetch the data. It’s just a simple no-brainer fetch operation. This ensures minimum latency.

Some of the popular key-value data stores used in the industry are Redis, Hazelcast, Riak, Voldemort & Memcache.

If you have a use case where you need to fetch data real fast with minimum fuss & backend processing then you should pick a key-value data store.

Key-value stores are pretty efficient in pulling off scenarios where super-fast data fetch is the order of the day.

Typical use cases of a key value database are the following:
* Caching
* Persisting user state
* Persisting user sessions
* Managing real-time data
* Implementing queues
* Creating leaderboards in online games & web apps
* Implementing a pub-sub system

## Caching
Caching is key to the performance of any kind of application. It ensures low latency and high throughput. An application with caching will certainly do better than an application without caching, simply because it returns the response in less time as opposed to the application without a cache implemented.

Implementing caching in a web application simply means copying frequently accessed data from the database which is disk-based hardware and storing it in RAM Random Access Memory hardware.

Across the architecture of our application, we can use caching at multiple places. Caching is used in the client browser to cache static data. It is used with the database to intercept all the data requests, in the REST API implementation etc.

Besides these places, I would suggest you to look for patterns. We can always cache the frequently accessed content on our website, be it from any component. There is no need to compute stuff over and over when it can be cached.

## Message Queue
Follows the FIFO (First in First Out) policy. The message that is sent first is delivered first. Though messages do have a priority attached with them that makes the queue a priority queue but for now let’s keep things simple.

### Publish Subscribe Model
A Publish-Subscribe model is the model where multiple consumers receive the same message sent from a single or multiple producers.

To implement the pub-sub pattern, message queues have exchanges which further push the messages to the queues based on the exchange type and the rules which are set. Exchanges are just like telephone exchanges which route messages from sender to the receiver through the infrastructure based on a certain logic.

## Stream Processing
Data can be ingested using both the real-time & the batch approach.

The data streaming into the system is heterogenous in nature & has to be converted into a standardized format. This conversion of data is a tedious process. It takes a lot of computing resources & time.

### Lambda Architecture
Lambda is a distributed data processing architecture that leverages both the batch & the real-time streaming data processing approaches to tackle the latency issues arising out of the batch processing approach. It joins the results from both the approaches before presenting it to the end user.

### Kappa Architecture
In Kappa architecture, all the data flows through a single data streaming pipeline as opposed to the Lambda architecture which has different data streaming layers that converge into one.

Kappa contains only two layers. Speed, which is the streaming processing layer, & the Serving which is the final layer.

Kappa is not an alternative for Lambda. Both the architectures have their use cases.

Kappa is preferred if the batch and the streaming analytics results are fairly identical in a system. Lambda is preferred if they are not.

## Event Driven Architecture
There are generally two kinds of processes in applications CPU intensive & IO intensive. IO in the context of web applications means events. A large number of IO operations mean a lot of events occurring over a period of time. And an event can be anything from a tweet to a click of a button, an HTTP request, an ingested message, a change in the value of a variable etc.

Non-blocking architecture is also known as the Reactive or the Event-driven architecture. Event-driven architectures are pretty popular in the modern web application development.

Technologies like NodeJS, frameworks in the Java ecosystem like Play, Akka.io are non-blocking in nature and are built for modern high IO scalable applications.

They are capable of handling a big number of concurrent connections with minimal resource consumption. Modern applications need a fully asynchronous model to scale. These modern web frameworks provide more reliable behaviour in a distributed environment. They are built to run on a cluster, handle large scale concurrent scenarios, tackle problems which generally occur in a clustered environment. They enable us to write code without worrying about handling multi-threads, thread lock, out of memory issues due to high IO etc.

Coming back to the Event-driven reactive architecture. It simply means reacting to the events occurring regularly. The code is written to react to the events as opposed to sequentially moving through the lines of codes.

Event-driven architecture is all about processing asynchronous data streams. The application becomes inherently asynchronous.

NodeJS is a single-threaded non-blocking framework written to handle more IO intensive tasks. It has an event loop architecture. 

NodeJS is not fit for CPU intensive tasks. CPU intensive operations are operations that require a good amount of computational power like for graphics rendering, running ML algorithms, handling data in enterprise systems etc. It would be a mistake to pick NodeJS for these purposes.

### Web Hooks
WebHooks are more like call-backs. It’s like I will call you when new information is available. You carry on with your work.

WebHooks enable communication between two services without a middleware. They have an event-based mechanism.

To use the Webhooks, consumers register an HTTP endpoint with the service with a unique API Key. It’s like a phone number. Call me on this number, when an event occurs. I won’t call you anymore.

Whenever the new information is available on the backend. The server fires an HTTP event to all the registered endpoints of the consumers, notifying them of the new update.

### Peer to Peer Architecture
P2P architecture is the base of blockchain tech. We’ve all used it at some point in our lives to download files via torrent. 

A P2P network is a network in which computers also known as nodes can communicate with each other without the need of a central server. The absence of a central server rules out the possibility of a single point of failure. All the computers in the network have equal rights. A node acts as a seeder and a leecher at the same time. So, even if some of the computers/nodes go down, the network & the communication is still up.

I want you to think of a messaging app. When two users communicate, the first user sends a message from his device, the message moves on the server of the organization hosting the messaging service, from there the message is routed to the destination, that is, the device of the user receiving the message.

The server of the organization is the central server. These systems are also known as Centralized systems.

The central server has access to all your messages. It can read it, share it with its associates, laugh about it and so on. So, communication is not really secure. Even though the businesses say that the entire message pipeline is encrypted and stuff. But still, data breaches happen, governments get access to our data. Data is sold to third parties for fat profits

Fortunately, P2P networks are resilient to all these scenarios, due to their design. They have a Decentralized architecture.

Nobody has control over your data, nobody has the power to delete your data as all the participating nodes in a P2P network have equal rights. During a zombie apocalypse when the huge corporation servers would be dead or on fire, we can still communicate with each other via a peer to peer connection.

## Picking Right Server Side Technology

### Real-time Data Interaction
If you are building an app that needs to interact with the backend server in real-time like stream data to & fro. For instance, a messaging application, a real-time browser-based massive multiplayer game, a real-time collaborative text editor or an audio-video streaming app like Spotify, Netflix etc.

You need a persistent connection between the client and server, also you need a non-blocking technology on the back-end. We’ve already talked about both the concepts in detail.

Some of the popular technologies which enable us to write these apps are NodeJS, Python has a framework called Tornado. If you are working in the Java Ecosystem you can look into Spring Reactor, Play, Akka.io.

### Peer to Peer Web Application
If you intend to build a peer to peer web app, for instance, a P2P distributed search engine or a P2P Live TV radio service, something similar to LiveStation by Microsoft.

Look into JavaScript, protocols like DAT, IPFS. Checkout FreedomJS, it’s a framework for building P2P web apps that work in the modern web browsers.

### CRUD (Regular Application)
If you have simple use cases such as a regular CRUD-based app like online movie booking portal, a tax filing app etc.

CRUD (Create Read Update Delete) is the most common form of web apps being built today by businesses. Be it an online booking portal, an app collecting user data or a social site etc. all have an MVC (Model View Controller) architecture on the backend.

Though the view part is tweaked a little with the rise of UI frameworks by React, Angular, Vue etc. The Model View Controller pattern stays.

Some of the popular technologies which help us implement these use cases are Spring MVC, Python Django, Ruby on Rails, PHP Laravel, ASP .NET MVC.

### CPU & Memory Intensive Applications 
Do you need to run CPU Intensive, Memory Intensive, heavy computational tasks on the backend such as Big Data Processing, Parallel Processing, Running Monitoring & Analytics on quite a large amount of data?

Performance is critical in systems running tasks which are CPU & Memory intensive. Handling massive amounts of data has its costs. A system with high latency & memory consumption can blow up the economy of a tech company.

Also, regular web frameworks & scripting languages are not meant for number crunching.

Tech commonly used in the industry to write performant, scalable, distributed systems are –

C++, it has features that facilitate low-level memory manipulation. Provides more control over memory to the developers when writing distributed systems. Majority of the cryptocurrencies are written using this language.

Rust is a programming language similar to C++. It is built for high performance and safe concurrency. It’s gaining a lot of popularity lately amongst the developer circles.

Java, Scala & Erlang are also a good pick. Most of the large scale enterprise systems are written in Java.

Elastic search an open-source real-time search and analytics engine is written in Java.

Erlang is a functional programming language with built-in support for concurrency, fault-tolerance & distribution. It facilitates the development of massively scalable systems. This is a good read on Erlang

Go is a programming language by Google to write apps for multi-core machines & handling a large amount of data.

Julia is a dynamically programmed language built for high performance & running computations & numerical analytics.
