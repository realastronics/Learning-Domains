# Data Communications \& Computer Networks

## 0) Fundamental Model
#### Key Metrics:

- Bandwidth - it is the maximum capacity of a link it terms of bits/sec.
- Throughput - this is the actual achieved transfer rate of bits/sec
- Latency - is the delay until data reaches the destination
- Jitter - is the variation in latency
- Loss - is the packets dropped
#### Core Issues:
The key issue with networking is physical constrains like Bandwidth limit, the speed of light, congestion, noise and failures.
#### Byte Stream Model:
is a communication abstraction where the network treats **data as a continuous, unstructured sequence of bytes** rather than distinct messages. It acts as a continuous conduit between the sender and receiver, leaving the application responsible for packaging and interpreting the data.
#### What is the internet?
The Internet is a globally distributed *packet-switched system* connecting billions of end systems through routers, links, and protocols. Data is broken into packets, routed hop-by-hop across multiple autonomous networks using IP, while higher-level protocols like TCP and HTTP provide reliable application communication.
#### Packet Switching
Instead of reserving a dedicated communication path, data is broken into self contained packets and each packet is routed independently through the network. This allows efficient sharing of network resources, better fault tolerance, and scalable communication.

In **circuit switching**, the communication channel becomes reserved (physically) and there is only one direct path between the sender and receiver, this is a faster method but much more resource intensive and inefficient, it will waste the bandwidth during a low traffic time. ex- Telephone Network, ISDN 
## 1\) Communication

Data Communication is the exchange of data between two devices via some transmission medium with a **protocol,** that is a set of rules that govern data communications. It represents an
agreement between the communicating devices.

#### Communication b/w two devices can be:

1. **Simplex** - unidirectional communication only, one receiver and one sender, ex: Keyboard and traditional monitor. (When you "click" something in a program, it is usually a **mouse** sending data about a screen position, not the monitor itself. The computer uses the mouse's input to determine what object is being clicked and acts accordingly.)
2. **Half Duplex** - each station can both transmit and receive, but not at the same
time, ex: one way lane, walkie talkie
3. **Full Duplex** - both stations can transmit and receive simultaneously, ex: telephone

## 2\) Networks:

A network is the interconnection of a set of devices capable of communication. A device can be a host/end-system (like Computer) or a connecting device like Modem.

#### A network has must be able to meet these 3 criteria:

1. **Performance** - is usually measured in by transit time, response time, **throughput** (bits/second going through the network), and **delay** (duration it takes a bit to travel through the network).
2. **Reliability** - the probability that a network will operate without failure over a specific period, ensuring consistent, dependable service delivery. It measures downtime and related things.
3. **Security** - is about protecting data from unauthorized access, damage, and having procedures for recovery incase of loss or breaches.

For networks there are two kind of **links** possible:

1. **point-to-point** - exclusive link shared by two devices (eg: infrared, satellite)
2. **multipoint** - link is shared by more than two devices, if all users are able to share it simultaneously then it’s a spatially shared connection, and if the users need to take turns then it’s a timeshared connection.

### 2.1) Topology of Networks

Topology refers to the way in which a network is laid out physically, it’s a geometrical representation. The 4 main types are:

!\[image.png](image.png)

1. **Mesh Topology** - every device is connected to every other device using a **point-to-point** link, **n(n-1)/2** is the total number of Full Duplex channels.
2. Star Topology - It has a central dedicated device connected to all hosts with point-to-point connection, called “**The Hub”.**
3. Bus Topolgy - It is a multipoint network with one long cable acts as a backbone.
4. Ring Topology - Each device has dedicated point-to-point connection with only the two
devices on either side of it forming a loop

### 2.2) Types of Networks

Networks can be classified into types based on the area of their coverage:

| Type                       | Full Form / Meaning       | Range / Structure             | Example                     |
| -------------------------- | ------------------------- | ----------------------------- | --------------------------- |
| **PAN**                    | Personal Area Network     | Very short range (few meters) | Bluetooth, phone hotspot    |
| **LAN**                    | Local Area Network        | Small area (room/building)    | Home, college lab Wi-Fi     |
| **MAN**                    | Metropolitan Area Network | City-wide network             | City cable/internet network |
| **WAN**                    | Wide Area Network         | Large geographic area         | Internet                    |
| **P2P**                    | Peer-to-Peer              | Devices communicate directly  | Torrent sharing             |
| **Broadcast / Multipoint** | One-to-many communication | Shared communication channel  | Wi-Fi, radio transmission   |

## 3\) Layers
#### Layering Principle
Networking is divided into layers where each layer solves a specific problem and provides services to the layer above. This enables abstraction, modularity, easier debugging, and interoperability across different hardware and protocols.
### 3.1) OSI Model
The **Open Systems Interconnection (OSI)** model is a conceptual framework consisting of **7-layers**, defined by the ISO (International Standards Organization) in the 1970’s. 

Think of the OSI model as a **communication pipeline**, where **each layer has one responsibility** and only talks to the layer immediately above and below it. This is like an ideal blueprint of how a network should work. OSI was a conceptual reference model; the Internet evolved around the **TCP/IP** (made by the Department of Defense) model, which better reflects real-world protocol stacks. 

**"All People Seem To Need Data Processing"**
Application → Presentation → Session → Transport → Network → Data Link → Physical

![[OSI Model Layers.png|350]]
#### Explaining the 7 layers of the OSI Model:

#### 1) Physical Layer 
This is where actual transmission happens, having devices like **Hub and Repeater**. It has **bits being sent physically**. Signal can be electrical, optical or radio waves, this is used to define voltage, frequency, connectors. Ex: Fiber Optic, Ethernet, Wi-fi Radio Waves.
#### a) Transmission Delay
It is the measure of how long it takes to push all the bits into the wire. 

	$TransmissionDelay = Packet Size ( in bits ) / Bandwidth ( bits/second )$`
##### b) Propagation Delay
Is the measure of how long until the bits reach the physical destination.

	$Propagation Delay = Distance / Propagation Speed$

The propagation speed depends on the material of the wire, like $copper = 2 * 10^8 m/s$

==for numerical questions, always remember to convert kbps, Mbps into bps.==

	$1 Kbps = 10^3 bps, 1 Mbps = 10^6 bps$
##### c) Attenuation
Is the measure of loss of signal power during travel. 

	$dB = 10 log_{10} ( P2 / P1 )$

where P1 = Original Power, P2 = Received Power
To fix attenuation, amplifiers and repeaters are used.
##### d) Noise
Is simply the unwanted signal interfering with desired signal, it's commonly caused by electrical interference, thermal noise, Wi-Fi interference.
##### e) SNR
Is the measure of how useful is the signal compared to noise, the higher our SNR the more clarity we will have.

	$SNR = Signal Power / Noise Power$
#### Transmission Media
Transmission media is the physical path through which signals travel from sender to receiver. It is of two types: **guided media** (twisted pair, coaxial, fiber optic) where signals travel through cables, and **unguided media** (radio, microwave, infrared) where signals propagate through free space.
#### 2) Data Link Layer
The Data Link Layer provides **node-to-node delivery** over a single physical link. Its purpose is to convert an unreliable raw bit pipe into a usable communication channel between directly connected devices. ex- communication between laptop-router, switch-server, router-router.

The core problem is that physical channels are noisy, shared, and imperfect. Data Link Layer solves these problems using framing, addressing, error detection, flow control, and medium access control.
##### a) Framing
Framing is the process of dividing a continuous bit stream into manageable units called **frames** by adding **headers and trailers**.  

Purpose:  
- Define frame boundaries  
- Carry MAC addresses  
- Add error detection information
##### b) Addressing (MAC)
MAC (Media Access Control) address is a unique identifier assigned to a network interface for communication on a local network.  

	IP decides -> which network; MAC decides -> which device on that network
##### c) Error Detection
Bits commonly flip due to thermal noise, interference, attenuation

	1. Parity
	2. Checksum
	3. CRC - most important, 
	4. Hamming Code
##### d) Flow Control
This is there to prevent a faster sender from overwhelming a slow receiver, it limits the amount of data that can be sent. ARQ ensures reliable transmission using acknowledgements (ACK), timers, and retransmissions. 

	1. Stop-and-Wait ARQ – send one frame and wait for ACK.
	2. Go-Back-N ARQ – send multiple frames; if one fails, retransmit it and all subsequent frames.
	3. Selective Repeat ARQ – retransmit only the lost/corrupted frames.
	
##### e) Multiple Access
Medium Access Control decides which device gets permission to transmit on a shared communication medium.

	1. ALOHA - simplest. transmit whenever, retry randomly. horrible efficiency.
	2. CSMA - Carrier Sense Multiple Access. Listen-if idle, send-otherwise wait.
	3. CSMA/CD - Collision Detection, used in old Ethernet Cables. Process was listen-transmit-detect-stop-backoff-retry.
	4. CSMA/CA - Collision Avoidance, this is used in Wi-Fi. It's needed because wireless device cannot reliably listen while transmitting. It uses random backoff and RTS/CTS.
	5. Token Passing - only node with token may transmit, token circulates randomly between transmitting devices.

==Wi-Fi cannot use Collision Detection because while transmitting, a wireless device’s own signal overwhelms incoming signals, so it cannot reliably listen to the channel at the same time.==
#### 3) Network Layer
This is the **“where”** of the communication, it is responsible for delivery of individual packets from the source to the destination host. It sends data grams to the Link layer:

   - [[#IP (Internet Protocol)|IP Address]]: every device gets a logical address, ex- 192.168.1.10 
   - **Forwarding**: 
   - **Routing**: When a packet arrives, the router sees the most matching path and forwards there. 
   - **Distance Vector**: 
   - **Link State/OSPF**: 
   - **Router Hoping**: The way packets move from one place to another is by jumping through different routers. They decide this using something called the "forwarding table"
   - **ARP**: 
   - **NAT** (Network Address Translation): is a networking technique used by routers to modify IP addresses while data is in transit. It allows multiple devices within a private local network to share a single, publicly routable IP address when accessing the internet. It was primarily designed for the IPv4 technology

==A hop is just: Router A sends packet to Router B over **some physical communication link**.==
#### 4) Transport Layer
The Transport Layer provides **end-to-end communication between processes (applications)** running on different hosts. While the Network Layer moves packets between machines, the Transport Layer ensures all data in communicated. Its major responsibilities include:

- **Segmentation:** Large application data is broken into smaller segments for transmission.
- **Reliability:** Lost data can be detected and retransmitted.
- **Ordering:** Segments arriving out of order can be reordered correctly.
- **Flow/Congestion Control:** Prevents a fast sender from overwhelming a slow receiver/congested network.
- **Multiplexing / Port Numbers:** Allows multiple applications (browser, Discord, game) to use the network simultaneously.

Two main transport protocols:

1. **TCP (Transmission Control Protocol)**: is a **connection-oriented, reliable byte-stream protocol**. It guarantees reliable and ordered delivery, retransmission of lost packets, & flow and congestion control.
   
2. **UDP (User Datagram Protocol)**: UDP is **connectionless and lightweight**. It provides no reliability, no ordering guarantees, no retransmissions, and minimal overhead. UDP is used when **low latency matters more than perfect delivery**, such as: gaming, voice calls, and DNS
#### 5) Session Layer
This layer controls the session establishment, maintenance, synchronization and termination,

#### 6) Presentation Layer
It has 3 main jobs, **Translation, Encryption, and Compression.** These make sure the host systems are on a uniform and fast layer for all communication

#### 7) Application Layer 
This is the highest layer, closest to the end-user, what applications like Chrome, Spotify use to access the network. It defines the protocols for specific services such as:

- HTTP: a client opens a connection to a server and sends requests, like **GET /index.html** request, which asks for the page. The server responds to the request with a numeric code (200, 400) about the status of the request and the linking information. It is all ascii text, used by RST APIs, MCPs. 
- DNS:
- SMTP:
- BitTorrent: The problem this addresses is of distributing huge files efficiently without central server overload. The way this works is breaking the data into pieces and splitting the load onto many clients, this scales much better.
##### DHCP (Dynamic Host Configuration Protocol)
DHCP automatically assigns network configuration to devices joining a network, including IP address, subnet mask, default gateway, and DNS server.

DHCP follows DORA process:
1. Discover
2. Offer
3. Request
4. Acknowledge

### 3.2) TCP/IP Model



#### Addresses in TCP/IP protocols

### 3.3) Encapsulation
Encapsulation is the process where *each layer adds its own header (and sometimes trailer)* to data from the layer above before passing it downward. It is the job of encapsulation to make sure all layers can function independently without, as each layers adds its own header so the adjacent layers need not understand the logic of every other layer.

Example:
Application Data
→ TCP Segment
→ IP Datagram
→ Ethernet Frame
→ Bits on wire

At the receiver, the reverse process happens: Decapsulation.

## 4\) Devices

| Device                           | One-Line Definition                                                         | Main Function                 | OSI Layer  |
| -------------------------------- | --------------------------------------------------------------------------- | ----------------------------- | ---------- |
| **Hub**                          | A device that sends received data to all connected devices.                 | Basic LAN connection          | Layer 1    |
| **Switch**                       | A device that forwards data to the correct device using MAC addresses.      | Efficient LAN communication   | Layer 2    |
| **Router**                       | A device that routes packets between different networks using IP addresses. | Connects networks/Internet    | Layer 3    |
| **Repeater**                     | A device that regenerates weak signals to extend network range.             | Signal strengthening          | Layer 1    |
| **Bridge**                       | A device that connects two LAN segments and filters traffic.                | Reduces network congestion    | Layer 2    |
| **Modem**                        | A device that converts digital and analog signals for internet access.      | Connects to ISP               | Layer 1/2  |
| **Gateway**                      | A device that enables communication between different protocols/networks.   | Protocol translation          | Layers 4–7 |
| **Access Point (AP)**            | A device that provides wireless access to a wired network.                  | Creates Wi-Fi network         | Layer 2    |
| **Firewall**                     | A security device that monitors and filters network traffic.                | Network protection            | Layers 3–7 |
| **NIC (Network Interface Card)** | Hardware that enables a device to connect to a network.                     | Network connectivity          | Layer 2    |
## 5) Error Detection
### Parity Check:

Even parity, the number of one’s must be even in the message, and for odd they must be odd. The idea is we add an additional number, (1 when we need to change the parity, 0 when the parity is matching) to the message.

ex - in the number 110010, the odd parity bit would be 0 since the number of 1’s present is already odd, and if we were asking the event parity bit that would be 1.

The main flaw with parity bit check is if two bits flip in an even parity bit check we would never know.

### Checksum

You break data into equal chunks **add them all up**, take the **complement** (flip all bits), and send that complement as the checksum. The receiver adds everything including the checksum — if the result is all 1s, no error.

(when adding binary strings and you see 1+1/a carry, you wrap it around and add to the result, like 1+1 = 10, you retain the 0 at the origional place and add the one to the last place)

add image

### Cyclic Redundancy Check

This is the most powerful error *detector*. It's based on **binary division** — specifically, division using **XOR** (no carries, no borrows — just XOR each bit).

#### The concept first:

* Sender takes the data, **appends zeros** (as many zeros as degree of divisor), divides by a **generator/divisor**, and the **remainder** becomes the CRC
* Sender transmits: **data + CRC**
* Receiver divides received message by same divisor — if remainder is **0**, no error

## 6) Protocol Deep Dives

### MAC Address
Media Access Control (MAC) address is a link-layer hardware identifier used for communication within a local network. MAC identifies the specific device/interface on a local link. Switches use MAC addresses to forward Ethernet frames inside LANs. IP helps reach the correct network; MAC helps reach the correct device within that network.

If two devices are on the same Wi-Fi (common router, different IPs) and exchange information, the packet does not travel through the internet, rather it checks for the same subnet using IP + subnet mask, then uses MAC for delivery.
### IP (Internet Protocol) 
IP is the core protocol of the Internet (Network Layer) responsible for moving packets across multiple interconnected networks using **logical addressing and routing**. When the Transport Layer (TCP/UDP) has data to send, *it passes a transport segment to IP, which encapsulates it inside an **IP datagram** containing an IP header and payload (`IP Header | Transport Segment`)*. 

The header typically contains the source IP, destination IP, TTL, protocol type (TCP/UDP), checksum, and fragmentation metadata. IP then passes the datagram to the Link Layer for local transmission.

IP provides **best-effort delivery**, meaning it attempts to deliver packets but guarantees **neither delivery, ordering, latency, nor duplicate prevention**. Packets may be dropped, delayed, duplicated, or arrive out of order; reliability is usually handled by higher-layer protocols like TCP. A major strength of IP is that it is **link-layer agnostic**—it works over Ethernet, Wi-Fi, fiber, 5G, satellite, etc., making the Internet highly interoperable.

Important fields:
- **TTL (Time To Live):** Prevents infinite routing loops by decrementing at every router; packet is discarded at 0.
- **Header Checksum:** Detects corruption in the IP header (not payload).
- **Fragmentation:** Splits large packets when the next link’s MTU is smaller; fragments are reassembled at the destination (less common in modern networks).

There are two commonly used types of IPs used, IPv4 (32 bit) and IPv6 (128 bit).
### TCP (Transport Layer Protocol)
TCP is used when **every byte matters**, like websites (HTTP/1, HTTP/2), databases, APIs, file transfer. Before sending data, TCP establishes a connection using a **3-way handshake** to ensure both sides can send and receive, and to synchronize sequence numbers. 

A 2-way handshake is insufficient because the server cannot know whether the client successfully received the server’s response. The third ACK confirms bidirectional readiness and synchronizes connection state.
## 7) Real Packet Journey

1. Browser checks cache
2. DNS resolves domain → IP
3. OS determines route
4. ARP finds router MAC
5. Packet leaves machine
6. Routers forward packet
7. Connection established (TCP / QUIC)
8. TLS handshake
9. HTTP request
10. Response returns
11. Browser renders page

This learning is being accompanies by practical expose to linux commands and lab experience, using oracle virtualbox VM on Ubuntu distro.

![[DCCN Mind Map.png|700]]

