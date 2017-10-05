# Network Design Principles

## End-To-End Argument :

> The function in question can completely and correctly be implemented only with the knowledge and help of the application standing at the end points of the communication systems. Therefore, providing that questino function as a feature of communication system itself is not possible.

In Laymen terms what it tries to say is that the intelligence required to implement a particular application on the communication network  should be placed at the endpoints of the network rather than the middle of the network. Example of end to end arguments

* Error handling and file handling
* End To End Encryption
* TCP/IP Error handling 

**Dumb Network, Intelligent Endpoints**

EndToEnd design principle is an argument and not a theorem so there are many cases where it is not the best choice.

Voilation of end-to-end argument :

* NAT
* VPN Tunnels
* TCP splitting
