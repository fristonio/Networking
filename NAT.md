# NAT

NAT stands for Network Address Translation, it is a method of remapping one IP address space into another by moodifying network address information in Internet Protocol(IP) datagram packet headers while they are in transit across a traffic routing device.

The need for an IP Address translation arises when a network's internal IP address cannot be used outside the network as they are invalid outside and because the internal addressing must be kept private from the external network.

**Address Realm**

It is a network domain in which the network address are uniquely assigned to entities such that datagrams can be routed to them. 

**Transparent Routing :**

It identify the routing functionality that a NAT device provides. This is different from the routing functionality of the traditional router device. In tranditional routers the router routes the packets within a single address realm, whereas in trasparent routing the datagram is routed between different address realm by modifying address content in the IP header.

A NAT router sits at the border between two address realms and translates address in IP headers so that when the packet leaves one realm and enters another, it can be routed properly.

There are three phases to address translation which result in the maintainence creation and termination of state for session passing through NAT devices which are :

**Address Binding :**

In this phase a local node IP address is associated with an external address for the purposes of translation. This address assignment can be of two types.
    * Static address assignment
    * Dynamic address Assignment

After binding all the subsequent sessions originating from or to this host will use the same binding for session based packet translation.

**Address lookup and Translation :**

After the binding all packets belonging to the session will go through the process of address lookup and translation which results in datagram forwarding from the origin address realm to destination address realm

**Address Unbinding :**

NAT performs unbinding when it realises that the last session using an address binding has terminated, unbinding produces a phase in which a private address is no longer associated with a global address fro purposes of translation.

```
                                 ________________
                                 (                )
                                (   External       )    +--+
                               (  Address Realm     )-- |__|
                                (     (N-Ext)      )   /____\
                                 (________________)    Host-X
                                        |              (Addr-X)
                                        |(Addr-Nx)
                           +--------------+
                           |              |
                           |  NAT router  |
                           |              |
                           +--------------+
                             |(Addr-Np)
                             |
                     ----------------
                    (                )
        +--+       (     Private      )
        |__|------(    Address Realm   )
       /____\      (     (N-pri)      )
       Host-A       (________________)
       (Addr-A)
```

### NAT Flavours

**Traditional NAT(Outbound NAT)**

Such NATs sessions are Unidirectional, outbound from the private network. Since IP addresses of hosts in external networks are unique and valid in external as well as private networks so NAT would not advertise private network to the external realm but network from external realms can be advertised within the private network. There are two variations to Traditional NATs Basic NATs and NAPT(Network address port translation).

Traditional NAT are designed to handle only outbound transactions that is, client on the local network initiate requests and devices on the internet send back resoponses.

**Bi-Directional NATs or Two Way NATs**

In such NATs sessions can be initiated from the hosts in public network as well as the private network. Inbound transactions are more difficult as compared to outbound transactions this is because of the fact that the inside network generally knows th IP address of the outside devices, since the are in public but the outside network doesn't know the private address of the inside network, moreover since private ip are non routable external hosts cannot get to the private network's local router.

There are only two ways to resolve the hidden address problem. One is to use the static mapping for devices like server on inside network that need to be accessed from outside. Using static mapping the global address of the device that is using static mapping will be publicly known which solves the problem.

The other solution is to use DNS. Since it allows requests to be sent as names instead of IP addresses the DNS servers translates these names to their corresponding address. The use of DNS with NAT can solve our problem the basic process being :

* The external realm source sends a DNS request.
* The DNS server for the internal network resolves the request to name to an inside local address.
* The inside local address is passed to NAT and used to create a dynamic mapping between the inside local address of the server and inside global address. This mapping is put into the NAT router's translation table through which the communication  takes place.
* For sending response the response is send to NAT, NAT sees the inside local address and replaces it with inside global address using the table maintained and routes back to outside client.

[Working of a Bi-Directional NAT](http://www.tcpipguide.com/free/t_IPNATBidirectionalTwoWayInboundOperation-3.htm)
