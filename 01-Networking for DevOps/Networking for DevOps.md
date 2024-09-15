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

We use tables to help us determine the routes we want to take. This screenshot demonstrates a typical route table in AWS:

![Networking Route Table](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/route-table.png)

### Routing Decisions
When making a routing decision, more specific rules are evaluated first:

- **Local Network**: If a packet's destination falls within the range `10.21.0.0/16`, it will remain within the local 
network (like staying in your neighborhood).

- **Transit Gateway (TGW)**: If the destination is within the range `10.0.0.0/8`, the packet will be sent to the Transit
Gateway (TGW) interface (similar to taking state highways).

- **Internet Traffic**: If the packet's destination does not match any of the more specific ranges, the widest rule is 
applied: `0.0.0.0/0`. This indicates internet traffic, and the packet will be redirected to the Network Address Translation
(NAT) interface (akin to hopping onto the interstate, like I-95!).

## 7.Domain Name System (DNS)

### DNS Overview
As previously discussed, computers identify each other using IP addresses, while humans use names. To bridge this gap 
between human readability and computer communication, the Domain Name System (DNS) converts human-readable domain names
into computer-friendly IP addresses and vice versa.

Here’s a step-by-step breakdown of how DNS works when you request a web page through a browser:

1. **Client Query**: The client initiates a query to a Recursive Resolver.
2. **Root Server**: The Recursive Resolver connects to a Root Server.
3. **TLD Server**: The Root Nameserver responds with the address of a Top Level Domain (TLD) Server (such as `.com` or `.net`).
4. **TLD Request**: The Recursive Resolver makes a request to the TLD Server.
5. **Domain Nameserver**: The TLD Server returns the IP address of the Domain Nameserver, which holds information about the requested domain.
6. **Domain Nameserver Query**: The Recursive Resolver sends a query to the Domain Nameserver.
7. **IP Address Returned**: The Domain Nameserver provides the IP address of the requested domain to the Recursive Resolver.
8. **Client Response**: The Recursive Resolver sends the IP address back to the client.

This process is similar to a game of telephone, where information is translated back and forth between computer and human
languages until it reaches its final form.

![Networking DNS](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/dns.png)

### Domains, Zones, and Delegation

### Domains and Hierarchy
A **domain** is a self-contained network on the internet. Domains can have subdomains, and those subdomains can have their
own subdomains, creating a hierarchical structure.

To visualize domains, think of a tree structure. At the top of this tree is the DNS root zone, which represents the highest
level of the DNS hierarchy. This root zone is divided into **Top-Level Domains (TLDs)**, such as `.com`, `.gov`, and `.io`.
Each TLD represents a domain, and all subdomains under it. For instance, `example.com` is a subdomain of the `.com` domain.
This hierarchy is akin to folders and subfolders in a file system.

Different organizations manage different domains. For example, ICANN manages the root domain, encompassing all internet 
domains, while Verisign controls the `.com` domain. Though ICANN oversees the entire tree, Verisign manages a branch of 
it, specifically the `.com` zone.

### Delegation
**Delegation** allows an organization that owns a domain to transfer control over a subdomain to another entity. This 
process is facilitated through **Nameserver (NS) records**. When a domain owner delegates a subdomain, they create an 
NS record to point to the new owner’s nameservers. This record directs all communications related to that domain to the 
servers of the new organization, effectively making them the domain owner for that subdomain.

#### Example Scenario
1. ICANN operates root nameservers globally.
2. Verisign sets up its own nameserver and requests ICANN to delegate the `.com` zone to them.
3. ICANN creates an NS record pointing to Verisign’s nameserver. Now, any query for a `.com` domain is directed to Verisign’s server.

4. You start a company, “Example Ltd,” and wish to register `example.com` within the `.com` zone.
5. You set up your own nameserver and ask Verisign to delegate control over `example.com` to you.
6. Verisign creates an NS record that delegates control of `example.com` to “Example Ltd.” You now control the `example.com` domain.

This hierarchical and delegated structure allows for efficient management and organization of domain names across the internet.

![Networking Domains Zones Deligations](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/domains-zones-deligations.png)

### DNS Record Types
**DNS records**, also known as zone files, contain information about a domain. They provide details such as the IP address
associated with the domain and instructions on how to handle queries. Each DNS record also includes a **Time-To-Live (TTL)**
setting, which determines how frequently a DNS server should refresh the record.

### Common DNS Record Types
Below are the most commonly used types of DNS records and their meaning.

![Networking DNS Record Types](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/dns-record-types.png)

- **A (Address) Record**: Maps a domain name to an IPv4 address. For example, `example.com` might have an A record pointing
to `192.0.2.1`.

- **AAAA (IPv6 Address) Record**: Maps a domain name to an IPv6 address. For example, `example.com` might have an AAAA record
pointing to `2001:db8::1`.

- **CNAME (Canonical Name) Record**: Aliases one domain name to another. For example, `www.example.com` can be set as a CNAME
for `example.com`, meaning requests for `www.example.com` are redirected to `example.com`.

- **MX (Mail Exchange) Record**: Specifies mail servers for handling email for the domain. For example, `example.com` might
have an MX record pointing to `mail.example.com` with a priority value.

- **NS (Name Server) Record**: Indicates which DNS servers are authoritative for the domain. For example, `example.com` might
have NS records pointing to `ns1.example.com` and `ns2.example.com`.

- **PTR (Pointer) Record**: Used for reverse DNS lookups, mapping an IP address to a domain name. For example, a PTR record
for `192.0.2.1` might point to `example.com`.

- **SOA (Start of Authority) Record**: Provides information about the domain’s zone, including the primary DNS server, the
domain administrator’s email, the domain’s serial number, and refresh timings.

- **TXT (Text) Record**: Allows for arbitrary text data to be associated with a domain. Commonly used for verification purposes
and to hold SPF (Sender Policy Framework) data for email authentication.

Each type of DNS record serves a specific purpose and is essential for the proper functioning and management of domains 
on the internet.

## 8.HTTP

### HTTP Methods
You’ve likely encountered Hypertext Transfer Protocol (HTTP) in your work. HTTP is crucial for interacting with web pages,
HTML documents, and APIs. It forms the backbone of data exchange on the internet, and a solid understanding of HTTP is 
essential for any DevOps engineer.

An **HTTP request** is a message sent from a client to a server to request access to a resource. As a DevOps engineer, 
it’s important to understand the different HTTP request methods and their purposes.

### Common HTTP Request Methods
There are 7 main HTTP request methods:

![Networking HTTP Request Methods](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/http-request-methods.png)

- **GET**: Retrieves data from a server. For example, when you visit a web page, your browser sends a GET request to retrieve the HTML content of that page.

- **POST**: Submits data to a server to create or update a resource. For example, submitting a form on a website sends a POST request with the form data to the server.

- **PUT**: Updates an existing resource on the server or creates a new resource if it does not exist. For example, sending a PUT request to update a user's profile information.

- **DELETE**: Removes a resource from the server. For example, sending a DELETE request to remove a user account.

- **HEAD**: Similar to GET but only retrieves the headers of a resource, not the resource itself. Useful for checking if a resource exists or if it has been modified.

- **OPTIONS**: Describes the communication options for the target resource. It is often used to determine what HTTP methods are supported by the server.

- **PATCH**: Partially updates a resource. Unlike PUT, which updates the entire resource, PATCH is used to apply partial modifications.

Understanding these HTTP methods helps in designing, debugging, and managing web services and applications. Each method serves a specific purpose and impacts how data is exchanged between clients and servers.

### HTTP Response Codes
Response codes indicate whether a request was completed successfully or failed. You’ve probably seen them floating around
in pop culture references or been on the receiving end of a hyperlink that goes nowhere.

![Networking HTTP Response Codes](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/http-response-codes.png)
