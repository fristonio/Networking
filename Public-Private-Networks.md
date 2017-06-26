# Private Networks :

Every system on the network needs a unique identifier with which it can be identified over the whole network. IP address serves as this identifier. Now as such, every system that accesses the Internet would need a unique IP address.
But in case of IPv4 there are actually not enough address availabe for all those who are accessing internet. To cope with this the concept of private IP address was introduced.
 
Three blocks of IP addresses were set aside as private, meaning that all of the router on the internet would be configured not to route them, they are therefore also reffered as **non-routable**. The question arises how does they solve our problem? Now since these private address weren't routed so all of the networks on the internet can use the same private address because it can never be discovered that they weren't unique. 

Now the question is, if these addresses weren't routed then how a particular system is identified over the internet. Address resolution solves this problem. These private address are assigned under a network and these networks have to be assigned a routable **public** IP. So all the systems connected to this network are assigned a unique private IP and they all shares a single **public** address to access teh internet. For this all system are configured to use a special server, called a PROXY SERVER.

A proxy server has two NICs(Network Interface Cards) since it is connected to two different network itself one to connect to interned which is assigned the public IP and the other is connected to the internal network.