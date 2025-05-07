# Advanced Programming Module 8

## Module 08 - High Level Networking

### Reflection

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
```

In the unary streaming RPC method, the client only sends one request to the server and the server sends one response back. The server has to wait for a request from the client before sending a response.
It's suitable in scenarios where the client needs to make only one stand-alone simple requests without further data exchanges or interactions. For example, authenticating one user, fetching data from a database and single form submissions.

In the server streaming RPC method, the server is able to send a stream of responses for a single client request. The server can send large amounts of data in the form of a stream of small data packets.
It's suitable in scenarios where the client needs to receive data updates continuously or a large amount of data. For example, it can be used for real-time updates such as weather data, stock market prices, news feeds, notification updates and money exchange values.

In the Bi-directional streaming RPC method, both the client and server can send continuous streams of data to each other simultaneously.
It is suitable for scenarios where there is real-time, asynchronous data exchange between both parties such as multiplayer games, collaborative editing and chat applications.
```

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
```
In order for a gRPC service to be secure, it requires mechanisms that enforce authentication and authorization of users involved and data encryption of sent packets.

Regaring authentication, the clients identity needs to be verified to ensure that the gRPC service's users can only use it. This prevents unwanted third parties from accessing or altering private data. Such mechanisms to achieve this include: API keys, mutual Transport Layer Security (TLC), OAuth, API keys and JWT tokens.

Authorization is required for data integrity and confidentiality as it protects private data from being accessed or modified by authenticated users who are not authorized. The following methods: Attribute-Based Access Control (ABAC), Role-Based Access Control (RBAC) and CUstom Access Control Lists (ACLs) can be used to prevent data leaks, security breaches and unintended operations from being performed on private data.

As for data encryption, the data packets before being sent to their destination must be encrypted. This prevents packet sniffing, data injection by unwanted third parties and ensures that the data can only be accessed by the parties involved in the data exchange. Encryption algorithms and TLS can be used to implement this.
```

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios live chat applications?
```
There are multiple aspects to consider when implementing gRPC, they include: security, synchronization and concurrency, errors, reliability scalability and performance.

The live chat application needs to be secure and ensure that the data exchanged is kept confidential and maintains integrity while preventing third parties from interacting with the data.

Ensuring good synchronization and concurrency management can be challenging when there are multiple users communicating on the app at the same time. Error handling must be implemented to ensure that the users can have a smoother experience using the app or communicating.

The application should be able to handle multiple users communicating at the same time and should be able to accommodate a growing number of active users. Moreover, no data packets should be lost during transmission and communication must be able to be done quickly in real-time. 
```

4. What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?
```
One advantage of using the line of code above is compatibility with the tokio module, leading to wider stream modifications, applications and access to asynchronous and await runtimes. Moreover this leads to faster data handling as Rust gRPC services can have better performance and handle large amounts of data streams with pipelines.

As for disadvantages, it can increase complexity due to its asynchronous nature which can be complicated when the gRPC service must accommodate many clients.
Additionally, methods to improve the service must be implemented such as data encryption for security and error handling for better user experience.
```

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
```
The mentioned aspects above can be achieve by applying modularity and following these SOLID prinicples :
    1. Single Responsibility Principle (SRP)
    2. Open Closed Principle (OCP)
    3. Liskov Substitution Principle (LSP)
    4. Interface Segregation Principle (ISP)
    5. Dependency Inversion Principle (DIP)

Different parts of the code can be seperated into their own modules with their own specific functions, promoting SRP and modularity. For instance, initializing ChatService, PaymentService and TransactionService into their own modules.

Next, to implement LSP, OCP and ISP. The same functions from all modules involving gRPC services can be put into a general module, allowing it to be extended and reused. Moreover, each module will have their own interface on top of this module with their specific methods and traits, promoting ISP and DIP. Having separate interfaces for each module enhances maintainability and makes it easier to test for bugs, it also enforces LSP and OCP as the interfaces can be modified without altering the general module.
```

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
```
Methods that improve security such as data encryption, validation, authorization, authentication, compliance to rules checks and fraud detection can be implemented. This ensures that only authenticated and authorized clients can process reliable and safe transactions with each other while protecting sensitive user data.
Additionally, logging and error handling can help check for bugs, keep track of transactions, ensure a smoother transaction service for users and check for breaches in security.
To further improve the user experience and performance, asynchronous programming and stream-based processing can be employed. This enables the server to process multiple payment requests concurrently.
If external payment systems are involved then the code needs to integrate and be compatible with those systems' APIs and libraries.
```

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
```
There are multiple impacts tha arise from adopting gRPC as a communication protocol. For instance, it enables a more, simplier, efficient and faster connections with services that is language agnostic.

Using gRPC provides, scalable and faster communication and support for multiple requests at the same time as it uses HTTP/2 which is more efficient than using HTTP calls.
It also makes development easier by generating client and server code from .proto files, reducing boilerplate code and ensuring consistency across services.
It provides high interoperability with other technologies and platforms that are written in different programming languages as gRPC is widely supported in non-Rust languages. This is enabled by Protocol Buffers which allow clients and servers on different platforms to be able to communicate and understand each other.
Lastly, it is more simpler than HTTP calls which allows for faster development time due to its simple and straightforward nature.
```

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
```
Some advantages of using HTTP/2 include better performance, scalablility, connection efficiency and lower latency from multiplexing, header compression, server push. Moreover, it is language agnostic allowing higher compatibility and applicability with different platforms and technologies in different progrmaming languages.

One advantages of using HTTP/2 is that requests and responses are not processed sequentially due to pipelines from multiplexing, unlike HTTP/1.1 which gives it a significant advantage over the latter.
Additionally, HTTP/2 can enhance performance with its binary protocol and binary framing layer that enable multiplexing. That can reduce overhead and improve data encoding compared to HTTP/1.1's text-based format.
HTTP/2's server push also improves performance and connection efficiency between clietns and servers. This lets the server send resources to the client before receiving client requests.
Header compression from HTTP/2's HPack can reduce size of transmitted data as they only allow necessary data in the header. This improves responsiveness and frees more bandwith resources in communication.

A disadvantage of using HTTP/2 is higher complexity due to its features such as header compression and multiplexing. Extra tests may need to be conducted or more complicated code implemented to accommodate these features.
Another downside is that HTTP/2 is not compatible with or supported by all platforms or systems, which reduces its application and inoperability with such legacy systems.
Lastly, HTTP/1.1 consumes less server resources than HTTP/2 when there are many concurrent connectionsm, so performance and costs need to be considered when implementing HTTP/2.
```

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
```
Compared to the bidirectional streaming capabilities of gRPC, REST APIs require establishing new connections for every client request. This  makes it not suitable for real-time communication and increases latency and network head due to its model.
Unlike with the bidirectional streaming capabilities of gRPC which only requires one connection from the client to send continuous streams of data which reduces latency and reduces network head. This makes it suitable for real-time communication with its streaming ability and persistent connections.
```

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
```
Protocol buffers enable automatic generation of client libraries and interfaces, which enables efficient and compact serialization and deserialization of binary messages unlike JSON. This improves network performance and frees more bandwith resources. Moreover, it allows interoperability in different services and platforms due to its language agnostic nature leading to wider applications between services.
Protocol Buffers also ensure type safety and error validation so messages sent are always valid making communication reliable.

On the other hand, JSON in REST API do not have type safety. However, it is more flexible and less restrictive due to its human-readable format and lack of a strict schema. It can easily handle dynamic or evolving data structures without requiring regeneration of code, making it adaptable to changing APIs.
```