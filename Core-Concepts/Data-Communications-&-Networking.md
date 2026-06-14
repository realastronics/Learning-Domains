# Data Communications \& Computer Networks

## 1\) Communication

Data Communication is the exchange of data between two devices via some transmission medium with a **protocol,** that is a set of rules that govern data communications. It represents an
agreement between the communicating devices.

#### Communication b/w two devices can be:

	1. **Simplex** - unidirectional communication only, one receiver and one sender, eg: Keyboard and traditional monitor. (When you "click" something in a program, it is usually a **mouse** sending data about a screen position, not the monitor itself. The computer uses the mouse's input to determine what object is being clicked and acts accordingly.)
1. **Half Duplex** - each station can both transmit and receive, but not at the same
time, eg: one way lane, walkie talkie
2. **Full Duplex** - both stations can transmit and receive simultaneously, eg: telephone

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

|Type|Full Form / Meaning|Range / Structure|Example|
|-|-|-|-|
|**PAN**|Personal Area Network|Very short range (few meters)|Bluetooth, phone hotspot|
|**LAN**|Local Area Network|Small area (room/building)|Home, college lab Wi-Fi|
|**MAN**|Metropolitan Area Network|City-wide network|City cable/internet network|
|**WAN**|Wide Area Network|Large geographic area|Internet|
|**P2P**|Peer-to-Peer|Devices communicate directly|Torrent sharing|
|**Broadcast / Multipoint**|One-to-many communication|Shared communication channel|Wi-Fi, radio transmission|

## 3\) Layers

### 3.1) OSI Model

The **Open Systems Interconnection (OSI)** model is a conceptual framework, defined by the ISO (International Standards Organization) in the 1970’s. Think of it as a **communication pipeline**, where **each layer has one responsibility** and only talks to the layer immediately above and below it.

**"All People Seem To Need Data Processing"**
Application → Presentation → Session → Transport → Network → Data Link → Physical

!\[image.png](b3f70486-edd7-4e78-8e69-e484dd85a956.png)

#### Explaning these 7 layers of the OSI Model:

1. **Physical Layer** - This is where actual transmission happens, having devices like **Hub and Rpeater**. It has **bits being sent physcially**. Singnal can be electrical, optical or radio waves, this is used to define voltage, frequency, connectors. Eg: Fibre Optic, Ethernet, Wifi Radio Waves.
2. **Data Link Layer -** The data link layer is responsible for moving frames from one hop (node) to the next.
3. **Network Layer -** This is the **“where”** of the communication, it is responsible for delivery of individual packets from the source to the destination host:

   1. IP Addressing: every device gets a logical address, eg- 192.168.1.10
   2. Routing: choses the best path for the communication
   3. Packet Forwarding: move packets hop by hop
4. **Transport Layer -** one of the **most important layers,** this controls the mechanism of data transfer:

   1. Segmentation: large data is broken down into smaller chunks
   2. Reliability:
   3. Ordering:
   4. Flow Control:
   5. Port Numbers:
5. **Session Layer -** This layer controls the session establishment, maintainence, synchronization and termination,
6. **Presentaiton Layer -** It has 3 main jobs, **Translation, Encryption, and Compression.** These make sure the host systems are on a uniform and fast layer for all commuicatoin
7. **Applicatoin Layer -** This is the highest layer, closest to the end-user, what applications like Chrome, Spotify use to access the network. It defines the protocols for specific services, eg: HTTP, SMTP, DNS, SSH

### 3.2) TCP/IP Protocol Suite

#### Addresses in TCP/IP protocols

## 4\) Devices

|Device|One-Line Definition|Main Function|OSI Layer|
|-|-|-|-|
|**Hub**|A device that sends received data to all connected devices.|Basic LAN connection|Layer 1|
|**Switch**|A device that forwards data to the correct device using MAC addresses.|Efficient LAN communication|Layer 2|
|**Router**|A device that routes packets between different networks using IP addresses.|Connects networks/Internet|Layer 3|
|**Repeater**|A device that regenerates weak signals to extend network range.|Signal strengthening|Layer 1|
|**Bridge**|A device that connects two LAN segments and filters traffic.|Reduces network congestion|Layer 2|
|**Modem**|A device that converts digital and analog signals for internet access.|Connects to ISP|Layer 1/2|
|**Gateway**|A device that enables communication between different protocols/networks.|Protocol translation|Layers 4–7|
|**Access Point (AP)**|A device that provides wireless access to a wired network.|Creates Wi-Fi network|Layer 2|
|**Firewall**|A security device that monitors and filters network traffic.|Network protection|Layers 3–7|
|**NIC (Network Interface Card)**|Hardware that enables a device to connect to a network.|Network connectivity|Layer 2|
|**Server**|A computer that provides resources or services to clients.|Hosts files/websites/services|Layers 5–7|
|**Client**|A device or software that requests services from a server.|Uses network services|Layers 5–7|

### Parity Check:

Even parity, the number of one’s must be even in the message, and for odd they must be odd. The idea is we add an additional number, (1 when we need to change the parity, 0 when the parity is matching) to the message.

eg - in the number 110010, the odd parity bit would be 0 since the number of 1’s present is already odd, and if we were asking the event parity bit that would be 1.

The main flaw with parity bit check is if two bits flip in an even parity bit check we would never know.

### Checksum

You break data into equal chunks **add them all up**, take the **complement** (flip all bits), and send that complement as the checksum. The receiver adds everything including the checksum — if the result is all 1s, no error.

(when adding binary strings and you see 1+1/a carry, you wrap it around and add to the result, like 1+1 = 10, you retain the 0 at the origional place and add the one to the last place)

add image

### Cyclic Redundancy Check

This is the most powerful error *detector*. It's based on **binary division** — specifically, division using **XOR** (no carries, no borrows — just XOR each bit).

### The concept first:

* Sender takes the data, **appends zeros** (as many zeros as degree of divisor), divides by a **generator/divisor**, and the **remainder** becomes the CRC
* Sender transmits: **data + CRC**
* Receiver divides received message by same divisor — if remainder is **0**, no error

