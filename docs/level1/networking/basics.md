## OSI Model (Layer 1 to 7)

The OSI (Open Systems Interconnection) model is a conceptual framework used to understand how different network protocols and technologies interact with each other. It consists of seven layers:

1. **Physical Layer**: This layer deals with the physical transmission of data over the network, including the specifications of cables, connectors, and network devices.

2. **Data Link Layer**: The data link layer provides reliable and error-free communication between directly connected devices by using protocols like Ethernet. It handles framing, error detection, and flow control.

3. **Network Layer**: The network layer is responsible for logical addressing and routing of data packets. IP (Internet Protocol) operates at this layer and enables the internetworking of different networks.

4. **Transport Layer**: The transport layer ensures reliable and orderly delivery of data between end systems. TCP (Transmission Control Protocol) provides reliable, connection-oriented communication, while UDP (User Datagram Protocol) offers faster, connectionless communication.

5. **Session Layer**: The session layer establishes, manages, and terminates connections between applications. It provides services such as session establishment, synchronization, and checkpointing.

6. **Presentation Layer**: The presentation layer handles data formatting and conversion to ensure compatibility between different systems. It deals with data encryption, compression, and character encoding.

7. **Application Layer**: The application layer is responsible for providing services directly to the end-user applications. Protocols like HTTP, FTP, DNS, and SMTP operate at this layer.

## IP/TCP/UDP

- **IP (Internet Protocol)**: IP is the core protocol of the internet, responsible for logical addressing and routing of data packets between different networks. IPv4 and IPv6 are the most widely used versions.

- **TCP (Transmission Control Protocol)**: TCP is a reliable, connection-oriented protocol that provides error detection, flow control, and sequencing of data packets. It guarantees the reliable delivery of data.

- **UDP (User Datagram Protocol)**: UDP is a lightweight, connectionless protocol that provides faster communication by sacrificing reliability. It is commonly used for real-time applications like streaming and VoIP.

## DNS

DNS (Domain Name System) is a decentralized system that translates human-readable domain names (e.g., example.com) into IP addresses. It enables users to access websites using memorable domain names instead of IP addresses.

## Firewalls (stateless/stateful)

- **Stateless Firewalls**: Stateless firewalls filter network traffic based on predefined rules without considering the context or state of the network connection. They inspect each packet individually.

- **Stateful Firewalls**: Stateful firewalls maintain a state table that tracks the state of network connections. They analyze the context of each packet, including its source, destination, and connection status, to make more informed filtering decisions.

## CIDR/Subnetting

CIDR (Classless Inter-Domain Routing) is a method of allocating and addressing IP networks. It allows for more efficient use of IP addresses by using variable-length subnet masks (VLSM) to divide IP address space into smaller subnets.

## HTTP/HTTPS/SSL/TTL

- **HTTP (Hypertext Transfer Protocol)**: HTTP is a protocol used for communication between web browsers and web servers. It defines how clients request resources and servers respond with HTML pages, images, etc.

- **HTTPS (Hypertext Transfer Protocol Secure)**: HTTPS is a secure version of HTTP that uses encryption to protect the privacy and integrity of data exchanged between clients and servers. It uses SSL/TLS protocols to establish a secure connection.

- **SSL/TLS (Secure Sockets Layer/Transport Layer Security)**: SSL/TLS are cryptographic