# ARP (Address Resolution Protocol)

ARP is a communication protocol used for discovering the link layer address associtaed with the given internet layer address, it is basically used for mapping a network address(eg. an IPv4 address ) to a physical address like a MAC address.

The address resolution protocol is a request and response protocol whose messages are encapsultaed by a link layer protocol. The communication channel for ARP exists only within the boundries of a single netwrok and never routed across internetwork nodes. ARP thus exists in link layer.

* ARP was not developed in OSI model, but is often described as operating below network layer as a part of the interface between the OSI network and OSI link layer.

### Network Hardware

Each system on a network actually has two addresses. A logical IP address that can be assigned and a physcial hardware address that is permanent and is burned to NIC. This permanent address is often reffered to as MAC(Media Address Control) address. Each packet sent over a local LAN network segment must include both logical and physical to identify the destination system.

Each network packet sent over a local LAN network udergoes a multi-layer encapsulation of data

![Multi Layer Encapsulation](/Resources/multi_layer_encapsulation.png)

Technically nothing is sent across the network cable. Only the votage in the network cable fluctuate rapidly and the interface(as we say) attached to the LAN cable senses and monitors these series of fluctuations and identifies them. These voltage fluctuation are what referred to as **LAYER 1 of OSI model**. It's the job of NIC to convert a frame into a series of voltage fluctuations when sending and to use these voltage fluctuation to rebuild a frame when receiving.

The encapsulation provides flexibility, as one layer's packet is the next lower layer's payload. Packets that travels over a LAN are encapsulated in an ethernet Frame.

![Multi Layer Encapsulation Payload](/Resources/multi_layer_encapsulation_payload.png)

Since for such communication to occur we need to know that a destination computer's mac address is so that it can put it in a frame, this is where ARP comes into play.

ARP is actually similar to DNS where a computer sends out an ARP request packet to the system to resolve an IP address to MAC address which then sends this response back. An ARP reuqest is basically just a broadcast that says **Whoever has the IP address A.B.C.D send me your mac address** and the response is tha MAC address of the system with that IP.

To reduce the number of address resolution requests, a client normally caches resolved address for a short period of time. The size of arp cache is finite, if not flushed regularly it will be full of obsolete entries for the systems that are not in use. This flush is periodic and deletes unused entries and unsuccessful attempts to contact systems which are currently down.

Thus if a host changes the MAC addres, it is detected by other hosts when the cache entry is deleted and a fresh arp association is made. 
