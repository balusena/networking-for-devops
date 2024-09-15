# Networking for DevOps

Understanding networking fundamentals is crucial for a successful career in DevOps. As a DevOps engineer, you'll need to
grasp the basics of the OSI model, which breaks down network communication into layers, helping you troubleshoot and optimize
network performance. Familiarity with TCP/IP protocols is essential, as these protocols form the backbone of most network
communications.

You'll also need to understand subnetting to calculate IP address ranges and subnet sizes accurately, which is vital for
efficient network design and management. Basic routing knowledge is necessary to manage and direct network traffic effectively,
ensuring data reaches its intended destination.

Additionally, proficiency with network debugging tools like Ping, Traceroute, and Telnet is important for diagnosing and
resolving connectivity issues. These tools help you identify where problems are occurring within the network and provide
insights into network performance.

Mastering these networking concepts and tools will enable you to build robust, scalable, and reliable systems, making you
a more effective DevOps engineer. This knowledge will not only improve your troubleshooting skills but also enhance your 
ability to design and maintain complex network infrastructures.

## 1. OSI Model
The Open Systems Interconnection (OSI) model is a set of standards that defines how computers communicate over a network.
In the OSI model, data transmission is broken down into seven layers, each building upon the one before it. Every layer 
uses data from the previous layer and serves a specific purpose in the overall process of network communication.

The OSI model operates from the bottom up, starting with layer 1 (Physical) and ending with layer 7 (Application). The 
top layer is the point where users interact most directly with the network. For example, if you’re reading this content 
on a device, you're engaging with the 7th layer right now.

![Networking OSI Model](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/osi-model.png)

## OSI Model Layers Breakdown

### Layer 1: Physical
The Physical layer handles raw data transmitted over physical media. This data consists of bits of information that the 
Physical layer converts into electrical signals, defining specific characteristics of the physical medium. For example, 
Physical layer specifications determine aspects like voltage levels, transmission distances, and cable standards. 
Technologies such as Bluetooth and Ethernet operate at this layer.

### Layer 2: Data Link
The Data Link layer takes data in the form of electrical signals (called frames) and transfers it across nodes within a 
single network. Data Link frames function only within a local network and do not traverse into other networks.

This layer also detects and corrects transmission errors by adding extra information, like an error detection code, to a
frame. The receiver checks the frame by comparing the received data to the error detection code.

### Layer 3: Network
The Network layer governs the connection of different subnetworks and networks through routers or gateways. It determines
the most efficient route to deliver information. If a message is too large, the Network layer may split it into fragments,
transmit them separately, and reassemble them at the destination.

### Layer 4: Transport
The Transport layer manages host-to-host communication for applications, ensuring reliable, connection-oriented communication
and flow control. Some protocols in this layer are connection-oriented (requiring a pre-established path between hosts), 
while others are connectionless, transmitting data end-to-end without the need for a connection.

### Layer 5: Session
The Session layer manages and controls connections, monitoring potential connection losses and reopening them when necessary.
It also optimizes connections by closing idle ones and reopening them when needed. This layer establishes synchronization
points within the data stream to ensure large messages are correctly reassembled.

### Layer 6: Presentation
Also known as the Syntax layer, the Presentation layer ensures that data received from another system is readable and 
understandable. This layer handles processes like data encoding, compression, and encryption to ensure proper data presentation.

### Layer 7: Application
The Application layer is the topmost layer of the OSI model, where data is presented in a format suitable for the end user.
This layer includes protocols such as HTTP, DNS, FTP, and SSH. Almost everyone interacts with Application layer protocols
on a daily basis, not just DevOps engineers!

## 2.TCP/IP

### What is TCP/IP, and how is it different from OSI?
The OSI model explained above is great for developing a theoretical understanding of a networking stack, but it's challenging
to implement in practice. Today, we primarily use the Transmission Control Protocol/Internet Protocol (TCP/IP) model. This
model has a similar layered structure but is simpler and more practical.

TCP/IP combines the three top layers of the OSI model (Application, Presentation, and Session) into a single Application
layer. Additionally, the two bottom layers of the OSI model (Data Link and Physical) are merged into the Network Interface
layer in TCP/IP.

The result is a streamlined 4-layer TCP/IP model, consisting of the following layers from bottom to top: Network Interface,
Network, Transport, and Application.

It's important to keep these differences in mind when dealing with real-world networking scenarios.

![Networking OSI vs TCP/IP Model](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/osi-vs-tcp-ip.png)

## 3.TCP vs UDP
The Transport layer of the TCP/IP model utilizes two major protocols: TCP and UDP. It's essential to understand the differences
between them.

### TCP
TCP is a connection-oriented protocol, meaning it establishes a link between the source and destination before transmitting
data. Once the connection is made, TCP breaks down large data sets into smaller packets, sends them across the connection,
and ensures data integrity throughout the process. TCP is the preferred protocol when data integrity is crucial, such as in
transactional systems.

### UDP
UDP, on the other hand, is a connectionless protocol. It begins transmitting data immediately without waiting for a connection
confirmation from the receiver. While there is a risk of data loss, UDP is often used when speed is more important than perfect
transmission, such as in voice or video streaming applications.

## 4.Ports and Protocols
The Transport layer of the TCP/IP model also introduces the concept of ports. Ports are labeled with specific port numbers,
which are digital identifiers used to match incoming network data with the appropriate process or application on the receiving
system.

![Networking Ports Protocols](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/ports-protocols.png)

While many ports are non-privileged meaning anyone can use them without special permissions some require root access. 
Ports 1-1023 are known as "well-known ports" and require root permissions for a server to listen on them. It's a good 
practice to avoid running web servers as root, assign minimal permissions to services, and use non-privileged ports 
whenever possible. 

This is why you may often see ports like 8080 for HTTP and 6443 for HTTPS they are non-privileged and don't require root
permissions.

## 5.IP Subnetting, CIDR

The most critical component of networking is the IP address. Every time you browse the internet, your browser connects to
a remote server using an IP address. You cannot use the internet or any network without one.

An IP address is a 32-bit number divided into four 8-bit sections called octets. It can be represented in both decimal and
binary formats. An IP address may contain a subnetwork (subnet) that’s different from the host. The address comes with a
subnet mask, which distinguishes the part of the IP address that is the network and the part that is the host address.

For example, given an IP address of `192.168.12.20` with the subnet mask of `255.255.255.0`, `192.168.12` represents the
network address, and `.20` represents the host address. This concept of a subnet mask leads us to classful addressing, 
where IP addresses are divided into five subclasses.

### Classful Addressing
In classful addressing, IP addresses have an 8-bit, 16-bit, or 24-bit network prefix:

- **Class A**: 8-bit network ID, 24-bit host ID, over 16 million addresses.
- **Class B**: 16-bit network and host IDs, 65,535 addresses.
- **Class C**: 24-bit network ID, 8-bit host ID, 254 addresses.

When allocating IP addresses, it's important to consider the size of your network. For large or small networks, it's 
straightforward to select the correct class. However, problems arise with medium-sized networks, where you might need 
more than 254 addresses (Class C) but fewer than 65,535 (Class B).

### Example Scenario
Let’s assume you need 1,000 addresses for your network. Since 1,000 is more than 254, you'd traditionally choose Class B.
However, this results in 64,000 unused addresses, which is inefficient. One alternative could be using multiple Class C 
ranges, but this complicates routing by having many small networks.

To solve this issue, we use **Classless Inter-Domain Routing (CIDR)**.

### Classless Inter-Domain Routing (CIDR)
CIDR eliminates the rigid class structure by allowing network administrators to move the subnet boundary anywhere within
the parent network. In other words, we are no longer restricted to 8-bit, 16-bit, or 24-bit subnet masks.

Let’s revisit our example. Imagine you need 300 hosts but have an address range that supports only 254. Traditionally, 
you'd need two Class C networks, but this complicates routing. With CIDR, you can adjust the subnet mask to fit your 
needs. By decreasing the subnet mask bits by one, you create a network that supports 510 hosts—much more efficient!

### Common IP Addresses and Subnet Masks
The table below outlines the most common combination of addresses and netmasks and important details about them.

![Networking CIDR ](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/cidr.png)

## 6.Routing
How do we get a packet of information from a host on one network to a host on another? In one word: **Routing**.

![Networking Routing](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/routing.png)

Think of a route as a path. Different routes lead to different destinations, and they are used depending on the target 
you’re trying to reach. It’s similar to driving. If your destination is a house in a quiet neighborhood, you’ll take a 
local road. If you want to go to a mall a few towns over, you may take a state highway. But if you’re planning a cross 
country road trip, you’ll hop onto the interstate.

Routing works the same way: based on the destination, different routes are chosen to ensure the packet reaches the correct
location efficiently.


