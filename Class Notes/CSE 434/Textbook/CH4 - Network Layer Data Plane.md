202411131925
Meta Tags: #idea 
Tags:

# CH4 - Network Layer Data Plane

## 4.2 What's Inside a Router?

![[Pasted image 20241113192637.png]]
> High-level view of a generic router architecture

>[!info] input ports
>- Performs the physical layer function of terminating an incoming physical link at the router, leftmost box of input port and rightmost box of output port
>- Performs link-layer functions needed to interoperate with the link layer at the other side of the incoming link, middle boxes of I/O ports
>- Perform lookup function at rightmost box of input port: where forwarding table is consulted to determine the router output port to which an arriving packet will be forwarded via the switching fabric
>
>Note that "ports" here—referring to the physical I/O router interfaces—are distinctly different from the software ports associated w/ network applications and sockets.

>[!info] switching fabric
>Connects the router's input ports to its output ports, completely contained within the router (a network inside of the network router).

>[!info] output port
>Store packets received from the switching fabric and transmits these packets on the outgoing link by performing the necessary link-layer and physical-layer functions. When a link is bidirectional, an output port will typically be paired with the input port for that link on the same line card.

>[!info] routing processor
>Performs control-plane functions.
>
>- traditional: executes routing protocols, maintains routing tables and attached link state information, and computes the forwarding table for the router
>- SDN: communicates with remote controller in order to receive forwarding table entries computed by the remote controller, and install these entries in the router's input ports.
>  
>  Also performs network management functions.







---
# *References*