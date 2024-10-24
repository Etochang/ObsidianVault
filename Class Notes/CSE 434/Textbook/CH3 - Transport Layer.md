202410221216
Meta Tags: #textbook
Tags: [[computer networking]]

# CH3 - Transport Layer

- Provides communication services directly to the application processes running on different hosts.
	- extends network layer's delivery service between two end systems to a deliver service between two application-layer processes running on the end systems.
- how can two entities communicate reliably over a medium that may lose and corrupt data?
- how can the transmission rate of transport-layer entities be controlled to avoid/recover from congestion within the network?
	- What are the causes and consequences of congestion?
	- What are commonly used congestion-control techniques?

## 3-1 Introduction and Transport-Layer Services

Transport-layer protocol provides for **logical communication** between application processes running on different hosts. 

>[!info] logical communication
>From an application's perspective, it is as if the hosts running the processes were directly connected, disregarding the connections (routers/links) in between.
>
>Application processes send messages to each other, free from the worry of the details of the physical infrastructure used to carry these messages.
>
>![[Pasted image 20241022122229.png]]

As shown in the above figure, transport-layer protocols are implemented in the end systems but not the routers. 

On the sending side, the transport layer converts application-level messages into transport-layer segments, and then passes said segments to the network layer where the segment is encapsulated within a network-layer packet/datagram and sent to its destination. 

**Routers act only on the network-layer fields of the datagram**.

On the receiving side, the network layer extracts the transport-layer segment from the datagram and passes it up to the transport layer, which then processes the received segment, making the data in the segment available to the receiving application.

### 3-1-1 Relationship Between Transport and Network Layers

The services that a transport protocol can provide are often constrained by the service model of the underlying network-layer protocol. If the network-layer protocol cannot provide delay or bandwidth guarantees for transport-layer segments sent between hosts, then the transport-layer protocol cannot provide delay or bandwidth guarantees for application messages sent between processes.

Nevertheless, certain services *can* be offered by a transport protocol even when the underlying network protocol doesn't offer the corresponding service at the network layer (e.g., reliable data transfer, encryption).

### 3-1-2 Overview of the Transport Layer in the Internet

- **UDP** (User Datagram Protocol) = provides unreliable, connectionless service to invoking application
- 



---
# *References*