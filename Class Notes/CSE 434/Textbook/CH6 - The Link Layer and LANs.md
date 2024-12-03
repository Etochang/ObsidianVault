202412031332
Meta Tags: #textbook 
Tags: [[computer networking]]

# CH6 - The Link Layer and LANs

>- How are packets sent across the *individual links*?
>- How are network-layer datagrams encapsulated in the link-layer frames for transmission?
>- Are different link-layer protocols used in the different links along the same communication path?
>- How are transmission conflicts in broadcast links resolved?
>- Is there addressing at the link layer, and how would it operate with network-layer addressing?
>- What is the difference between a switch and a router?

There are two fundamentally different types of link-layer channels:

- Broadcast: connect multiple hosts in wireless LANs, satellite networks, and hybrid fiber-coaxial cable (HFC) access networks
- Point-to-point: between two nodes

## 6.1 Introduction to the Link Layer

>[!info] node 
>Any device that runs a link-layer protocol (hosts, routers, switches, WiFi access points, etc.)

>[!info] links
>The communication channels that connect adjacent nodes along the communication path

Over a given link, a transmitting node encapsulates the datagram in a **link-layer frame** and transmits the frame into the link. 

### Services Provided by the Link Layer

- *Framing*: A frame consists of a data field and a number of header fields. The frame structure is specified by the link-layer protocol. 
- *Link Access*: A medium access control (MAC) protocol specifies the rules by which a frame is transmitted onto the link.
- *Reliable Delivery*: Guarantees to move each network-layer datagram across the link w/o error. Often used for links that are prone to high error rates to avoid end-to-end retransmission of data, sometimes unnecessary overhead.
- *Error Detection and Correction*: Usually more sophisticated in the link layer and is implemented in hardware.

### Where is the Link Layer Implemented❔

![[Pasted image 20241203135026.png]]

The link layer is usually implemented on the **network adapter**, also sometimes known as a **network interface controller (NIC)**. 

On the sending side, the controller takes a datagram from the higher layers of the protocol stack, encapsulates it in a link-layer frame, and then transmits the frame into the communication link following the link-access protocol. 

On the receiving side, a controller receives the entire frame, extracts the network-layer datagram, and sends it upwards on the protocol stack.

The link layer is a combination of hardware and software.

## 6.3 Multiple Access Links and Protocols

>[!info] point-to-point link
>Single sender at one end of the link and a single receiver at the other end of the link.

>[!info] broadcast link
>Can have multiple sending and receiving nodes connected to the same shared broadcast channel.

Broadcast implies that when any one node transmits a frame, the channel broadcasts the frame and each of the other nodes receives a copy. 

The **multiple access problem**: how to coordinate the access of multiple sending and receiving nodes to a shared broadcast channel.

The **multiple access protocol**: how nodes regulate their transmission into the shared broadcast channel.

When nodes receive multiple frames at the same time, the transmitted frames **collide** at all of the receivers. Typically, this means that none of the receivers can understand any of the colliding frames.

Multiple access protocols can generally be classified into three categories:

- Channel Partitioning
- Random Access
- Taking-Turns

Ideally, a multiple access protocol for a broadcast channel of rate *R* should have the following characteristics:

1. When only one node has data to send, that node has a throughput of R bps.
2. When M nodes have data to send, each of these nodes has a throughput of R/M bps. This need not necessarily imply that each of the M nodes always has an instantaneous rate of R/M, but rather that each node should have an average transmission rate of R/M over some suitably defined interval of time.
3. The protocol is decentralized; that is, there is no master node that represents a single point of failure for the network.
4. The protocol is simple, so that it is inexpensive to implement.












---
# *References*