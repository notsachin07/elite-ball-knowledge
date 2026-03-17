# 📡 TCP/IP: The Internet Protocol Suite

> *"TCP/IP is to networking what oxygen is to breathing - essential and everywhere."*

![TCP/IP Layers](../images/Internet/tcp-ip-layers.jpg)

---

## 📚 Table of Contents
- [What is TCP/IP?](#what-is-tcpip)
- [The TCP/IP Model](#the-tcpip-model)
- [Layer 1: Network Access (Link)](#layer-1-network-access-link)
- [Layer 2: Internet Layer](#layer-2-internet-layer)
- [Layer 3: Transport Layer](#layer-3-transport-layer)
- [Layer 4: Application Layer](#layer-4-application-layer)
- [TCP vs UDP](#tcp-vs-udp)
- [Ports and Sockets](#ports-and-sockets)
- [How TCP Ensures Reliability](#how-tcp-ensures-reliability)
- [Real-World Data Flow](#real-world-data-flow)

---

## 🤔 What is TCP/IP?

**TCP/IP** is the foundational protocol suite that makes the Internet work. It's a set of rules that governs how data is transmitted across networks.

```
┌─────────────────────────────────────────────────────────────────┐
│                    TCP/IP IN A NUTSHELL                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  TCP/IP is actually TWO protocols working together:             │
│                                                                  │
│  📦 IP (Internet Protocol)                                      │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Handles ADDRESSING and ROUTING                         │   │
│  │  • Gets packets from A to B                               │   │
│  │  • Like the postal system addressing                      │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🤝 TCP (Transmission Control Protocol)                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Handles RELIABLE DELIVERY                              │   │
│  │  • Makes sure all data arrives correctly                  │   │
│  │  • Like registered mail with confirmation                 │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  Together: TCP/IP = The Internet's Communication System         │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Why TCP/IP Matters

| Without TCP/IP | With TCP/IP |
|----------------|-------------|
| No standardized communication | Universal protocol |
| Each network speaks different language | One language for all |
| Can't connect different networks | Internet becomes possible! |
| Data gets lost, no one knows | Reliable delivery guaranteed |

---

## 🏗️ The TCP/IP Model

The TCP/IP model has 4 layers (compared to OSI's 7 layers).

### The 4 Layers

```
┌─────────────────────────────────────────────────────────────────┐
│                    TCP/IP MODEL (4 Layers)                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Layer 4    ┌───────────────────────────────────────────────┐  │
│   APPLICATION│  HTTP, HTTPS, FTP, SMTP, DNS, SSH             │  │
│              │  User-facing protocols                         │  │
│              └───────────────────────────────────────────────┘  │
│                              │                                   │
│                              ▼                                   │
│   Layer 3    ┌───────────────────────────────────────────────┐  │
│   TRANSPORT  │  TCP, UDP                                      │  │
│              │  Reliable (TCP) or Fast (UDP) delivery        │  │
│              └───────────────────────────────────────────────┘  │
│                              │                                   │
│                              ▼                                   │
│   Layer 2    ┌───────────────────────────────────────────────┐  │
│   INTERNET   │  IP, ICMP, ARP                                 │  │
│              │  Addressing and routing                        │  │
│              └───────────────────────────────────────────────┘  │
│                              │                                   │
│                              ▼                                   │
│   Layer 1    ┌───────────────────────────────────────────────┐  │
│   NETWORK    │  Ethernet, WiFi, Fiber                         │  │
│   ACCESS     │  Physical transmission of bits                 │  │
│              └───────────────────────────────────────────────┘  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### TCP/IP vs OSI Model

```
    TCP/IP Model              OSI Model
    ────────────              ─────────
    
    ┌────────────┐         ┌────────────┐
    │ Application│ ◄─────► │ Application│ Layer 7
    │            │         ├────────────┤
    │            │         │Presentation│ Layer 6
    │            │         ├────────────┤
    │            │         │  Session   │ Layer 5
    └────────────┘         └────────────┘
    
    ┌────────────┐         ┌────────────┐
    │ Transport  │ ◄─────► │ Transport  │ Layer 4
    └────────────┘         └────────────┘
    
    ┌────────────┐         ┌────────────┐
    │  Internet  │ ◄─────► │  Network   │ Layer 3
    └────────────┘         └────────────┘
    
    ┌────────────┐         ┌────────────┐
    │  Network   │ ◄─────► │ Data Link  │ Layer 2
    │  Access    │         ├────────────┤
    │            │         │  Physical  │ Layer 1
    └────────────┘         └────────────┘
    
    TCP/IP: Practical, used in real networks
    OSI: Theoretical, good for teaching
```

---

## 🔌 Layer 1: Network Access (Link)

The bottom layer handles the physical transmission of data.

### What Happens Here

```
┌─────────────────────────────────────────────────────────────────┐
│                    NETWORK ACCESS LAYER                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  This layer deals with:                                         │
│                                                                  │
│  🔌 Physical Medium                                             │
│     • Ethernet cables (Cat5, Cat6, Cat7)                       │
│     • Fiber optic cables                                        │
│     • WiFi radio waves                                          │
│     • Bluetooth                                                  │
│                                                                  │
│  📝 Framing                                                     │
│     • Wraps data in frames for transmission                    │
│     • Adds source/destination MAC addresses                    │
│                                                                  │
│  🔢 MAC Addresses                                               │
│     ┌──────────────────────────────────────────────────────┐   │
│     │  Example: AA:BB:CC:DD:EE:FF                          │   │
│     │                                                       │   │
│     │  • 48 bits (6 bytes)                                 │   │
│     │  • Burned into hardware (mostly)                     │   │
│     │  • Unique to each network interface                  │   │
│     │  • First 3 bytes: Manufacturer                       │   │
│     │  • Last 3 bytes: Device ID                           │   │
│     └──────────────────────────────────────────────────────┘   │
│                                                                  │
│  Technologies: Ethernet, WiFi (802.11), PPP, DSL              │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Ethernet Frame Structure

```
┌──────────────────────────────────────────────────────────────────┐
│                     ETHERNET FRAME                                │
├────────────┬────────────┬────────────┬────────────┬─────────────┤
│  Preamble  │ Dest MAC   │ Source MAC │   Type     │   Payload   │
│  8 bytes   │ 6 bytes    │ 6 bytes    │  2 bytes   │ 46-1500 B   │
├────────────┴────────────┴────────────┴────────────┴─────────────┤
│                            │                                     │
│                            │              ┌─────────────────────┤
│                            │              │        FCS          │
│                            │              │      4 bytes        │
│                            │              │   (Error check)     │
│                            │              └─────────────────────┘
└──────────────────────────────────────────────────────────────────┘
```

---

## 🌐 Layer 2: Internet Layer

This layer handles addressing and routing between networks.

### What Happens Here

```
┌─────────────────────────────────────────────────────────────────┐
│                    INTERNET LAYER                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Main Protocol: IP (Internet Protocol)                          │
│                                                                  │
│  📍 Addressing                                                  │
│     • Every device gets an IP address                          │
│     • IPv4: 192.168.1.1                                        │
│     • IPv6: 2001:db8::1                                        │
│                                                                  │
│  🗺️ Routing                                                     │
│     • Determines best path for packets                         │
│     • Routers use routing tables                               │
│     • Can take different paths to same destination             │
│                                                                  │
│  📦 Packetization                                               │
│     • Breaks data into IP packets                              │
│     • Each packet can travel independently                     │
│                                                                  │
│  Other Protocols:                                               │
│  • ICMP - Error messages, ping                                 │
│  • ARP - IP to MAC address resolution                          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### IP Packet Structure

```
┌─────────────────────────────────────────────────────────────────┐
│                       IPv4 PACKET                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │ 0                   1                   2               3 │  │
│  │ 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8│  │
│  ├───────────────┬───────────────┬───────────────────────────┤  │
│  │ Version │ IHL │    TOS        │       Total Length        │  │
│  ├───────────────┴───────────────┼───────────────────────────┤  │
│  │        Identification         │ Flags │  Fragment Offset  │  │
│  ├───────────────┬───────────────┼───────────────────────────┤  │
│  │      TTL      │   Protocol    │    Header Checksum        │  │
│  ├───────────────┴───────────────┴───────────────────────────┤  │
│  │                    Source IP Address                       │  │
│  ├───────────────────────────────────────────────────────────┤  │
│  │                  Destination IP Address                    │  │
│  ├───────────────────────────────────────────────────────────┤  │
│  │                    Options (if any)                        │  │
│  ├───────────────────────────────────────────────────────────┤  │
│  │                                                            │  │
│  │                        PAYLOAD                             │  │
│  │                    (TCP/UDP segment)                       │  │
│  │                                                            │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                  │
│  Important Fields:                                              │
│  • TTL: Hops remaining (prevents infinite loops)               │
│  • Protocol: What's inside (6=TCP, 17=UDP, 1=ICMP)            │
│  • Source/Dest IP: Where from, where to                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### ICMP: The Helper Protocol

```
┌─────────────────────────────────────────────────────────────────┐
│                    ICMP (Internet Control Message Protocol)      │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Used for network diagnostics and error messages.               │
│                                                                  │
│  📍 PING (Echo Request/Reply)                                   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  💻 ─── Echo Request ───► 🖥️                             │   │
│  │  💻 ◄── Echo Reply ────── 🖥️                             │   │
│  │                                                           │   │
│  │  $ ping google.com                                        │   │
│  │  64 bytes from 142.250.x.x: time=15ms                    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  🗺️ TRACEROUTE                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Uses TTL to discover path:                               │   │
│  │  TTL=1 → First router responds                           │   │
│  │  TTL=2 → Second router responds                          │   │
│  │  ... continues until destination                          │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ❌ Error Messages                                              │
│  • Destination Unreachable                                     │
│  • Time Exceeded                                               │
│  • Redirect                                                    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚚 Layer 3: Transport Layer

This layer manages end-to-end communication between applications.

### What Happens Here

```
┌─────────────────────────────────────────────────────────────────┐
│                    TRANSPORT LAYER                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Two Main Protocols:                                            │
│                                                                  │
│  🤝 TCP (Transmission Control Protocol)                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Connection-oriented                                    │   │
│  │  • Reliable, ordered delivery                             │   │
│  │  • Flow control & congestion control                      │   │
│  │  • Error detection & correction                           │   │
│  │  • Used by: HTTP, HTTPS, FTP, SMTP, SSH                  │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ⚡ UDP (User Datagram Protocol)                                │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  • Connectionless                                         │   │
│  │  • Fast, but unreliable                                   │   │
│  │  • No ordering guaranteed                                 │   │
│  │  • Minimal overhead                                       │   │
│  │  • Used by: DNS, VoIP, Gaming, Streaming                 │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  Key Functions:                                                 │
│  • Segmentation: Breaking data into segments                   │
│  • Multiplexing: Multiple apps share network                   │
│  • Port numbers: Identify specific applications                │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 💻 Layer 4: Application Layer

The top layer where user applications interact with the network.

### Common Application Protocols

```
┌─────────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  🌐 Web                                                         │
│     • HTTP (80) - Web pages                                    │
│     • HTTPS (443) - Secure web                                 │
│                                                                  │
│  📧 Email                                                       │
│     • SMTP (25/587) - Sending email                            │
│     • POP3 (110) - Receiving email                             │
│     • IMAP (143) - Receiving email (better)                    │
│                                                                  │
│  📁 File Transfer                                               │
│     • FTP (21) - File transfer                                 │
│     • SFTP (22) - Secure file transfer                         │
│                                                                  │
│  🖥️ Remote Access                                               │
│     • SSH (22) - Secure shell                                  │
│     • Telnet (23) - Insecure shell (legacy)                    │
│     • RDP (3389) - Windows remote desktop                      │
│                                                                  │
│  📍 Network Services                                            │
│     • DNS (53) - Domain name resolution                        │
│     • DHCP (67/68) - IP address assignment                     │
│     • NTP (123) - Time synchronization                         │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## ⚔️ TCP vs UDP

### The Fundamental Difference

```
┌─────────────────────────────────────────────────────────────────┐
│                    TCP vs UDP                                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  🤝 TCP = Phone Call 📞                                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  1. Dial number (connect)                                 │   │
│  │  2. Wait for answer (handshake)                          │   │
│  │  3. Have conversation (data transfer)                    │   │
│  │  4. Say goodbye (close connection)                       │   │
│  │                                                           │   │
│  │  ✅ You KNOW the other person heard you                  │   │
│  │  ✅ Can ask them to repeat if unclear                    │   │
│  │  ❌ Takes time to set up                                 │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ⚡ UDP = Sending a Postcard 📮                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  1. Write message                                         │   │
│  │  2. Drop in mailbox                                       │   │
│  │  3. Hope it arrives!                                      │   │
│  │                                                           │   │
│  │  ✅ Super fast, no waiting                               │   │
│  │  ✅ Can send many at once                                │   │
│  │  ❌ No confirmation of delivery                          │   │
│  │  ❌ Might arrive out of order                            │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Comparison Table

| Feature | TCP | UDP |
|---------|-----|-----|
| **Connection** | Connection-oriented | Connectionless |
| **Reliability** | Guaranteed delivery | Best-effort delivery |
| **Order** | Ordered | No ordering |
| **Speed** | Slower (overhead) | Faster |
| **Header Size** | 20-60 bytes | 8 bytes |
| **Error Checking** | Yes + correction | Basic checksum only |
| **Flow Control** | Yes | No |
| **Use Case** | Web, email, file transfer | Streaming, gaming, VoIP |

### Visual Comparison

```
    TCP: Reliable Delivery
    ─────────────────────
    
    💻 ─── Packet 1 ───► 🖥️
    💻 ◄─── ACK 1 ────── 🖥️  ✅ Confirmed
    
    💻 ─── Packet 2 ───► 🖥️
    💻 ◄─── ACK 2 ────── 🖥️  ✅ Confirmed
    
    💻 ─── Packet 3 ───► ❌ (Lost!)
    💻 ─── (timeout) ───
    💻 ─── Packet 3 ───► 🖥️  (Retransmit)
    💻 ◄─── ACK 3 ────── 🖥️  ✅ Confirmed
    
    
    UDP: Fire and Forget
    ────────────────────
    
    💻 ─── Packet 1 ───► 🖥️
    💻 ─── Packet 2 ───► 🖥️
    💻 ─── Packet 3 ───► ❌ (Lost! Oh well...)
    💻 ─── Packet 4 ───► 🖥️
    💻 ─── Packet 5 ───► 🖥️
    
    No waiting, no confirmation!
```

### When to Use What

```
┌─────────────────────────────────────────────────────────────────┐
│                    WHEN TO USE TCP vs UDP                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  USE TCP WHEN:                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  ✓ Data must arrive completely and correctly             │   │
│  │  ✓ Order matters                                         │   │
│  │  ✓ Reliability > Speed                                   │   │
│  │                                                           │   │
│  │  Examples:                                                │   │
│  │  • Web browsing (HTTP/HTTPS)                             │   │
│  │  • Email (SMTP, IMAP)                                    │   │
│  │  • File downloads (FTP)                                  │   │
│  │  • SSH terminal sessions                                 │   │
│  │  • Database queries                                       │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  USE UDP WHEN:                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  ✓ Speed > Reliability                                   │   │
│  │  ✓ Small delays are worse than lost data                 │   │
│  │  ✓ Real-time is important                                │   │
│  │                                                           │   │
│  │  Examples:                                                │   │
│  │  • Video streaming (Netflix, YouTube)                    │   │
│  │  • Voice calls (VoIP, Zoom)                              │   │
│  │  • Online gaming                                         │   │
│  │  • DNS queries                                           │   │
│  │  • Live sports broadcasts                                 │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚪 Ports and Sockets

### What Are Ports?

```
┌─────────────────────────────────────────────────────────────────┐
│                    PORTS EXPLAINED                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Think of it like an apartment building:                        │
│                                                                  │
│  🏢 IP Address = Building Address (192.168.1.1)                 │
│  🚪 Port = Apartment Number (:80, :443, :22)                    │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │                   192.168.1.1                           │    │
│  │  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐          │    │
│  │  │ :80  │ │ :443 │ │ :22  │ │ :25  │ │:3306 │          │    │
│  │  │ HTTP │ │HTTPS │ │ SSH  │ │ SMTP │ │MySQL │          │    │
│  │  └──────┘ └──────┘ └──────┘ └──────┘ └──────┘          │    │
│  │     ▲        ▲        ▲        ▲        ▲              │    │
│  │     │        │        │        │        │              │    │
│  │   Web    Secure    Remote   Email    Database         │    │
│  │  Server   Web      Shell   Server                      │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                  │
│  Port Range: 0 - 65535 (16-bit number)                         │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Port Categories

```
┌─────────────────────────────────────────────────────────────────┐
│                    PORT RANGES                                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  🔒 WELL-KNOWN PORTS (0 - 1023)                                 │
│     Reserved for common services (need root/admin)             │
│     ┌─────────────────────────────────────────────────────┐    │
│     │  20-21  FTP                                         │    │
│     │  22     SSH                                         │    │
│     │  23     Telnet                                      │    │
│     │  25     SMTP                                        │    │
│     │  53     DNS                                         │    │
│     │  80     HTTP                                        │    │
│     │  443    HTTPS                                       │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
│  📋 REGISTERED PORTS (1024 - 49151)                             │
│     Assigned by IANA for specific applications                 │
│     ┌─────────────────────────────────────────────────────┐    │
│     │  3306   MySQL                                       │    │
│     │  5432   PostgreSQL                                  │    │
│     │  6379   Redis                                       │    │
│     │  8080   HTTP alternate                              │    │
│     │  27017  MongoDB                                     │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
│  🎲 DYNAMIC/PRIVATE PORTS (49152 - 65535)                       │
│     Used for temporary connections (ephemeral ports)           │
│     Your browser uses these for outgoing connections           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### What is a Socket?

```
┌─────────────────────────────────────────────────────────────────┐
│                    SOCKETS                                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  A SOCKET = IP Address + Port + Protocol                        │
│                                                                  │
│  It uniquely identifies a network connection:                   │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │                                                          │    │
│  │  Client Socket: 192.168.1.5:54321 (TCP)                 │    │
│  │  Server Socket: 142.250.190.14:443 (TCP)                │    │
│  │                                                          │    │
│  │  Together they form a CONNECTION:                       │    │
│  │  192.168.1.5:54321 ←─────► 142.250.190.14:443          │    │
│  │  (Your laptop)              (Google HTTPS)              │    │
│  │                                                          │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                  │
│  Multiple connections can exist to same server:                 │
│                                                                  │
│  192.168.1.5:54321 ←→ 142.250.190.14:443  (Tab 1)             │
│  192.168.1.5:54322 ←→ 142.250.190.14:443  (Tab 2)             │
│  192.168.1.5:54323 ←→ 142.250.190.14:443  (Tab 3)             │
│                                                                  │
│  Different source ports = different connections!               │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🤝 How TCP Ensures Reliability

### The Three-Way Handshake

```
┌─────────────────────────────────────────────────────────────────┐
│                TCP THREE-WAY HANDSHAKE                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  💻 Client                               🖥️ Server             │
│      │                                        │                  │
│      │  1. SYN (seq=100)                     │                  │
│      │     "Hey, wanna talk?"                │                  │
│      │─────────────────────────────────────► │                  │
│      │                                        │                  │
│      │  2. SYN-ACK (seq=300, ack=101)        │                  │
│      │     "Sure! I heard you."              │                  │
│      │ ◄─────────────────────────────────────│                  │
│      │                                        │                  │
│      │  3. ACK (ack=301)                     │                  │
│      │     "Great, I heard you too!"         │                  │
│      │─────────────────────────────────────► │                  │
│      │                                        │                  │
│      │     ═══════════════════════════       │                  │
│      │        CONNECTION ESTABLISHED          │                  │
│      │     ═══════════════════════════       │                  │
│      │                                        │                  │
│      │  Now data transfer can begin!         │                  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Sequence Numbers & Acknowledgments

```
┌─────────────────────────────────────────────────────────────────┐
│                RELIABLE DATA TRANSFER                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  💻 Client                               🖥️ Server             │
│      │                                        │                  │
│      │  Data (seq=1, 100 bytes)              │                  │
│      │─────────────────────────────────────► │                  │
│      │                                        │                  │
│      │  ACK (ack=101)                        │                  │
│      │  "Got bytes 1-100, send 101 next"     │                  │
│      │ ◄─────────────────────────────────────│                  │
│      │                                        │                  │
│      │  Data (seq=101, 100 bytes)            │                  │
│      │─────────────────────────────────────► │                  │
│      │                                        │                  │
│      │  ACK (ack=201)                        │                  │
│      │  "Got bytes 101-200, send 201 next"   │                  │
│      │ ◄─────────────────────────────────────│                  │
│      │                                        │                  │
│      │  Data (seq=201, 100 bytes)            │                  │
│      │────────────────────── ❌ (LOST!)      │                  │
│      │                                        │                  │
│      │  (Timeout - no ACK received)          │                  │
│      │                                        │                  │
│      │  Data (seq=201, 100 bytes)            │                  │
│      │  (RETRANSMIT)                         │                  │
│      │─────────────────────────────────────► │                  │
│      │                                        │                  │
│      │  ACK (ack=301)                        │                  │
│      │ ◄─────────────────────────────────────│                  │
│      │                                        │                  │
│  Lost packet was detected and resent! ✅                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Connection Termination (Four-Way)

```
┌─────────────────────────────────────────────────────────────────┐
│                TCP CONNECTION CLOSE                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  💻 Client                               🖥️ Server             │
│      │                                        │                  │
│      │  1. FIN                               │                  │
│      │     "I'm done sending"                │                  │
│      │─────────────────────────────────────► │                  │
│      │                                        │                  │
│      │  2. ACK                               │                  │
│      │     "OK, noted"                       │                  │
│      │ ◄─────────────────────────────────────│                  │
│      │                                        │                  │
│      │  3. FIN                               │                  │
│      │     "I'm done sending too"            │                  │
│      │ ◄─────────────────────────────────────│                  │
│      │                                        │                  │
│      │  4. ACK                               │                  │
│      │     "OK, goodbye!"                    │                  │
│      │─────────────────────────────────────► │                  │
│      │                                        │                  │
│      │     ═══════════════════════════       │                  │
│      │        CONNECTION CLOSED              │                  │
│      │     ═══════════════════════════       │                  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📦 Real-World Data Flow

### How Data Moves Through the Layers

```
┌─────────────────────────────────────────────────────────────────┐
│              DATA ENCAPSULATION & DECAPSULATION                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  SENDING (Encapsulation)                                        │
│                                                                  │
│  Application    │ "Hello World!" │                              │
│                 └────────────────┘                              │
│                         │                                        │
│                         ▼                                        │
│  Transport     ┌─────┬────────────────┐                         │
│                │ TCP │ "Hello World!" │                         │
│                └─────┴────────────────┘                         │
│                         │                                        │
│                         ▼                                        │
│  Internet      ┌────┬─────┬────────────────┐                    │
│                │ IP │ TCP │ "Hello World!" │                    │
│                └────┴─────┴────────────────┘                    │
│                         │                                        │
│                         ▼                                        │
│  Network       ┌──────┬────┬─────┬────────────────┬─────┐       │
│  Access        │ ETH  │ IP │ TCP │ "Hello World!" │ FCS │       │
│                └──────┴────┴─────┴────────────────┴─────┘       │
│                         │                                        │
│                         ▼                                        │
│                  10101100110010101... (bits on wire)            │
│                                                                  │
│                                                                  │
│  RECEIVING (Decapsulation) - Reverse process                    │
│                                                                  │
│  Network Access: Strip Ethernet header → Pass IP packet up     │
│  Internet: Strip IP header → Pass TCP segment up                │
│  Transport: Strip TCP header → Pass data to application        │
│  Application: "Hello World!" 🎉                                 │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Complete Example: Web Request

```
┌─────────────────────────────────────────────────────────────────┐
│          COMPLETE FLOW: GET google.com                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. APPLICATION LAYER                                           │
│     Browser creates: GET / HTTP/1.1                             │
│                      Host: google.com                           │
│                                                                  │
│  2. TRANSPORT LAYER (TCP)                                       │
│     ┌─────────────────────────────────────────────────────────┐ │
│     │ Source Port: 54321 (random)                              │ │
│     │ Dest Port: 443 (HTTPS)                                   │ │
│     │ Seq: 1000                                                │ │
│     │ Flags: PSH, ACK                                          │ │
│     │ Payload: HTTP request                                    │ │
│     └─────────────────────────────────────────────────────────┘ │
│                                                                  │
│  3. INTERNET LAYER (IP)                                         │
│     ┌─────────────────────────────────────────────────────────┐ │
│     │ Source IP: 192.168.1.5 (your IP)                        │ │
│     │ Dest IP: 142.250.190.14 (Google's IP)                   │ │
│     │ TTL: 64                                                  │ │
│     │ Protocol: 6 (TCP)                                        │ │
│     │ Payload: TCP segment                                     │ │
│     └─────────────────────────────────────────────────────────┘ │
│                                                                  │
│  4. NETWORK ACCESS LAYER (Ethernet)                             │
│     ┌─────────────────────────────────────────────────────────┐ │
│     │ Dest MAC: AA:BB:CC:DD:EE:FF (router)                    │ │
│     │ Source MAC: 11:22:33:44:55:66 (your NIC)                │ │
│     │ Type: 0x0800 (IPv4)                                      │ │
│     │ Payload: IP packet                                       │ │
│     │ FCS: checksum                                            │ │
│     └─────────────────────────────────────────────────────────┘ │
│                                                                  │
│  5. Physical transmission as electrical/light signals 📡       │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🧪 Hands-On Exercises

### Exercise 1: View Active Connections

```bash
# Windows
netstat -an

# Linux/Mac
netstat -tuln
# or
ss -tuln
```

### Exercise 2: Capture Packets (Wireshark)

```bash
# Install Wireshark
# https://www.wireshark.org/

# Filter for:
# - TCP three-way handshake: tcp.flags.syn==1
# - HTTP traffic: http
# - DNS queries: dns
```

### Exercise 3: Test TCP vs UDP

```bash
# TCP - reliable, confirmed
nc -v google.com 80

# UDP - fast, no confirmation  
nc -u -v 8.8.8.8 53
```

### Exercise 4: Check Open Ports

```bash
# See what's listening on your machine
# Linux/Mac
lsof -i -P -n | grep LISTEN

# Windows
netstat -an | findstr LISTENING
```

---

## 📖 Key Takeaways

```
┌──────────────────────────────────────────────────────────────┐
│                    KEY TAKEAWAYS                              │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  ✅ TCP/IP is the foundation of the Internet                │
│                                                               │
│  ✅ 4 Layers: Network Access → Internet → Transport →       │
│     Application                                               │
│                                                               │
│  ✅ TCP = reliable, ordered, connection-oriented             │
│                                                               │
│  ✅ UDP = fast, unreliable, connectionless                   │
│                                                               │
│  ✅ Ports identify applications (0-65535)                    │
│                                                               │
│  ✅ Socket = IP + Port + Protocol                            │
│                                                               │
│  ✅ TCP uses 3-way handshake and acknowledgments             │
│                                                               │
│  ✅ Data is encapsulated layer by layer                      │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## 🔗 Additional Resources

### 📹 Videos
- [TCP/IP Model Explained - PowerCert](https://www.youtube.com/watch?v=OTwp3xtd4dg)
- [TCP vs UDP - Fireship](https://www.youtube.com/watch?v=qqRYkcta6IE)
- [TCP 3-Way Handshake - Sunny Classroom](https://www.youtube.com/watch?v=xMtP5ZB3wSk)

### 📚 Documentation
- [RFC 793 - TCP](https://tools.ietf.org/html/rfc793)
- [RFC 768 - UDP](https://tools.ietf.org/html/rfc768)
- [RFC 791 - IP](https://tools.ietf.org/html/rfc791)

### 🛠️ Tools
- [Wireshark](https://www.wireshark.org/) - Packet analyzer
- [tcpdump](https://www.tcpdump.org/) - Command-line packet capture
- [netcat](http://netcat.sourceforge.net/) - Network utility

---

## ⏭️ What's Next?

Now that you understand TCP/IP, let's explore:

**[➡️ 06 - Routing & Switching: How Data Travels](./06-routing-and-switching.md)**

We'll learn:
- How routers find the best path
- Switching in local networks
- Routing protocols (BGP, OSPF)
- The journey of a packet across the Internet

---

<div align="center">

**🎓 Elite Ball Knowledge - Internet Fundamentals**

[← Previous: HTTP/HTTPS](./04-http-https-protocols.md) | [Home](./README.md) | [Next: Routing →](./06-routing-and-switching.md)

</div>
