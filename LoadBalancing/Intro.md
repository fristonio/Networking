# Introduction

Load balancing is the distribution of workloads across compute resources, it aims to optimize throughput and resource usage. There are various mechanisms of load balancing involved when it comes to multi cluster multi region application deployment. In laymen terms load balancer serves a simple purpose of distributing multiple clients among multiple servers.

Load balancing can be done on both hardware level and software level, while the throughput provided by hardware load balancing is much more as compared to software load balancing, it does not provide much scope of reconfigurability and are quite expensive.

Some minimal tasks a load balancer should be capable of doing is
* **Service Discovery** - Finding out the exact location of the service to direct the request to.
* **Health Checking** - This is quite necessery when we are trying to create a highly available service, this is done to make sure that we don't route request to a server which is non responsive.
* **Load Balancing** - This refers to the core algorithm and mechanism involved in the actual process.

A network load balancer deals with load balancing of network packets. The lifecycle of a normal network packet is

* A packet is recieved on the network interface, which is a physical connection to the network.
* The network card recieves the frame and issues an interrupt
* The device driver handles the interrupt, this copies the packet from frame to RAM and allocates a `sk_buff` for the recieved packet. The packet is transferred to `rx_ring` through DMA.
* `skb` is a generalized packet buffer, while handling the packet the the pointer to this skb is passed up and down.
* This buffer is then passed on to the CPU queue, and a soft interrupt is issued. This is the RX_Queue

From hereon the packet is handeled by the Kernel TCP/IP stack, which process the packet and then pass it on to the userland application.

In terms of networking a load balancer is a device which recieves a network packet sends it to once of the service where it can be used for processing. This transmission of packet to a service can be done at various level or after various levels of packet parsing in the TCP/IP stack, this leads to the need and existance of various types of load balancer:

### L4 Load balancing

L4 here refers to Layer 4 of the OSI networking model, this type of load balancing solution deals with traditional layer 4 protocols like TCP and UDP. In this technique the packet is parsed up to Layer 4 and then passed to the required service as a backend. This type is not aware of any of the application level details of the data. This type of load balancer can further be classified into various types on the basis of the connection handling technique.

**Termination**

In this type of load balancing two different connections are used, one from client to the load balancer and other from the load balancer to the actual backed application service. Essentially in the process of requesting a resource from service the request is first handled by the load balancer which in turn uses a seperate request to get that resource from clients behalf from the server.

**Passthrough**

Termination load balancers are not very resourceful since they use two seperate connection which creates additional overhead in packet handling. A better alternative to approach load balancing is using a passthrough technique.
In pass through load balancing the packets are forwarded to the service after doing a Network Address Translation(NAT), to make sure that packets corresponding to same request reach the same server connection-tracking is used. The overhead of making an additional request is reduced in this case.

![PassThrough Load Balancing](/Resources/lb_passthrough.png)

**Direct Server Return(DSR)**

Building on the concept of PassThrough load balancer DSR load balancer are built, while traditional pass through load balancer uses load-balancer for both ingress and egress of packet, DSR directly sends the packet to the client without sending it back to the load balancer, this reduces additional overhead faced by load balancer where it process egress packets(90% of req-resp cycle) along with ingress packets.

Using DSR load balancer is less loaded as compared to simple pass through. Since for DSR to work the service needs to know about the client IP, rather than using NAT we use GRE(Generic Routing encapsulation) to encapsulate the packets sent from the load balancer to the backend service.

![DSR load balancer](/Resources/lb_dsr.png)


### L7 bLoad balancing

This type of load balancing is more commonly referred to as **Application Load Balancing**. Layer7 provides a more verbose way to process request and analyze them, using these types of load balancer we can easily identify and thus distinguish between various application level protocols, like HTTP, GRPC etc.

With the added benifit of verbosity comes the additional overhead of parsing the network packets up to the application layer or Layer7.
