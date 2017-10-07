# Switches

A network switch(also known as switching hub, bridging hub, MAC bridge)is a computer networking device that connects devices together on a computer network using packet switching to recieve process and forward data to the destination device.

A switch is a multiport bridge that uses hardware address to process and forward data at DLL of OSI model. Each network device connected to a switch can be identified by its network address, which allows switch to regulate the flow of traffic.

Each device connected to a switch port can transfer data to any other one at a time, and the transmission will not interfere. A limitation for this is, in half duplex mode each switch port can only either revieve or transmit data at a time. 

**Hubs**

Hubs are similar to switches that is a common connection point for devices in a network. They are used to connect segments of a LAN.

**Switches vs Hubs**

Switches are high-performance alternatives to hubs. Both serves a basic purpose to pass data between devices connected to the. Hubs achieves this by broadcasting data to all other connected devices, while switches first determine which device is the intended recipient of the data and then sends it to that one device directly via a so-called "virtual-circuit".

Hubs practically do not have any way of distinguishing which port the frame should be sent to. So it is sent to all the port to ensure that the frame reachs the destination.

Switches actually sets up a virtual direct connection between the two computers which means that switch bandwidth isn't shared.
