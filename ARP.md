# ARP (Address Resolution Protocol)

ARP is a communication protocol used for discovering the link layer address associtaed with the given internet layer address, it is basically used for mapping a network address(eg. an IPv4 address ) to a physical address like a MAC address.

The address resolution protocol is a request and response protocol whose messages are encapsultaed by a link layer protocol. The communication channel for ARP exists only within the boundries of a single netwrok and never routed across internetwork nodes. ARP thus exists in link layer.

* ARP was not developed in OSI model, but is often described as operating below network layer as a part of the interface between the OSI network and OSI link layer.

### Network Hardware

Each system on a network actually has two addresses. A logical IP address that can be assigned and a physcial hardware address that is permanent and is burned to NIC. This permanent address is often reffered to as MAC(Media Address Control) address. Each packet sent over a local LAN network segment must include both logical and physical to identify the destination system.

NIC is actually both a layer1(because it intercepts the electrical signal) as well as layer2(because it looks at the MAC address of the frames it sees). Similar case is with switches. Routers on the other hand also looks at the IP address to see which interface the packets needs to go out of placing it in layer 3 also.

Each network packet sent over a local LAN network udergoes a multi-layer encapsulation of data

![Multi Layer Encapsulation](/Resources/multi_layer_encapsulation.png)

Technically nothing is sent across the network cable. Only the votage in the network cable fluctuate rapidly and the interface(as we say) attached to the LAN cable senses and monitors these series of fluctuations and identifies them. These voltage fluctuation are what referred to as **LAYER 1 of OSI model**. It's the job of NIC to convert a frame into a series of voltage fluctuations when sending and to use these voltage fluctuation to rebuild a frame when receiving.

The encapsulation provides flexibility, as one layer's packet is the next lower layer's payload. Packets that travels over a LAN are encapsulated in an ethernet Frame.

![Multi Layer Encapsulation Payload](/Resources/multi_layer_encapsulation_payloads.png)

Since for such communication to occur we need to know that a destination computer's mac address is so that it can put it in a frame, this is where ARP comes into play.

ARP is actually similar to DNS where a computer sends out an ARP request packet to the system to resolve an IP address to MAC address which then sends this response back. An ARP reuqest is basically just a broadcast that says **Whoever has the IP address A.B.C.D send me your mac address** and the response is tha MAC address of the system with that IP.

To reduce the number of address resolution requests, a client normally caches resolved address for a short period of time. The size of arp cache is finite, if not flushed regularly it will be full of obsolete entries for the systems that are not in use. This flush is periodic and deletes unused entries and unsuccessful attempts to contact systems which are currently down.

Thus if a host changes the MAC address, it is detected by other hosts when the cache entry is deleted and a fresh arp association is made. 

Switches Routers and even our computers maintains this arp table. Our computer maintains this arp table to identify hosts in the local network to view arp table in your system just ping any system to make entry corresponding to that ip address in your local arp table and use `arp -a` to view the arp table.

A common entry that almost always exist in the arp table of local system, points to the gateway(router ip) so in case the ip requested is not in the same LAN segment the ARP request is sent to default gateway IP. The system knows that in order to access host on a different network segment it has to send the packet out the default gateway so it arps to get the MAC address of the router(gateway) interface.


#### A sample frame.

Taken from [Debian Network Guide](http://www.aboutdebian.com/network.htm)

Let's take a look at a somewhat realistic frame. You're on your PC at work which is connected to an Ethernet LAN and you send your mom an e-mail. Remember, when sending information the encapsulation process starts at the top OSI layer (Application layer) and works it's way down through the transport, network, and link layers. (Received frames go up the OSI layers and get de-encapsulated at each layer.)

* Since e-mail messages are sent using the SMTP protocol, your e-mail message will get wrapped in a TCP segment with port 25 as the destination port.
* Then, since your mom's e-mail address contained the domain name of her ISP, your system has to send out a DNS request to get the IP address of the mail server for that domain name. Once it has that it will use it as the destination IP address as it wraps the TCP segment up in an IP packet.
* Because the source and destination IP addresses are for different networks, your system will send out an ARP request to get the MAC address for the default gateway router's interface. With that it can wrap the IP packet inside an ethernet frame, calculate the checksum value for the FCS (Frame Check Sequence), and pass it down to the hardware layer to be put on the wire.


Note that your system had to do two address resolution queries (DNS and ARP) to get the two destination addresses (IP and MAC). Only after it has both of them can it complete the frame.

E-mail packet encapsulated in a frame

![Sample Email packet encapsulation](/Resources/email_encapsulation_frame.png)

At some point the packet will likely encounter your proxy server and it will change the source IP address of the packet to the public address of the external interface of the proxy server. The proxy server will use the randomly generated source port number (58631) to keep track of your PC's SMTP "conversation" with the mail server.

As your e-mail packet travels over the Internet the frame type will change to whatever medium (frame relay, ATM, etc.) is encountered along the way. The intermediate hop routers de-encapsulate and re-encapsulate with the proper frame type as necessary because routers can connect to different network mediums. But once the proxy server has changed the private IP address to a public one and sent the frame on its way, the IP addresses in the packet (and any information in the layers above it) never change as it winds its way through the Internet. Only the Layer 2 framing changes.
