# DHCP

> Dynamic Host Configuration Protocol(DHCP) is a network service that enables host computers to be assigned settings from a server automatically rather than manually configuring each network host.

* DHCP provides settings to client which includes 
	* Ip address and netmask
	* IP address of gateway and DNS servers to use

* DHCP has a lot of advantages as we do not have to change settings for each client rather any change in the setting of dhcp is reflected in each client. 

* Allocating IP addresses is much easier with DHCP as DHCP posses a pool of ip addresses from which it dynamically allocates ip addresses to clients on first come first served basis. As soon as a dhcp client is no longer available the ip address belonging to him, the ip address is released back to the pool for use by other dhcp clients. Thus an address can be leased for a period of time. After this period of time the has to renegociate the lease with server to maintain the use of address.

DHCP works on a client server model. When a client just boots up and tries to connect to a network it does not have any network configuration available to connect to internet. It neither have an IP and nor does it know anything about the network it is connecting to.

It starts off with sending a **DHCPDISCOVER** message with 0.0.0.0 as the source address and 255.255.255.255 as destination address. If the DHCP server is on the local subnet it directly recieves the messages or in case of a different subnet, a relay agent connected to the client subnet is used to passon the request to the DHCP server. This message uses UDP protocol and the port number is 67.

On recieving DHCPDISCOVER message the DHCP server replies with a **DHCPOFFER** message. This message contains the network configuration settings for the requesting client. This message is sent as a broadcast message for the client to recieve. It uses UDP and 68 as the destination protocol.

The client forms a **DHCPREQUEST** message and sends it to the server indicating that it wants to accept the network configuration sent in DHCPOFFER. This message still contains the source IP address as 0.0.0.0

Once the server recieves the DHCPREQUEST message it sends the client **DHCPACK** message indicating that the client can now use the IP address offered.

There are some other DHCP messages also :

| Message | Explaination |
-----|-----
| DHCPNAK | It is opposite to DHCPACK and is sent when the server is not able to fulfill the clients DHCPREQUEST.|
| DHCPDECLINE | From the client to server when it finds out that the IP offered is already in use. |
| DHCPINFORM | From client to server when the IP is static and the remaining details are to be filled by DHCP server dynamically |
| DHCPRELEASE | Client to server when it wants to terminate the lease of the network address |

**Lease in DHCP**

IP  address assigned by DHCP server to DHCP client is on a lease. After the lease expires the DHCP server is free to assign the same IP address to any other host or device requesting for the same. For example, keeping lease time 8-10 hours is helpful in case of PC’s that are shut down at the end of the day.  So, lease has to be renewed from time to time. The DHCP client tries to renew the lease after half of the lease time has expired. This is done by the exchange of DHCPREQUEST and DHCPACK messages. While doing all this, the client enters the renewing stage.
