## Networks and sub-networks

A subnetwork is a logical division of a network managed with TCP/IP protocols.

The practice of division of a network is called subnetting.

The division is used to separate two group of addresses :

* The one which are used for routing
* The one which are assigned to network interfaces 

The division of the network is performed with the help of a Subnet mask.

Routers are used to manage subnet masks.

### Subnet mask Ip v4

An IP address has 2 parts :
- A host address
- A network address

The subnet mask separates the two.

The host address can be further divided into a subnet network address and host adresses by subnetting.

A subnet mask is a 32 bits address.

Networks bits are all set to 1 and host bits are all set to 0. 

Example :

    Netmask decimal : 240.0.0.0
    Netwask binary : 11110000 00000000 00000000 00000000

Applying the subnetmask to an IP address with the bitwise AND operator produces the network address. 

### Motivation of subnetting

To divide a large network into smaller network for organization and security purpose.

Nodes of a subnet see all packets transmitted by any node in the network. 

### Classes of networks

Network classes have been defined depending on the number of host addresses available within the network.

IP V4 : 32 bits adresses

Class A : 

* /8 (meaning 8 bits allocated to network identification)
* netmask : 255.0.0.0
* 2^24 : 16777216 interface addresses

Class A = /8, Class B = /16, and Class C = /24

#### Classless Inter Domain Routing

Subnetting with classes is coarse grained.

In order to avoid to waste unused adresses in a subnetwork, finer grained Classless Inter Domain Routing (CIDR) is used.

CIDR is allocated with 1 bits increments, from /4 to /30.