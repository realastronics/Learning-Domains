# Data Communications \& Computer Networks

# 0) Fundamental Model
### Key Metrics:

- Bandwidth - it is the maximum capacity of a link it terms of bits/sec.
- Throughput - this is the actual achieved transfer rate of bits/sec
- Latency - is the delay until data reaches the destination
- Jitter - is the variation in latency
- Loss - is the packets dropped
### Core Issues:
The key issue with networking is physical constrains like Bandwidth limit, the speed of light, congestion, noise and failures.
### Byte Stream Model:
The byte stream model treats **data as a continuous, unstructured sequence of bytes.** While it is simple and universally applicable, it **lacks built-in awareness of boundaries**. This requires applications to manage framing, handle multithreaded stream access, and navigate complex character encoding boundaries manually. 
### What is the internet?
The Internet is a globally distributed *packet-switched system* connecting billions of end systems through routers, links, and protocols. Data is broken into packets, routed hop-by-hop across multiple autonomous networks using IP, while higher-level protocols like TCP and HTTP provide reliable application communication.
### Packet Switching
Instead of reserving a dedicated communication path, data is broken into self contained packets and each packet is routed independently through the network. This allows efficient sharing of network resources, better fault tolerance, and scalable communication.

In **circuit switching**, the communication channel becomes reserved (physically) and there is only one direct path between the sender and receiver, this is a faster method but much more resource intensive and inefficient, it will waste the bandwidth during a low traffic time. ex- Telephone Network, ISDN 
# 1\) Communication
Data Communication is the exchange of data between two devices via some transmission medium with a **protocol,** that is a set of rules that govern data communications. It represents an
agreement between the communicating devices.
#### Communication b/w two devices can be:

1. **Simplex** - unidirectional communication only, one receiver and one sender, ex: Keyboard and traditional monitor. (When you "click" something in a program, it is usually a **mouse** sending data about a screen position, not the monitor itself. The computer uses the mouse's input to determine what object is being clicked and acts accordingly.)
2. **Half Duplex** - each station can both transmit and receive, but not at the same
time, ex: one way lane, walkie talkie
3. **Full Duplex** - both stations can transmit and receive simultaneously, ex: telephone
# 2\) Networks:
A network is the interconnection of a set of devices capable of communication. A device can be a host/end-system (like Computer) or a connecting device like Modem.
#### A network has must be able to meet these 3 criteria:

1. **Performance** - is usually measured in by transit time, response time, **throughput** (bits/second going through the network), and **delay** (duration it takes a bit to travel through the network).
2. **Reliability** - the probability that a network will operate without failure over a specific period, ensuring consistent, dependable service delivery. It measures downtime and related things.
3. **Security** - is about protecting data from unauthorized access, damage, and having procedures for recovery incase of loss or breaches.

For networks there are two kind of **links** possible:

1. **point-to-point** - exclusive link shared by two devices (eg: infrared, satellite)
2. **multipoint** - link is shared by more than two devices, if all users are able to share it simultaneously then it’s a spatially shared connection, and if the users need to take turns then it’s a timeshared connection.

## 2.1) Topology of Networks
Topology refers to the way in which a network is laid out physically, it’s a geometrical representation. The 4 main types are:
![[network-topologies.png|470]]

1. **Mesh Topology** - every device is connected to every other device using a **point-to-point** link, **n(n-1)/2** is the total number of Full Duplex channels.
2. **Star Topology** - It has a central dedicated device connected to all hosts with point-to-point connection, called “**The Hub”.**
3. **Bus Topology** - It is a multipoint network with one long cable acts as a backbone.
4. **Ring Topology** - Each device has dedicated point-to-point connection with only the two
devices on either side of it forming a loop

## 2.2) Types of Networks
Networks can be classified into types based on the area of their coverage:

| Type                       | Full Form / Meaning       | Range / Structure             | Example                     |
| -------------------------- | ------------------------- | ----------------------------- | --------------------------- |
| **PAN**                    | Personal Area Network     | Very short range (few meters) | Bluetooth, phone hotspot    |
| **LAN**                    | Local Area Network        | Small area (room/building)    | Home, college lab Wi-Fi     |
| **MAN**                    | Metropolitan Area Network | City-wide network             | City cable/internet network |
| **WAN**                    | Wide Area Network         | Large geographic area         | Internet                    |
| **P2P**                    | Peer-to-Peer              | Devices communicate directly  | Torrent sharing             |
| **Broadcast / Multipoint** | One-to-many communication | Shared communication channel  | Wi-Fi, radio transmission   |

# 3\) Layers
#### Layering Principle
Networking is divided into layers where each layer solves a specific problem and provides services to the layer above. This enables abstraction, modularity, easier debugging, and interoperability across different hardware and protocols.
#### Encapsulation
Encapsulation is the process of wrapping application data with protocol-specific headers (and trailers) as it moves down the network stack. Each layer adds information required for communication with its corresponding layer on the receiving device.
At the destination, the reverse process is called **Decapsulation**, where each layer removes its own header before passing the data to the layer above.

                `Encapsulation`

`Application        Data`
        `↓`
`Transport          Segment`
        `↓`
`Network            Datagram`
        `↓`
`Data Link          Frame`
        `↓`
`Physical           Bits`

                `↓↓↓↓↓`

             `Transmission`

                `↑↑↑↑↑`

             `Decapsulation`

`Bits`
        `↑`
`Frame`
        `↑`
`Datagram`
        `↑`
`Segment`
        `↑`
`Data`
## 3.1) OSI Model
The **Open Systems Interconnection (OSI)** model is a conceptual framework consisting of **7-layers**, defined by the ISO (International Standards Organization) in the 1970’s. 

Think of the OSI model as a **communication pipeline**, where **each layer has one responsibility** and only talks to the layer immediately above and below it. This is like an ideal blueprint of how a network should work. OSI was a conceptual reference model; the Internet evolved around the **TCP/IP** (made by the Department of Defense) model, which better reflects real-world protocol stacks. 

**"All People Seem To Need Data Processing"**
Application → Presentation → Session → Transport → Network → Data Link → Physical

![[OSI Model Layers.png|350]]
#### Explaining the 7 layers of the OSI Model:

#### 3.1.1) Physical Layer 
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
#### 3.1.2) Data Link Layer
The Data Link Layer provides **node-to-node delivery** over a single physical link. Its purpose is to convert an unreliable raw bit pipe into a usable communication channel between directly connected devices. ex- communication between laptop-router, switch-server, router-router.

The core problem is that physical channels are noisy, shared, and imperfect. Data Link Layer solves these problems using framing, addressing, error detection, flow control, and medium access control.
##### a) Framing
Framing is the process of dividing a continuous bit stream into manageable units called **frames** by adding **headers and trailers**.  

Purpose:  
- Define frame boundaries  
- Carry [[#MAC Address|MAC addresses]]  
- Add error detection information
##### b) Addressing (MAC)
MAC (Media Access Control) address is a unique identifier assigned to a network interface for communication on a local network.  
`IP decides -> which network; MAC decides -> which device on that network`
##### c) Error Detection
Bits commonly flip due to thermal noise, interference, attenuation, etc. 
Covered in detail [[#5) Error Detection|here]]

	1. Parity
	2. Checksum
	3. CRC - most important, 
	4. Hamming Code

#### Sliding Window Protocol
The Sliding Window Protocol is a flow control mechanism in which the sender is allowed to transmit multiple packets before receiving acknowledgments, improving network utilization by keeping the communication channel continuously busy.
##### d) Flow Control
This is there to prevent a faster sender from overwhelming a slow receiver, it limits the amount of data that can be sent. **ARQ (Automatic Repeat Request)** is a family of protocols used to ensures reliable transmission using acknowledgements (ACK), timers, and retransmissions. 

ARQ works on a three 3 step idea, sender sends fame -> receiver sends ACK -> if ACK not received before timeout, resend.

	1. Stop-and-Wait ARQ – send one frame and wait for ACK, if no ack that means package lost, and re-transmit that one.
	2. Go-Back-N ARQ – send multiple frames; if one fails, retransmit it and all subsequent frames.
	3. Selective Repeat ARQ – retransmit only the lost/corrupted frames.
##### e) Multiple Access
Medium Access Control decides which device gets permission to transmit on a shared communication medium.

**Random Access:**
1. ALOHA - simplest. transmit whenever, retry randomly. horrible efficiency.
2. CSMA - Carrier Sense Multiple Access. Listen-if idle, send-otherwise wait.
3. CSMA/CD - Collision Detection, used in old Ethernet Cables. Process was listen-transmit-detect-stop-backoff-retry.
4. CSMA/CA - Collision Avoidance, this is used in Wi-Fi. It's needed because wireless device cannot reliably listen while transmitting. It uses random backoff and RTS/CTS.
5. CSMA Variants:
	1. 1-Persistent CSMA: Station transmits immediately when channel becomes idle; high collision probability.
	2. Non-Persistent CSMA: If channel is busy, station waits for a random time before retrying; reduces collisions but increases delay.
	3. p-Persistent CSMA: In slotted channels, station transmits with probability p when channel becomes idle and waits with probability 1-p.

**Controlled Access:**
Token Passing - only node with token may transmit, token circulates randomly between transmitting devices.

**Channelization**
- **FDMA (Frequency Division Multiple Access)** – Divides the communication channel into separate **frequency bands**, allowing multiple users to transmit simultaneously on different frequencies.
- **TDMA (Time Division Multiple Access)** – Allows users to share the same frequency by assigning each user a dedicated **time slot** for transmission.
- **CDMA (Code Division Multiple Access)** – Allows all users to transmit simultaneously on the same frequency and time by assigning each user a unique **orthogonal code** that separates their signals mathematically.

==Wi-Fi cannot use Collision Detection because while transmitting, a wireless device’s own signal overwhelms incoming signals, so it cannot reliably listen to the channel at the same time.==
#### ARP (Address Resolution Protocol)
Is a protocol that maps an IPv4 address to a MAC address within a local network so data link layer frames can be delivered correctly. It acts as a bridge between the Network Layer (IP addressing) and Data Link Layer (MAC addressing).

Working:
1. Sender knows destination IP but not MAC.
2. Sender broadcasts ARP request asking “Who has this IP?”
3. Target device replies with its MAC address.
4. Sender stores the mapping in ARP cache for future use.

If destination is outside the local subnet, ARP is used to obtain the MAC address of the default gateway instead of the final destination.
### 3.1.3) Network Layer
This is the **“where”** of the communication, it is responsible for delivery from the **source to the destination** host it does this across multiple interconnected networks, unlike Data Link Layer that just handles one-hop communication. 

The core responsibilities for it are:

	1. Logical Addressing (IP) - IP addresses uniquely identify devices on a network at the logical level. They allow routers to route packets between different networks.
	2. Routing - deides which path to take, it runs algorithms like Distance Vectors, Link State, OSPF, RIP, and BGP to deicde this.
	3. Forwarding - is local, it recevies the packet, checks the forwarding table and sends the packet to the next hop
	4. Fragmentation - is the process of dividing a large IP packet into smaller fragments when the next network link supports a smaller maximum transmission unit (MTU).
	5. Congestion Awareness - This layer must handle situations where packet arriva rate exceeds orwarding capacity, causing latency and queue. Congestion may be managed using buffering, packet dropping, and congestion control mechanisms (part of TCP). Actual congestion is handled by the Transport Layer.
#### IPv4 Datagram
An IPv4 datagram is the packet format used by the Internet Protocol to transmit data across multiple interconnected networks. It consists of an IP header and payload, where the payload usually contains a TCP or UDP segment.

The minimum size of IPv4 header is 20 bytes (since each layer must be 4 bytes) and maximum can be 60 bytes. Both the source IP and Destination IP are 4 bytes (32 bits) each. 
 ![[ipv4_packet_structure.webp| 500]]
#### Subnetting
A **subnet (subnetwork)** is a group of devices that can communicate directly at Layer 2 (Data Link Layer) without requiring a router. **Subnetting** is the process of dividing a large IP network into smaller logical subnetworks by borrowing bits from the host portion and converting them into additional network bits.
Its main goals are better IP utilization, reduced broadcast traffic, improved security, and easier routing/network management.

IPv4 addresses are **32 bits** long and consist of two parts: the **Network Portion**, which identifies the subnet, and the **Host Portion**, which identifies a device within that subnet.
#### CIDR (Classless Inter-Domain Routing)
This notation specifies how many bits belong to the network portion. For example, in `/24`, the first 24 bits are network bits and the remaining 8 bits are host bits.

Example:  
`/24 = 255.255.255.0`

Usable hosts in a subnet are calculated as:
`2^n - 2`
where `n` is the number of host bits. The `-2` accounts for the reserved **network address** and **broadcast address**.
##### Packet Traversal Across Routers (Hop-by-Hop Forwarding)
When a packet travels across multiple routers, the **IP packet survives end-to-end**, but the **Data Link frame changes at every hop**. This is because MAC addresses are only meaningful on a **local link (one hop)**, while IP addresses identify the original source and final destination across the entire Internet.

At each router, the incoming **frame header is stripped**, exposing the IP datagram inside. The router reads the **destination IP address**, consults its forwarding table to determine the next hop, decrements the **TTL**, recalculates the IP header checksum, and then encapsulates the same IP packet inside a **new frame** with new source and destination MAC addresses for the next link. Thus, **MAC addresses change hop-by-hop**, while **source and destination IP usually remain unchanged throughout the journey**.
##### NAT (Network Address Translation): 
is a networking technique used by routers to modify IP addresses while data is in transit. It allows multiple devices within a private local network to share a single, publicly routable IP address when accessing the internet. It was primarily designed for the IPv4 technology
##### Routing vs Forwarding
Routing is a global decision making and runs relatively infrequently, like when topology changes, link fails, or router joins. It outputs a Routing/Forwarding Table. Forwarding is a per-packet local action, the moment router receives packet, the table is checked and the packet is send to the next hop.
##### *Routing Algorithms*
- **Distance Vector Algorithm** - each router knows only it's neighbors, so it periodically tells it's **distance to every destination**. This is a simple and easy algorithm, however suffers from slow convergence, routing loops, and count-to-infinity problems. 
   
   RIP (Routing Information Protocol) is a protocol implementing Distance Vector, with a max hop limit = 15
   
- **Link State Routing** - every router builds a complete map of the network topology and computes the shortest path to all destinations using shortest path algorithms such as Dijkstra’s algorithm. It has fast convergence, better scalability and fewer loops, however suffers from higher memory and CPU usage.
   
   OSPF (Open Shortest Path First) - It is a Link State routing protocol that computes shortest paths using Dijkstra’s algorithm. Unlike RIP, it uses path cost instead of hop count and converges faster, making it more scalable for large networks.
   
 - **Path Vector** - routers advertise the **entire path (sequence of autonomous systems)** to a destination instead of just distance or topology, enabling **loop prevention** and **policy-based routing** across the Internet.
   
   BGP (Broad Gateway Protocol) - It is the routing protocol used to exchange routing information between autonomous systems on the Internet. It is policy-based and enables global Internet routing.

==A hop is just: Router A sends packet to Router B over **some physical communication link**==.
### 3.1.4) Transport Layer
The Transport Layer provides **end-to-end communication between processes (applications)** running on different hosts. While the Network Layer moves packets between machines, the Transport Layer ensures all data in communicated. Its major responsibilities include:

- **Segmentation:** Large application data is broken into smaller segments for transmission.
- **Reliability:** Lost data can be detected and retransmitted.
- **Ordering:** Segments arriving out of order can be reordered correctly.
- **Flow/Congestion Control:** mechanism that prevents a fast sender from overwhelming a slow receiver by regulating the amount of data that can be transmitted before receiving an acknowledgment.
- **Multiplexing / Port Numbers:** the process of combining data from multiple applications into a single outgoing data stream for transmission over the network, allows multiple applications to run simultaneously.

|Flow Control|Congestion Control|
|---|---|
|Protects the **receiver**|Protects the **network**|
|Receiver is slow|Routers are overloaded|
|Uses Receive Window|Uses Congestion Window|
|End-to-end|Network-wide|

**Port Numbers -** A **port number** is a logical identifier that uniquely identifies a running application or service on a host, allowing multiple network applications to communicate simultaneously over the same IP address. ex: Port 51023 - Chrome

**Socket -** A socket is an endpoint of communication between two applications and is uniquely identified by the combination of an IP address and a port number.

**Transport protocols:**
1. **TCP (Transmission Control Protocol)**: is a **connection-oriented, reliable byte-stream protocol**. It guarantees reliable and ordered delivery, retransmission of lost packets, & flow and congestion control.
   
2. **UDP (User Datagram Protocol)**: UDP is **connectionless and lightweight**. It provides no reliability, no ordering guarantees, no retransmissions, and minimal overhead. UDP is used when **low latency matters more than perfect delivery**, such as: gaming, voice calls, and DNS
### 3.1.5) Session Layer
This layer controls the session establishment, maintenance, synchronization and termination,
### 3.1.6) Presentation Layer
It has 3 main jobs, **Translation, Encryption, and Compression.** These make sure the host systems are on a uniform and fast layer for all communication
#### 3.1.7) Application Layer 
This is the highest layer, closest to the end-user, what applications like Chrome, Spotify use to access the network. It defines the protocols for specific services such as:

- HTTP: a client opens a connection to a server and sends requests, like **GET /index.html** request, which asks for the page. The server responds to the request with a numeric code (200, 400) about the status of the request and the linking information. It is all ascii text, used by RST APIs, MCPs. 
- DNS:
- SMTP:
- BitTorrent: The problem this addresses is of distributing huge files efficiently without central server overload. The way this works is breaking the data into pieces and splitting the load onto many clients, this scales much better.
#### DHCP (Dynamic Host Configuration Protocol)
DHCP automatically assigns network configuration to devices joining a network, including IP address, subnet mask, default gateway, and DNS server.

DHCP follows DORA process:
1. Discover
2. Offer
3. Request
4. Acknowledge
## 3.2) TCP/IP Model



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
Physical channels are noisy due to attenuation, interference, thermal noise, and signal distortion, causing bits to flip during transmission. Error control techniques are used to **detect** or **correct** corrupted data.

Error techniques are of two types:
- **Error Detection** → detects if corruption happened (Parity, Checksum, CRC)
- **Error Correction** → detects and fixes errors (Hamming Code)
Errors are commonly:
- **Single-bit error** → only one bit changes
- **Burst error** → multiple consecutive bits change (more common in real networks)
### 5.1 Parity Check:
Parity check is the simplest error detection technique where an extra bit called the **parity bit** is added to the data to make the total number of 1s either even or odd.  

Types:  
- **Even Parity** → total number of 1s must be even, ex- 110110 will have an even parity, since it has four number of 1s.
- **Odd Parity** → total number of 1s must be odd

However this check is very limited as any if two bits flip the error goes undetected.
### 5.2 Checksum
You break data into equal chunks **add them all up**, take the **complement** (flip all bits), and send that complement as the checksum. The receiver adds everything including the checksum — if the result is all 1s, no error.

(when adding binary strings and you see 1+1/a carry, you wrap it around and add to the result, like 1+1 = 10, you retain the 0 at the original place and add the one to the last place)
### 5.3 Cyclic Redundancy Check (CRC)
**Cyclic Redundancy Check (CRC)** detects transmission errors by performing **binary polynomial division using XOR instead of subtraction**.
#### The Concept
The sender and receiver agree on a fixed **generator (divisor)** beforehand.
1. The sender appends **(generator length − 1)** zeros to the original data. These zeros act as placeholders for the CRC bits.
2. The sender divides the modified data by the generator using **XOR division** (no carries or borrows).
3. The **remainder** obtained from the division is called the **CRC**.
4. The sender replaces the appended zeros with the CRC bits and transmits **Data + CRC**.
5. The receiver divides the received message by the **same generator**.
6. If the remainder is **0**, the message is assumed to be error-free. Otherwise, an error is detected.

> **Key Idea:** The sender constructs the transmitted message so that it is **exactly divisible** by the agreed generator. If even a single bit changes during transmission, this divisibility is usually lost, resulting in a non-zero remainder.

#### Example
Suppose:

Data = `101100`
Generator = `1101`
Generator length = **4**

Step 1: Append **( G - 1 ) zeros:** (`4−1=3`)
```
101100000
```
Step 2: Divide using XOR.
Suppose the remainder is:
```
101
```
Step 3: Replace the appended zeros with the remainder.
```
101100101
```

The transmitted message becomes:
```
Data + CRC = 101100101
```
At the receiver:
```
101100101 ÷ 1101
```
- Remainder = `000` → Accept the data.
- Non-zero remainder → Error detected.
### 5.4 Hamming Code
Hamming Code is an error correction technique that can detect and correct single-bit errors by inserting parity bits at positions that are powers of 2.
## 6) Protocol Deep Dives

### Ethernet Cable vs Ethernet Protocol
**Ethernet Cable** is the physical medium (e.g., Cat5e, Cat6, Cat7) that carries electrical signals between devices. It belongs to the **Physical Layer**.

**Ethernet Protocol (IEEE 802.3)** is the set of rules governing communication over a wired LAN. It defines frame format, MAC addressing, error detection (CRC), and medium access (CSMA/CD). It belongs primarily to the **Data Link Layer**. 
A cable without Ethernet is just a wire. Ethernet without a cable can even run over **fiber optics**.
### MAC Address
Media Access Control (MAC) address is a link-layer hardware identifier used for communication within a local network. MAC identifies the specific device/interface on a local link. Switches use MAC addresses to forward Ethernet frames inside LANs. IP helps reach the correct network; MAC helps reach the correct device within that network.

If two devices are on the same Wi-Fi (common router, different IPs) and exchange information, the packet does not travel through the internet, rather it checks for the same subnet using IP + subnet mask, then uses MAC for delivery.
### IP (Internet Protocol) 
IP is the core protocol of the Internet (Network Layer) responsible for moving packets across multiple interconnected networks using **logical addressing and routing**. When the Transport Layer (TCP/UDP) has data to send, *it passes a transport segment to IP, which encapsulates it inside an **IP datagram** containing an IP header and payload (`IP Header | Transport Segment`)*. 

The header typically contains the source IP, destination IP, TTL, protocol type (TCP/UDP), checksum, and fragmentation metadata. IP then passes the datagram to the Link Layer for local transmission.

IP provides **best-effort delivery**, meaning it attempts to deliver packets but guarantees **neither delivery, ordering, latency, nor duplicate prevention**. Packets may be dropped, delayed, duplicated, or arrive out of order; reliability is usually handled by higher-layer protocols like TCP. A major strength of IP is that it is **link-layer agnostic**—it works over Ethernet, Wi-Fi, fiber, 5G, satellite, etc., making the Internet highly interoperable.

Important fields:
- **TTL (Time To Live):** Prevents infinite routing loops by decrementing at every router; packet is discarded at 0. It gives every packet a "life" and incase of a network error with self routing, the life would send. This saves endless memory occupancy.
- **Header Checksum:** Detects corruption in the IP header (not payload).
- **Fragmentation:** Splits large packets when the next link’s MTU is smaller; fragments are reassembled at the destination (less common in modern networks).

There are two commonly used types of IPs used, IPv4 (32 bit) and IPv6 (128 bit).

==If the internet were built using **Media Access Control (MAC)** addresses instead of IP addresses for global routing, it would simply break. Because MAC addresses are flat and lack geographical or hierarchical structure, routers would have to test every single device on earth to find a destination, causing routing tables to explode and the internet to become instantly unscalable.==
### TCP (Transport Layer Protocol)
TCP is used when **every byte matters**, like websites (HTTP/1, HTTP/2), databases, APIs, file transfer. Before sending data, TCP establishes a connection using a **3-way handshake** to ensure both sides can send and receive, and to synchronize sequence numbers. 

A 2-way handshake is insufficient because the server cannot know whether the client successfully received the server’s response. The third ACK confirms bidirectional readiness and synchronizes connection state.
### Protocol Data Unit (PDU)
A **Protocol Data Unit (PDU)** is the unit of data exchanged at a particular layer of the OSI or TCP/IP model. As data moves down the network stack, each layer encapsulates it by adding its own header (and sometimes a trailer), creating a new PDU specific to that layer.

How PDU moves from the Browser to the bits:
```
Browser
↓
HTTP Request (Application Data)
↓
TCP adds TCP Header
= TCP Segment
↓
IP adds IP Header
= IP Datagram
↓
Ethernet/Wi-Fi adds Frame Header + Trailer
= Frame
↓
Physical Layer
= Bits
```
## Real Packet Journey

1. User enters a URL in the browser.
2. Browser checks cache for the requested resource.
3. DNS resolves the domain name to an IP address.
4. Operating System determines the best route.
5. ARP resolves the next-hop MAC address (usually the default gateway).
6. Data is encapsulated into a Frame and transmitted.
7. Routers forward the packet across networks.
8. Destination establishes a connection (TCP or QUIC).
9. TLS handshake establishes encryption (HTTPS).
10. HTTP request and response are exchanged.
11. Browser receives the response, renders the webpage, and displays it to the user.

```
User enters URL
        ↓
DNS Lookup
        ↓
TCP Connection (or QUIC)
        ↓
TLS Handshake (HTTPS)
        ↓
HTTP Request
        ↓
IP
        ↓
Ethernet/Wi-Fi
        ↓
Bits
```
This learning is being accompanies by practical expose to linux commands and lab experience, using oracle virtualbox VM on Ubuntu distro.

![[DCCN Mind Map.png|700]]

