# Public-Private Networks :

Every system on the network needs a unique identifier with which it can be identified over the whole network. IP address serves as this identifier. Now as such, every system that accesses the Internet would need a unique IP address.
But in case of IPv4 there are actually not enough address availabe for all those who are accessing internet. To cope with this the concept of private IP address was introduced.
 
Three blocks of IP addresses were set aside as private, meaning that all of the router on the internet would be configured not to route them, they are therefore also reffered as **non-routable**. The question arises how does they solve our problem? Now since these private address weren't routed so all of the networks on the internet can use the same private address because it can never be discovered that they weren't unique. 

Now the question is, if these addresses weren't routed then how a particular system is identified over the internet. Address resolution solves this problem. These private address are assigned under a network and these networks have to be assigned a routable **public** IP. So all the systems connected to this network are assigned a unique private IP and they all shares a single **public** address to access teh internet. For this all system are configured to use a special server, called a PROXY SERVER.

A proxy server has two NICs(Network Interface Cards) since it is connected to two different network itself, one to connect to internet which is assigned the public(routable) IP(External Interface) and the other is connected to the internal network, where it is assigned a private IP so that it can communicate with internal network(Internal Interface). THe proxy server acts as a gateway onto the internet.

Public IP addresses are available from ISP these IPs can be dynamic as well as static.

### Request cycle :

When a system on the internal network with a private address wants to request information from web, it actually sends request to the internal interface of the proxy server. The proxy server with it's public routable address on the external NIC, is the one that actually sends the request to the Web server.

The web server sends back the response back to the proxy server's external NIC, and the proxy server then forwards the response to the system on the internal network that made the request.

The translation of private address to a public address and back again is most commonly known as **NAT**(Network Address Translation)

### Private Ip address ranges :

* 10.0.0.1 to 10.255.255.254
* 172.16.0.1 to 172.31.255.254
* 192.168.0.1 to 192.168.255.254

**Reserved IP Address :**

Another set of IP addresses are there which are reserved and thus cannot be used as public IP addresses to access internet which includes :

* **127.0.0.1 - 127.255.255.255** : These addresses are called loopback address.
* **0.0.0.0 to 0.255.255.255**