# TUN TAP

Each network communication have a physical interface associated with it, which is responsible for putting the packets on the communication channel(like wire) for example ethernet interface(eth0). TUN/TAP devices are virtual intrerpretation of those intrefaces they are managed entirely by the kernel.
These devices provides userspace programs the ability to interact with the traffic in a way like they are really behind a real interface.

TUN and TAP devices works at different levels or layers. TUN devices works at layer 3 or IP layer, which actually are point to point connections. They receives only IP packets.
TAP devices in contrast works on layer 2 or Ethernet layer and thus handle traffic like bare network adapters.

These devices provide the virtual interfaces. To create a virtual interface

```sh
$ ip tuntap add new_interface mode tap
```

You can check for the interface using `ip link show` linux command. To remove a tuntap device use `del` command.

These virutal interface can then be given IPs using

```sh
$ ip addr add 10.0.31.10 dev new_interface
$ ip addr add 10.0.21.20/32 dev new_interface
```

The file descriptors for these devices are present in `/dev/net/tap` and `/dev/net/tun`

A veth pair is a pair of directly connected virtual network interfaces. An ethernet frame sent to one end of a veth pair is received by the other end of a veth pair. Networking uses veth pairs as virtual patch cables to make connections between virtual bridges.
