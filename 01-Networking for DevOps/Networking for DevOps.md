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

### There are 4 categories of HTTP responses:
- **200s: Successful responses**
- **300s: Redirects**
- **400s: Client errors**
- **500s: Server errors**

## Common HTTP Response Codes
HTTP response codes are essential for understanding the status of a server's response to a client’s request. They help in
diagnosing issues and managing the communication between clients and servers. Here are some of the most common HTTP response
codes you should be familiar with:

![Networking HTTP Response Codes 2](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/http-response-codes-2.png)

### 1xx - Informational
- **100 Continue**: Indicates that the initial part of a request has been received and the client should continue with the request.

### 2xx - Success
- **200 OK**: The request was successful, and the server returned the requested resource.
- **201 Created**: The request was successful, and a new resource was created as a result.
- **204 No Content**: The request was successful, but there is no content to send in the response.

### 3xx - Redirection
- **301 Moved Permanently**: The requested resource has been permanently moved to a new URL.
- **302 Found**: The requested resource has been temporarily moved to a different URL.
- **304 Not Modified**: The resource has not been modified since the last request, so the client can use its cached version.

### 4xx - Client Error
- **400 Bad Request**: The server could not understand the request due to invalid syntax.
- **401 Unauthorized**: The request requires user authentication.
- **403 Forbidden**: The server understood the request but refuses to authorize it.
- **404 Not Found**: The server could not find the requested resource.
- **405 Method Not Allowed**: The request method is not allowed for the requested resource.

### 5xx - Server Error
- **500 Internal Server Error**: The server encountered an unexpected condition that prevented it from fulfilling the request.
- **502 Bad Gateway**: The server, while acting as a gateway or proxy, received an invalid response from the upstream server.
- **503 Service Unavailable**: The server is currently unable to handle the request due to temporary overloading or maintenance.
- **504 Gateway Timeout**: The server, while acting as a gateway or proxy, did not receive a timely response from the upstream server.

Understanding these response codes is crucial for diagnosing issues and ensuring smooth operation of web services and applications.

### HTTP Headers

HTTP headers are used to pass additional information between clients and servers. They provide essential details for various
purposes, such as authentication, caching, and specifying the type of client device sending the request. HTTP headers are
categorized into four general contexts:

### General Header
- **Definition**: Headers that apply to both request and response messages.
- **Examples**:
  - `Date`: Specifies the date and time at which the message was sent.
  - `Connection`: Controls whether the connection should be kept alive or closed after the completion of the request/response.

### Request Header
- **Definition**: Headers that are included in request messages sent from a client to a server.
- **Examples**:
  - `Authorization`: Contains credentials for authenticating the client to the server.
  - `Accept`: Specifies the media types that the client is willing to receive from the server.
  - `User-Agent`: Provides information about the client’s software and operating system.

### Response Header
- **Definition**: Headers that are included in response messages sent from a server to a client.
- **Examples**:
  - `Location`: Redirects the client to a different URL (used with status codes like 301 and 302).
  - `Server`: Provides information about the server software that handled the request.
  - `WWW-Authenticate`: Indicates how the client should authenticate to access the resource (used with status codes like 401).

### Entity Header
- **Definition**: Headers that provide information about the entity (resource) itself or the resource requested.
- **Examples**:
  - `Content-Type`: Specifies the media type of the resource (e.g., `text/html`, `application/json`).
  - `Content-Length`: Indicates the size of the response body in bytes.
  - `Last-Modified`: Provides the date and time at which the resource was last modified.

Understanding these HTTP headers is crucial for handling and managing web requests and responses effectively.

## 9.Network Troubleshooting Tools

### 1.ping
The easiest tool to test network connections is `ping`. It uses the ICMP protocol’s ECHO_REQUEST datagram to obtain an 
ICMP ECHO_RESPONSE from a remote host. The `ping` command is integrated into all versions of Windows, so you just need 
to open your command prompt or application to start using it.

To troubleshoot using `ping`, first run it on your own network (the local host) to ensure that your network interface is
working. Simply open the command prompt and type `ping www.google.com`. As you continue troubleshooting, you can ping hosts
and gateways further along the network to diagnose the location of connectivity problems.

![Networking Ping](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/ping.png)

When you ping, you receive information back, including the percentage of lost packets and average round-trip latency.

### 2.traceroute
Sometimes a network is particularly slow, and you need to track the routes of your packets or identify which gateway is 
causing delays. This can be challenging to do manually, which is where the `traceroute` command comes in handy.

`traceroute` (sometimes written as `tracert`) is a diagnostic command that shows possible routes across an IP network and
calculates any transit delays along that route. While `ping` only shows a final round-trip time for packets to go from host
to destination and back, `traceroute` calculates the total time spent establishing a connection by adding up the round-trip
times for each subsequent node along a given route.

The goal of `traceroute` for troubleshooting is to send User Datagram Protocol (UDP) probes with increasing Time to Live
(TTL) values until the Internet Control Message Protocol (ICMP) returns a “time exceeded” message. This message indicates
that the packet has reached a router along the route. The TTL is increased by one each time until the “port unavailable” 
message is received, signaling either the end of the destination or that the maximum TTL has been reached.

The probes start by sending a packet with TTL=1. Each time a packet hits a router, it lowers the TTL by 1. When you receive
a time exceeded message, it means TTL has reached 0, and you have reached another stop along the route. The TTL is incremented
by one each time, gradually revealing each hop along the route until the destination is found or the maximum number of hops
is hit. 

The report you receive includes:
- The Time to Live
- The IP addresses of each stop in the route—each gateway that has responded to the probe
- The round-trip time for each router along the route

This information is valuable for determining the exact route and troubleshooting any speed or network issues. Additionally,
`traceroute` marks any router on the route that does not respond within the time limit with an asterisk (*), helping you
pinpoint where to focus your troubleshooting efforts.

**Here’s an example of a report output from a traceroute command. Take a close look at it.**

![Networking Traceroute](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/traceroute.png)

You may notice that lines 2 and 3 are identical. This is an example of a buggy kernel in the second hop that forwards packets
with zero TTL – `lbl.csam.arpa`.

As you can see, `traceroute` can provide a lot of really helpful diagnostic information quickly and simply. However, it does
have limitations. Some networks don’t provide address-to-name translations. When these appear in your report, you have to guess
the path that packets take across the network. This happens in the report sample above at hop number 6 with IP address 
128.32.197.4, a router along the NSFNet, which doesn’t provide the named translation.

Overall, though, `traceroute` is a commonly used diagnostic tool and one that you will use often in your DevOps career.

### 3.Telnet
One important caveat to tools like `ping` and `traceroute` is that a server responding to these tools does not necessarily
mean that it is fully operational.

Imagine you have a virtual machine with an Apache HTTP server running on it. For web pages to load, the Apache daemon needs
to be up and running. Even if the virtual machine responds to `ping` requests, you won’t be able to load web pages if Apache
isn’t running.

Conversely, if a server does not respond to `ping`, it’s not necessarily down. Some system administrators configure firewalls
to drop all `ping` requests, so you might get no response from the server. However, the server behind this firewall can still
be reachable via other protocols.

Because of these limitations with `traceroute` and `ping`, you may need to test whether a specific protocol allows you to
establish a network connection. The `telnet` command can help with this.

Historically, `telnet` was used as a command-line interface for accessing remote servers. However, because `telnet` does 
not encrypt data, it is not secure for remote access and has since been replaced by SSH.

Despite this, `telnet` remains useful for testing whether one host can establish a network connection using a certain protocol.

For example, to test the connection to `google.com` on port 443 using `telnet`, you would use the following command:

![Networking Telnet](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/telnet.png)

As you can see above, the command succeeded, which means that a connection is allowed between our local machine and a remote
system on a given port.

### 4.curl
As a DevOps engineer, you’re frequently going to have to transfer data, and that means you should know how to use curl. 
curl is an open-source data transfer tool that supports multiple Application-layer protocols. It’s most commonly used for
sending HTTP requests, which are requests for access to a resource on a server. curl is freely available and may already
be on your system. If it isn’t, you can easily install it.

The most basic way to use curl is to perform an HTTP GET request (remember from our table earlier in this article that 
this is a request for a resource (HTTP) that returns the entire entity in the response (GET).

**The basic syntax is:** 
```
ubuntu@balasenapathi:~$ curl http://example.com
<!doctype html>
<html>
<head>
    <title>Example Domain</title>
    <meta charset="utf-8" />
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <style type="text/css">
        body {
            background-color: #f0f0f2;
            margin: 0;
            padding: 0;
            font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
        }
        div {
            width: 600px;
            margin: 5em auto;
            padding: 2em;
            background-color: #fdfdff;
            border-radius: 0.5em;
            box-shadow: 2px 3px 7px 2px rgba(0,0,0,0.02);
        }
        a:link, a:visited {
            color: #38488f;
            text-decoration: none;
        }
        @media (max-width: 700px) {
            div {
                margin: 0 auto;
                width: auto;
            }
        }
    </style>
</head>

<body>
<div>
    <h1>Example Domain</h1>
    <p>This domain is for use in illustrative examples in documents. You may use this
    domain in literature without prior coordination or asking for permission.</p>
    <p><a href="https://www.iana.org/domains/example">More information...</a></p>
</div>
</body>
</html>
```
This will send an HTTP GET request to the example.com host.This is the HTML content of the "Example Domain" website at 
http://example.com, which is commonly used for testing purposes. The website displays a simple message and a link for 
more information.

If you’re checking an exact response code and only want to see response headers, you can use curl -I. The syntax looks 
like this in our example:
```
ubuntu@balasenapathi:~$ curl -I http://example.com
HTTP/1.1 200 OK
Age: 599837
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8
Date: Mon, 09 Sep 2024 09:23:17 GMT
Expires: Mon, 16 Sep 2024 09:23:17 GMT
Last-Modified: Thu, 09 Aug 2018 15:35:29 GMT
Server: ECS (nyb/1D2E)
Vary: Accept-Encoding
X-Cache: HIT
Content-Length: 1256
```
This output gives you metadata about the response, such as the HTTP status code (200 OK), the Content-Type, the server 
details, and caching information, but it does not display the HTML content of the page.

By default, curl uses the HTTP GET method. If you wanted to use another method to return a certain type of response, you
can use the -X flag in your curl command followed by the type of request that you want. For example,

Running the command curl -X POST http://example.com would send a POST request to http://example.com. However, since 
http://example.com doesn't accept POST requests (it's a static page used for testing), you would typically receive a 
response indicating that the method is not allowed.
```
ubuntu@balasenapathi:~$ curl -X POST http://example.com
<html>
<head>
<title>405 Method Not Allowed</title>
</head>
<body>
<center><h1>405 Method Not Allowed</h1></center>
<hr><center>nginx</center>
</body>
</html>
```
The status code 405 Method Not Allowed tells you that the server does not support POST requests to this URL. The specific
format of the response can vary depending on the server configuration.

In this case, the curl -X POST http://example.com command sends an HTTP POST request (which is typically used for submitting
data or making changes to a resource), but since http://example.com does not support POST requests, the server responds 
with an error.

curl is the master of data transfer, and we can even download files/store a file’s response with curl by using the -o flag
Syntax for this may look something like this:
```
ubuntu@balasenapathi:~$ curl http://example.com/maile -o output.file.
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
curl: (22) The requested URL returned error: 404 Not Found
```
since the URL http://example.com/maile doesn't exist (it's a non-existent path), you will likely receive a 404 Not Found error.
The command will still attempt to save the response (the error page) in output.file. The exact output on the terminal will look
something like this:
```
ubuntu@balasenapathi:~$ cat output.file
<!doctype html>
<html>
<head>
    <title>404 Not Found</title>
</head>
<body>
    <h1>Not Found</h1>
    <p>The requested URL /maile was not found on this server.</p>
</body>
</html>
```
This indicates that the resource /maile does not exist on the example.com server.

There are other curl commands, too. Explore curl more deeply on the site for the curl project, where you’ll find a plethora
of helpful (and totally free) resources. Once you’re familiar with the tool, you’ll be able to use it to accomplish a number
of programming tasks.

### 5.dig
The next tool to learn is "dig", not “how to dig”, but just "dig" – which stands for Domain Information Groper.

It is used for troubleshooting Domain Name System (DNS) problems and verifying DNS records. dig performs DNS Lookups and
then shows you the answers returned from the name server(s).

The basic syntax of dig for a DNS record lookup is [dig] [domain name]. This will make an NS query and return the "A record"
Address record for a given domain name.

Let's break down this example by looking up the DNS record for the domain google.com. At the top, you can see the request: 
dig google.com. In the ANSWER section of the response, you get a number of pieces of information:

**The queried server (google.com)**
- TTL ( in this case 93)
- Query class (IN= internet)
- Query type (A= address)
- The IP address for the queried domain (172.217.0.46)
So there you have it the google.com DNS record is associated with the IP address 172.217.0.46.
```
ubuntu@balasenapathi:~$ dig google.com
```
![Networking Dig DNS](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/dig-dns.png)

Like with curl, the dig has a default method. By default, dig will attempt to query each server specified using the 
/etc/resolv.conf file, the automatic file type for configuring DNS name servers. But in some cases, you may want to send
queries to a specific DNS server. You can do this with the @ flag.

This example checks the DNS record for google.com on specifically the 8.8.8.8 server. As you can see, it returns a different
ANSWER from the /etc/resolv.conf file used in the default above.
```
ubuntu@balasenapathi:~$ dig @8.8.8.8 google.com
```

![Networking Dig IP](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/dig-ip.png)

By default, dig also returns an ANSWER of a A record (address). But you can also check different types of DNS records using
the -t option. The syntax for this would look like:

dig -t [record type] [domain name]
The example below specifics the TXT record for the google domain.
```
ubuntu@balasenapathi:~$ dig -t TXT google.com
```

![Networking Dig Record Type](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/dig-record-type.png)

**Other dig record types you may want to specifically query:**
- MX record- mail exchanger, tells you what mail server accepts email messages for a given domain name
- NS record- all authoritative servers for a domain name
- ALL- all DNS records for a domain name

Dig is a great tool for DevOps engineers to have in their toolbox because it helps you troubleshoot for your name servers,
double-check records, and trace IP addresses and their domain names, among other things.

### 6.netstat
netstat is a command that shows you specific information about the communications between your local machine and other 
machines/devices on the network. Netstat shows active TCP connections as well as ports on which the server is listening.
It is useful when you need to see which network services are running on a local machine.

In the example below, we can discover that there is an apache web server listening on the default HTTP port.

![Networking NETSTAT](https://github.com/balusena/networking-for-devops/blob/main/01-Networking%20for%20DevOps/netstat.png)