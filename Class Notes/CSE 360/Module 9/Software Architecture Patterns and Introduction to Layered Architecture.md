202406162151
Meta Tags: #class
Tags: [[Software Architecture]]

# Software Architecture Patterns and Introductions to Architectures

## Architectural patterns

- similar to design patterns, used to represent, share and reuse knowledge.
- An architectural pattern is a stylized description of good design practice
- should include info about when they are and when they aren't useful
- may be represented using tabular and graphical descriptions

1. Layered Pattern
2. Client-Server Pattern
3. Event-Driven Pattern
4. Service Oriented Pattern
5. Microservices Pattern
6. Model-View-Controller
7. ModelView-ViewModel

## A Generic Layered Architecture

- organizes the system into a set of layers (or abstract machines) each of which provide a set of services.
- Supports the incremental development of sub-systems in different layers; when a layer interface changes, only the adjacent layer is affected.
- Each layer provides services for the layer above
- inefficient since goes from user layer to hardware layer

## Client-Server Architecture

- distributed system model which shows how data and processing is distributed across a range of components
	- can be implemented on a single computer
- set of stand-alone servers which provide specific services such as printing, data management, etc.
- set of clients which call on these services
- network which allow clients to access servers
- distributes functionality
- the functionality of the system is organized into services, with each service delivered from a separate server. Clients are users of these services and access servers to make use of them
- used when data in a shared database has to be accessed from a range of locations. Because servers can be replicated, may also be used when the load on a system is variable.
- **Advantages:** servers can be distributed across a network; general functionality can be available to all clients and doesn't need to be implemented by all services.
- **Disadvantages:** each service is a single point of failure, so susceptible to DoS attacks or server failure; performance may be unpredictable because it depends on the network as well as the system. May be management problems if servers are owned by different organizations.

## MVC Architecture

![[Pasted image 20240616220900.png]]

- separates presentation and interaction from the system data. The system is structured into three logical components: the Model manages the system data and associated operations on that data; the View defines and manages how the data is presented to the user; the Controller manages user interaction and passes them to the View and the Model.
- used when there are multiple ways to view and interact with data. Also used when the future requirements for interaction and presentation of data are unknown
- **Advantages:** allows the data to change independently of its representation and vice versa. Supports presentation of the same data in different ways with changes made in one representation shown in all of them
- **Disadvantages:** can involve additional code and code complexity when the data model and interactions are simple.






---
# *References*