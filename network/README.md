
### Connectivity troubleshooting techniques

Let's imagine you deploy a web server on the cloud, but the server can't be reached from clients.

In order to solve the connectivity failure issue, one could proceed following a method to :

1 - Identify the failing component in the network route
2 - Find out what's wrong with that component

In order to solve the first several tools can be used :

- Check that you can reach other websites from the client
- Check you can reach other websites on in the same server network group from the client
- Check the route taken by data taken with traceroute. If the route shows a complete path up to the web server you try to reach, then the problem is with the web server itself

- Check the transport layer with ping
- Check the route taken by data taken with traceroute
- Check the name resolution with a DNS
- Check the firewall rules

One could record the network communication using a tool such as Wireshark by capturing data flowing through the network card of the communication initiator.

It should then be possible to follow the TCP stream and to identify a failing component in the route.

Traceroute is command which shows you the path a packet of information takes from A to B. A is the computer from which you run traceroute.



### Ip v6

### Interfaces

#### Ethernet
#### Bridge
#### Loopback

### Ifconfig

### LAN, WAN

### Virtual networks

### Virtual IP



 


