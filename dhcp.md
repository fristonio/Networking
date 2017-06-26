# DHCP

> Dynamic Host Configuration Protocol(DHCP) is a network service that enables host computers to be assigned settings from a server automatically rather than manually configuring each network host.

* DHCP provides settings to client which includes 
	* Ip address and netmask
	* IP address of gateway and DNS servers to use

* DHCP has a lot of advantages as we do not have to change settings for each client rather any change in the setting of dhcp is reflected in each client. 

* Allocating IP addresses is much easier with DHCP as DHCP posses a pool of ip addresses from which it dynamically allocates ip addresses to clients on first come first served basis. As soon as a dhcp client is no longer available the ip address belonging to him, the ip address is released back to the pool for use by other dhcp clients. Thus an address can be leased for a period of time. After this period of time the has to renegociate the lease with server to maintain the use of address.