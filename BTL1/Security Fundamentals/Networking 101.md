## TCP 

**Transmission Control Protocol** (TCP) is a connection-oriented protocol that allows two systems to establish a connection that will enable the two-way transmission of data. Any data loss is detected and automatically corrected, which is why TCP is a reliable protocol. TCP works at the transport layer in the OSI model.

But how exactly do systems communicate with each other using TCP? A process referred to as the "three-way handshake" is conducted. To start, both systems must have unique IP addresses and have assigned and enabled the port for the data transfer. The IP address works as a primary identifier, while the specified port allows the operating system to assign connections to the specific client and server programs.

1. The requesting client sends the server an SYN (synchronize) packet with a random number, which ensures that data is sent in the right order and nothing is missed.
2. The server receives the packet and accepts the connection by sending an SYN-ACK (synchronize acknowledgment) packet back to the client, including the client's sequence number plus 1. It also transmits its own sequence number to the requesting client.
3. Finally, the **client** acknowledges the receipt of the SYN-ACK segment by sending its own **ACK packet**, which in this case contains the server's sequence number plus 1. At the same time, the client can already begin transferring data to the server.

![[Pasted image 20250210120225.png]]
![[Pasted image 20250210120247.png]]
## UDP

**User Datagram Protocol** (UDP) is a protocol that allows datagrams to be sent without connection in IP-based networks. To achieve the desired services on the target hosts, it uses ports that are listed as one of the core components in the UDP header.

- **UDP is connectionless**: Data transport via UDP is characterized by the fact that it takes place without an existing connection between the addressee and recipient.
- **UDP uses ports**: Like TCP, UDP uses ports so that the packets are transferred to the correct subsequent protocols or the desired applications on the target system.
- **UDP enables fast, delay-free communication**: The transport protocol is suitable for fast data transmission due to the lack of connection setup.
- **UDP does not guarantee the security and integrity of the data**: The absence of mutual authentication between addressee and recipient ensures the excellent transmission speed of UDP – however, the protocol can neither guarantee the completeness nor the security of the data packets.

## ICMP

Have you ever pinged an IP address or domain to see if you can reach it? This process uses ICMP. The **Internet Control Message Protocol** is an internet layer protocol used by network devices to diagnose network communication issues.

Commonly, the ICMP protocol is used on network devices, such as routers.

## IP Adresses

An **Internet Protocol** (IP) address provides an identity to a networked device on the internet.

Can be:
	**Private IP**: are used inside a network (a home network that is used by tablets, Wi-Fi cameras, wireless printers, and desktop PCs)
	**Public IP**: These are used on the outside of a network and are assigned by an ISP.
	**Static and Dynamic**: means that, respectively, they either change or they don't.

## MAC Adresses

A **Media Access Control** (MAC) address is a hardware identification number that uniquely identifies each device on a network.

# OSI

![[Pasted image 20250210121202.png]]

#### **Step 1. The Application Layer (Layer 7)**

This layer (also known as a high-level layer) is one of only 2 layers that the user can interact with. The Application layer is in charge of providing an interface to the user to interact, communicate, and even give commands to the computer. In this one, you will find e-mail applications, web browsers, file transfer applications, etc.

Some application layer protocols include HTTP as well as SMTP (Simple Mail Transfer Protocol is one of the protocols that enables email communications).

#### **Step 2. The Presentation Layer (Layer 6)**

This layer is considered the "translator" between the machine and the user. It is in charge of guaranteeing that the data is understandable for the applications that will be operated by the user, allowing its correct visualization. And is also responsible for the encryption and decryption of the incoming and outgoing data.

#### **Step 3. The Session Layer (Layer 5)**

The session layer is responsible for managing sessions between machines to enable communication between them. It is responsible for handling the opening, closing, and resetting of sessions (to ensure proper communication between both parties), and is in charge of establishing the order of communication between a sender and a receiver, among many other activities of this nature.

#### **Step 4. The Transport Layer (Layer 4)**

The transport layer is responsible for the transparent transfer of data between two computers. It assembles and fragments the packets that will be sent in the communication, while providing different mechanisms for verifying the integrity, to ensure that the information reaches the system accurately (some of these are error control, flow control, control of congestion, and re-sending of information, in case there is a failure in the communication).

#### **Step 5. The Network Layer** **(Layer 3)**

The network layer is responsible for redirecting the connection and transferring the data between two different networks by physical means, in search of the best path that allows this data to reach its destination in the shortest time possible.

#### **Step 6. The Data Link Layer (Layer 2)**

This layer is in charge of the addressing and physical transmission of the data, carrying out its encapsulation, and separating them into frames that will be easily directed by the physical transfer media.

#### **Step 7. The Physical Layer (Layer 1)**

This layer (also known as a low-level layer) is another of the 2 layers that can be manipulated by the user, since, in this case, it includes the physical elements of the networks (ethernet cables, optical fiber, etc.) responsible for the topology and the global connections from the computer to the network that allows the transmission and the physical operation of the system.

# Network Devices

#### **Router**

A router is a network device that forwards data based on a logical address. In the case of TCP/IP networks, the router would forward data based on the IP addresses of systems. If you're on your home network and want to visit Google.com, your request will go to the router (DNS will convert the domain name Google.com into the IP address), and your request will be sent over the internet to the Google.com web server IP.

![[Pasted image 20250210121440.png]]

#### **Hub**

A hub is a network device that connects all devices on a Local-Area-Network or LAN. When a system sends data to the hub on one port, the hub will broadcast these to all other attached devices (see image below). Hubs can be referred to as "dumb" devices because they do not understand who is the intended recipient of the data that has been received, so it sends it to all devices. Although the data will eventually reach the intended system, it generates unnecessary traffic, and can also allow attackers to steal data. If an attacker is connected to a hub, whenever any connected host sends data, it will be sent to every other host, including the attacker's machine!

![[Pasted image 20250210121508.png]]

#### **Switch**

A switch works as a smart version of a hub because it actually understands where to send data, instead of sending it to everyone. It achieves this by using MAC addresses as unique identifiers for recipients of incoming data, so it can send it to the right system. In this diagram below, if the Desktop Computer wants to print a document, they would send the request which would reach the Network Switch, which will know to send it to the Printer as the Desktop Computer will include the MAC address in the request (which is gained by using Address Resolution Protocol, or ARP).

![[Pasted image 20250210121545.png]]
#### **Bridge**

A network bridge device works to connect separate networks to make them into one larger network. This is different than a router, which allows networks to be connected but work independently. In the OSI model, bridging works at Layer 2, the Data Link Layer.

![[Pasted image 20250210121608.png]]

#### **Firewall**

A firewall is a network device that provides fundamental network security, by monitoring incoming and outgoing traffic and determining whether to allow or block it, based on rules. Firewalls can come in software form or hardware form as physical devices that are plugged into the network infrastructure. This allows us to create private networks, where only intended communications can come in, or out. We have an activity later in the course where you'll set up your own PfSense firewall to better understand how rules work!

![[Pasted image 20250210121632.png]]

# Protocols and Ports

In computer networking, a port is a communication endpoint. At the software level, a port identifies a specific process or a type of network service.

#### **Port 20, 21 - File Transfer Protocol (FTP)**

This protocol is used to transfer files between systems, where users can connect to an FTP product and can view, upload, or download them. An example of usage would be a company using a server for file storage, where employees can connect in via FTP and retrieve files. FTP is extremely insecure as the communication is in clear text, including the username and password used, which can easily be captured by attackers that are listening to network traffic.

#### **Port 22 - Secure Shell (SSH)**

SSH allows users to connect to a remote host, such as a server if they have SSH open. This channel is encrypted, so any data moved between two connected systems will not be clearly visible. An example of usage would be an IT technician using SSH to connect to a server from their desktop to carry out maintenance.

#### **Port 23 - Telnet**

This service was used before SSH and offers the same functionality, however, Telnet does not use encryption, so the traffic can be captured and read by an attacker. Telnet should not be used due to this weakness, and SSH should always be implemented instead.

#### **Port 25 - Simple Mail Transfer Protocol (SMTP)**

This protocol is used to send emails between servers within the network, or to external networks, such as over the internet. This is just a transport method, to actually download and view emails you need to use an email client and the protocol POP or IMAP.

#### **Port 53 - Domain Name System (DNS)**

DNS operates on TCP and UDP ports 53 and uses relational databases to convert human-readable hostnames and domain names (such as Google.com) into their respective IP addresses so that communications can be sent to and from these hosts. The reason we use domain names is that they're easy to remember. You remember **securityblue.team**, but you probably won't remember **3.9.68.12**!

#### **Port 67, 68 - Dynamic Host Configuration Protocol (DHCP)**

DHCP is designed to assign IP address-related information to any hosts on the network automatically, such as the subnet mask and IP address. When you connect your phone to your network, it is assigned an IP on the network because of the dynamic host configuration protocol. DHCP uses 2 ports; UDP port 67 and UDP port 68.

#### **Port 80 - Hypertext Transfer Protocol (HTTP)**

HTTP allows clients (browsers such as Chrome and Firefox) to connect to web servers and request content, which appears in the form of file downloads, web pages, and streaming services. 
So if you want to view the securityblue.team homepage, your browser will make an HTTP request to our web server, requesting to download the HTML web page. 
The server will respond with a 200 status code (which means "OK", it has been successful) and then send the HTML page to the client, so you can view it on your screen. As HTTP is not encrypted, it is possible to conduct sniffing attacks and see cleartext data as it is transmitted between the client and the server, such as passwords.

#### **Port 443 - Hypertext Transfer Protocol Secure (HTTPS)**

HTTPS is a secure version of HTTP and has the same functionality of retrieving content from web servers. However, the difference between the two is that HTTPS uses encryption to protect the transfer of data between a web server and a client. How do you turn HTTP into HTTPS? 
You need to use Transport Layer Security (TLS) formerly known as Secure Socket Layer (SSL). Sites that use HTTPS are less susceptible to man-in-the-middle and sniffing attacks.

#### **Port 514 - Syslog (UDP)**

A Syslog server will have port 514 open and listening for incoming Syslog notifications, transported by UDP protocol packets. These packets are generated by remote systems that have been set up to forward Syslog information to the server. This is typically used to send information about IT systems to a SIEM platform so that devices can be monitored for security events or issues.

#### **Port 3389 - Remote Desktop Protocol (TCP)**

Remote Desktop Protocol (RDP) is a Microsoft proprietary protocol that enables remote connections to other computers, typically over TCP port 3389.