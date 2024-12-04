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

### Channel Partitioning Protocols

FDM and TDM:

![[Pasted image 20241203140953.png]]

The above both have the problem that a node is limited to a bandwidth of R/N, even when it is the only node with packets to send.

A third channel partitioning protocol is **code division multiple access (CDMA)**. CDMA assigns a different *code* to each node. Each node then uses its unique code to encode the data bits it sends. If the codes are chosen carefully, different nodes can transmit simultaneously and still have their respective receivers correctly receive the encoded data bits in spite of interfering transmissions by other nodes. 

### Random Access Protocols

A transmitting node always transmits at the full rate of the channel. When there is a collision, each node involved in the collision repeatedly retransmits the frame after waiting a independently random delay until it gets through without a collision. 

Examples: ALOHA, CSMA

### Taking-Turns Protocols

- **polling protocol**: requires one of the nodes to be designated as a master node. The master node **polls** each of the nodes in a round-robin fashion to transmit up to a maximum number of frames.
	- eliminates the collisions and empty slots that plague random access protocols
	- introduces a polling delay
	- if the master node fails, the entire channel becomes inoperative
	- Example: Bluetooth
- **token-passing protocol:** no master node; a small, special-purpose frame known as a **token** is exchanged among the nodes in some fixed order. When a node receives a token, it holds onto the token only if it has some frames to transmit; otherwise, it immediately forwards the token to the next node.
	- decentralized and highly efficient
	- failure of one node can crash the entire channel
	- if token is not released, recovery procedure must be invoked to get the token back in circulation
	- Example: FDDI, IEEE 802.5 token ring protocol

## 6.4 Switched Local Area Networks

![[Pasted image 20241203142051.png]]

- everything operates at the link layer
- routing algorithms like OSPF aren't used
- link-layer addresses instead of IP addresses

### Link-Layer Addressing and ARP

Hosts and routers do not have link-layer addresses—their **adapters** (NICs) have link-layer addresses. A host or router w/ multiple network interfaces will thus have multiple link-layer addresses associated with it, just as it would also have multiple IP addresses associated with it. 

Link-layer switches **do not** have link-layer addresses associated with their interfaces that connect to hosts and routers. This is because the job of the link-layer switch is to carry datagrams between hosts and routers; a switch does this job **transparently**, without the host or router having to explicitly address the frame to the switch.

![[Pasted image 20241203142502.png]]

A link-layer address is variously called a **LAN address**, a **physical address**, or a **MAC address**. 

No two adapters have the same address because IEEE manages the MAC address space.

An adapter's MAC address has a flat structure and doesn't change no matter where the adapter goes. In contrast, IP addresses have a hierarchical structure and need to be changed when the host moves to a different network.











---
# *References*