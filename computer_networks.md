# 🌐 Computer Networks — Interview Questions & Answers

> A comprehensive quick-reference guide covering the most frequently asked Computer Networks questions in product-based company interviews.

---

## 1. Introduction to Computer Networks

### Q1. What is a Network?

A **network** is a collection of two or more computers and devices connected together to share resources (files, printers, internet) and communicate with each other. Devices in a network communicate through defined rules called **protocols**.

**Key Points:**

- Enables resource sharing and communication
- Can be wired (Ethernet) or wireless (Wi-Fi)
- Uses protocols like TCP/IP for communication

---

### Q2. Types of Networks (LAN, WAN, MAN)

| Type    | Full Form                 | Range                       | Example          |
| ------- | ------------------------- | --------------------------- | ---------------- |
| **LAN** | Local Area Network        | Small area (room, building) | Office network   |
| **MAN** | Metropolitan Area Network | City-wide                   | Cable TV network |
| **WAN** | Wide Area Network         | Country/worldwide           | The Internet     |

Other types include **PAN** (Personal Area Network) and **CAN** (Campus Area Network).

---

### Q3. Hub, Switch, and Router

| Device     | Layer          | Intelligence                   | Function                                    |
| ---------- | -------------- | ------------------------------ | ------------------------------------------- |
| **Hub**    | Physical (L1)  | Dumb — broadcasts to all ports | Connects devices; sends data everywhere     |
| **Switch** | Data Link (L2) | Smart — uses MAC addresses     | Sends data only to the intended device      |
| **Router** | Network (L3)   | Smartest — uses IP addresses   | Connects different networks; routes packets |

---

### Q4. Network Topology and its Types

**Topology** = the physical or logical arrangement of devices in a network.

| Topology   | Shape          | Pros           | Cons                       |
| ---------- | -------------- | -------------- | -------------------------- |
| **Bus**    | Single cable   | Cheap, easy    | Single point of failure    |
| **Star**   | Central hub    | Easy to manage | Hub failure = network down |
| **Ring**   | Circular       | Equal access   | One break = network down   |
| **Mesh**   | Every-to-every | Very reliable  | Expensive, complex         |
| **Tree**   | Hierarchical   | Scalable       | Root failure = problems    |
| **Hybrid** | Combination    | Flexible       | Complex                    |

---

### Q5. Nodes and Links

- **Node**: Any device connected to a network (computer, printer, router, switch).
- **Link**: The communication pathway between two nodes.
  - **Point-to-point link**: Dedicated connection between two nodes.
  - **Multipoint link**: Shared connection among multiple nodes.

---

## 2. OSI Model

### Q6. OSI Model Overview

The **Open Systems Interconnection (OSI)** model is a conceptual framework with **7 layers** that standardizes how data is transmitted over a network. Each layer has a specific role and communicates with the layers directly above and below it.

**Purpose:** Standardization, modularity, and easier troubleshooting.

---

### Q7. Layers of OSI Model

| #   | Layer            | Function                                        | Protocol/Example     | Data Unit |
| --- | ---------------- | ----------------------------------------------- | -------------------- | --------- |
| 7   | **Application**  | User interface & services                       | HTTP, FTP, SMTP, DNS | Data      |
| 6   | **Presentation** | Data translation, encryption, compression       | SSL/TLS, JPEG, ASCII | Data      |
| 5   | **Session**      | Establishes, manages, terminates sessions       | NetBIOS, RPC         | Data      |
| 4   | **Transport**    | End-to-end delivery, error/flow control         | TCP, UDP             | Segment   |
| 3   | **Network**      | Routing & logical addressing (IP)               | IP, ICMP, OSPF       | Packet    |
| 2   | **Data Link**    | Frame delivery, MAC addressing, error detection | Ethernet, PPP        | Frame     |
| 1   | **Physical**     | Bit transmission over physical media            | Cables, Hubs, Wi-Fi  | Bits      |

> **Mnemonic (top→down):** **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

---

## 3. TCP/IP Model

### Q8. TCP/IP Protocol Suite

The **TCP/IP model** is the practical model used by the internet. It was developed by the US Department of Defense (DoD). Unlike the theoretical OSI model, TCP/IP is implementation-oriented.

**Key Protocols:**

- **TCP** (Transmission Control Protocol): Reliable, connection-oriented
- **IP** (Internet Protocol): Handles addressing and routing
- **UDP**: Unreliable, connectionless, faster
- **HTTP, FTP, SMTP, DNS**: Application-level protocols

---

### Q9. Different Layers of the TCP/IP Model

| #   | Layer              | OSI Equivalent                       | Function                                |
| --- | ------------------ | ------------------------------------ | --------------------------------------- |
| 4   | **Application**    | Application + Presentation + Session | User-facing protocols (HTTP, FTP, DNS)  |
| 3   | **Transport**      | Transport                            | End-to-end communication (TCP, UDP)     |
| 2   | **Internet**       | Network                              | Logical addressing & routing (IP, ICMP) |
| 1   | **Network Access** | Data Link + Physical                 | Physical transmission (Ethernet, Wi-Fi) |

---

### Q10. Difference between OSI and TCP/IP Model

| Feature              | OSI Model                     | TCP/IP Model                  |
| -------------------- | ----------------------------- | ----------------------------- |
| Layers               | 7                             | 4                             |
| Nature               | Theoretical/reference         | Practical/implementation      |
| Developed by         | ISO                           | DoD (ARPANET)                 |
| Approach             | Generic, protocol-independent | Protocol-dependent            |
| Session/Presentation | Separate layers               | Merged into Application       |
| Reliability          | Defines but not implemented   | Implemented in real protocols |

---

## 4. Physical Layer

### Q11. Data Transmission

The process of sending data as electrical signals, light pulses, or radio waves over a medium.

**Types:**

- **Simplex**: One-way only (e.g., TV broadcast)
- **Half-Duplex**: Two-way, but one at a time (e.g., Walkie-talkie)
- **Full-Duplex**: Two-way, simultaneously (e.g., Telephone)

**Transmission modes:** Serial (one bit at a time) vs. Parallel (multiple bits simultaneously).

---

### Q12. Bandwidth

**Bandwidth** is the maximum rate of data transfer across a network path, measured in **bits per second (bps)**.

- **Bandwidth** = maximum capacity (like the width of a highway)
- **Throughput** = actual data transferred (like the traffic on the highway)
- **Latency** = time delay

> Higher bandwidth ≠ always faster. Latency and congestion also matter.

---

### Q13. Transmission Media and Wireless Transmission

**Guided (Wired) Media:**
| Type | Speed | Use Case |
|------|-------|----------|
| **Twisted Pair** | Up to 10 Gbps | LAN, telephone |
| **Coaxial Cable** | Up to 10 Gbps | Cable TV |
| **Fiber Optic** | Up to 100+ Gbps | Long-distance, backbone |

**Unguided (Wireless) Media:**
| Type | Range | Use Case |
|------|-------|----------|
| **Radio Waves** | Long | AM/FM, Wi-Fi |
| **Microwaves** | Line of sight | Satellite, telecom towers |
| **Infrared** | Very short | TV remote, short-range |

---

## 5. Data Link Layer

### Q14. What is Data Link Layer and its Functions?

The **Data Link Layer (Layer 2)** ensures reliable transfer of data frames between two directly connected nodes.

**Functions:**

1. **Framing**: Breaks data into frames
2. **Physical Addressing**: Adds MAC addresses (source & destination)
3. **Error Detection/Correction**: Uses CRC, checksums
4. **Flow Control**: Prevents overwhelming the receiver
5. **Access Control**: Determines which device has access to the link

**Sub-layers:** LLC (Logical Link Control) and MAC (Media Access Control)

---

### Q15. Error Detection and Correction

**Error Detection Methods:**

- **Parity Check**: Single parity bit (detects single-bit errors)
- **Checksum**: Sum of data segments
- **CRC (Cyclic Redundancy Check)**: Polynomial division — most commonly used

**Error Correction Methods:**

- **Hamming Code**: Detects and corrects single-bit errors
- **ARQ (Automatic Repeat reQuest)**: Retransmits erroneous frames
  - Stop-and-Wait ARQ
  - Go-Back-N ARQ
  - Selective Repeat ARQ

---

### Q16. Data Link Protocols

- **HDLC** (High-level Data Link Control): Bit-oriented protocol
- **PPP** (Point-to-Point Protocol): Used for direct connection between two nodes (e.g., dial-up)
- **SLIP** (Serial Line Internet Protocol): Older, simple framing

---

### Q17. Multiple Access Protocols

When multiple devices share a single link, protocols manage who transmits when:

| Category              | Protocol                | How it Works                                  |
| --------------------- | ----------------------- | --------------------------------------------- |
| **Random Access**     | ALOHA, CSMA/CD, CSMA/CA | Devices transmit anytime, handle collisions   |
| **Controlled Access** | Polling, Token Passing  | Central control or token determines who sends |
| **Channelization**    | FDMA, TDMA, CDMA        | Divide channel by frequency/time/code         |

- **CSMA/CD**: Used in Ethernet — detect collision, stop, wait, retry
- **CSMA/CA**: Used in Wi-Fi — avoid collision before transmitting

---

### Q18. MAC Address

- **MAC (Media Access Control)** address is a unique **48-bit** (6-byte) hardware address assigned to every NIC.
- Format: `AA:BB:CC:DD:EE:FF` (hexadecimal)
- Also called **physical address** or **burned-in address**
- **Cannot be changed** (hardcoded into the NIC by the manufacturer)
- Used at Layer 2 for local network communication

> **MAC vs IP:** MAC = who you _are_ (permanent). IP = where you _live_ (can change).

---

### Q19. Channel Allocation Problem

The problem of fairly dividing a shared communication channel among multiple users.

**Approaches:**

- **Static Allocation**: Fixed division (FDMA, TDMA) — wastes bandwidth if some users are idle
- **Dynamic Allocation**: On-demand — more efficient (ALOHA, CSMA)

---

### Q20. Data Link Layer Switching

**Switches** operate at Layer 2 and use MAC addresses to forward frames.

- **Learning**: Switch learns MAC addresses from incoming frames
- **Flooding**: If destination unknown, send to all ports
- **Forwarding**: If destination known, send to correct port
- **Filtering**: Don't forward if source and destination are on the same port

---

### Q21. Ethernet LANs

**Ethernet** is the most widely used LAN technology (IEEE 802.3).

- Speed variants: 10 Mbps, 100 Mbps (Fast Ethernet), 1 Gbps (Gigabit), 10 Gbps
- Uses **CSMA/CD** for collision handling
- Frame format: Preamble | Dest MAC | Src MAC | Type | Data | CRC

---

## 6. Network Layer

### Q22. Congestion Control Algorithms

**Congestion** = too many packets in the network, causing delays and packet loss.

**Approaches:**

- **Open-loop**: Prevention (traffic shaping, admission control)
- **Closed-loop**: Detection and correction

**TCP Congestion Control:**

1. **Slow Start**: Start small, grow exponentially
2. **Congestion Avoidance**: Grow linearly after threshold
3. **Fast Retransmit**: Retransmit on 3 duplicate ACKs
4. **Fast Recovery**: Don't go back to slow start

---

### Q23. IP Addressing and Subnetting

**IP Address**: A logical address assigned to every device on a network.

**IPv4 Classes:**
| Class | Range | Default Mask | Use |
|-------|-------|-------------|-----|
| A | 1.0.0.0–126.x.x.x | 255.0.0.0 (/8) | Large networks |
| B | 128.0.0.0–191.x.x.x | 255.255.0.0 (/16) | Medium networks |
| C | 192.0.0.0–223.x.x.x | 255.255.255.0 (/24) | Small networks |

**Subnetting**: Dividing a large network into smaller, manageable sub-networks using a **subnet mask** to borrow bits from the host portion.

---

### Q24. IPv4 and IPv6 Protocols

| Feature         | IPv4                         | IPv6                      |
| --------------- | ---------------------------- | ------------------------- |
| Address Size    | 32-bit                       | 128-bit                   |
| Format          | Dotted decimal (192.168.1.1) | Hexadecimal (2001:db8::1) |
| Total Addresses | ~4.3 billion                 | 3.4 × 10³⁸                |
| Header          | Variable length              | Fixed 40-byte header      |
| Security        | Optional (IPSec)             | Built-in IPSec            |
| NAT             | Required                     | Not needed                |

---

### Q25. ICMP (Internet Control Message Protocol)

ICMP is a **network-layer protocol** used for error reporting and diagnostic functions.

- **Ping**: Uses ICMP Echo Request/Reply to test connectivity
- **Traceroute**: Uses ICMP to trace the path packets take
- Error messages: Destination Unreachable, Time Exceeded, Redirect
- ICMP does **not** carry application data

---

### Q26. Tunneling

**Tunneling** = encapsulating one network protocol inside another.

- Used to carry IPv6 packets over an IPv4 network (and vice versa)
- Examples: **VPN tunnels**, **GRE tunneling**, **IPSec tunneling**
- The original packet is wrapped in a new header for transit

---

### Q27. Subnet

A **subnet** (subnetwork) is a logical subdivision of an IP network.

**Benefits:**

- Reduces network congestion
- Improves security (isolates segments)
- Efficient use of IP addresses

**Example:** Network `192.168.1.0/24` can be subnetted into:

- `192.168.1.0/26` (64 hosts)
- `192.168.1.64/26` (64 hosts)
- `192.168.1.128/26` (64 hosts)
- `192.168.1.192/26` (64 hosts)

---

### Q28. Gateway and Router

| Feature      | Gateway                                        | Router                                       |
| ------------ | ---------------------------------------------- | -------------------------------------------- |
| **Function** | Connects networks with **different protocols** | Connects networks with the **same protocol** |
| **Layer**    | Up to Layer 7                                  | Layer 3                                      |
| **Example**  | Connecting a LAN to the Internet               | Forwarding IP packets between subnets        |

> A **default gateway** is the router that your device sends packets to when the destination is outside the local network.

---

### Q29. Count to Infinity Problem

A problem in **distance-vector routing** protocols (like RIP) where routers keep incrementing the hop count for a downed link, creating a routing loop.

**Solutions:**

- **Split Horizon**: Don't send route info back to the source
- **Route Poisoning**: Advertise the failed route with infinite metric (16 in RIP)
- **Hold-down Timer**: Ignore updates for a route for a fixed period after it goes down

---

## 7. Transport Layer

### Q30. Elements of Transport Protocol

The transport layer provides **end-to-end communication** between processes on different hosts.

**Key Elements:**

- **Addressing**: Uses **port numbers** (0–65535) to identify processes
- **Multiplexing/Demultiplexing**: Multiple apps share the network
- **Connection Establishment**: 3-way handshake (TCP)
- **Flow Control**: Prevents sender from overwhelming receiver
- **Error Control**: Ensures reliable delivery
- **Congestion Control**: Prevents network overload

---

### Q31. TCP (Transmission Control Protocol)

**TCP** is a **connection-oriented, reliable** transport protocol.

**Features:**

- ✅ Reliable delivery (acknowledgements, retransmissions)
- ✅ Ordered delivery (sequence numbers)
- ✅ Flow control (sliding window)
- ✅ Congestion control
- ✅ Error detection (checksum)
- ❌ Slower due to overhead

**Used for:** HTTP, FTP, SMTP, SSH — where data accuracy matters.

---

### Q32. UDP (User Datagram Protocol)

**UDP** is a **connectionless, unreliable** transport protocol.

**Features:**

- ✅ Fast — minimal overhead
- ✅ No connection setup
- ❌ No reliability guarantee
- ❌ No ordering
- ❌ No flow/congestion control

**Used for:** DNS, video streaming, online gaming, VoIP — where speed matters more than accuracy.

---

### Q33. State Transition Diagram

Describes the **lifecycle of a TCP connection** through various states:

```
CLOSED → SYN_SENT → ESTABLISHED → FIN_WAIT_1 → FIN_WAIT_2 → TIME_WAIT → CLOSED
CLOSED → LISTEN → SYN_RCVD → ESTABLISHED → CLOSE_WAIT → LAST_ACK → CLOSED
```

Key states: `LISTEN`, `ESTABLISHED`, `TIME_WAIT`, `CLOSE_WAIT`

---

### Q34. 3-Way Handshake

TCP uses a **3-way handshake** to establish a reliable connection:

```
Client → Server:   SYN        (seq=x)           "Can we connect?"
Server → Client:   SYN-ACK    (seq=y, ack=x+1)   "Yes, let's connect!"
Client → Server:   ACK        (ack=y+1)           "Connection established!"
```

**Why 3 steps?** Both sides must agree on initial sequence numbers to ensure synchronized, reliable communication.

---

### Q35. Congestion Control Mechanisms

| Mechanism                | Description                                                     |
| ------------------------ | --------------------------------------------------------------- |
| **Slow Start**           | Start with cwnd=1, double each RTT until threshold              |
| **Congestion Avoidance** | Increase cwnd by 1 per RTT (linear growth)                      |
| **Fast Retransmit**      | Retransmit on 3 duplicate ACKs without waiting for timeout      |
| **Fast Recovery**        | After fast retransmit, don't go back to slow start              |
| **AIMD**                 | Additive Increase, Multiplicative Decrease — core TCP principle |

---

## 8. Session Layer

### Q36. Session Layer — Basic Introduction

The **Session Layer (Layer 5)** manages **sessions** (dialogues) between two communicating devices.

**Functions:**

- **Session Establishment**: Opens a communication session
- **Session Maintenance**: Keeps the session alive; adds checkpoints for recovery
- **Session Termination**: Gracefully closes the session
- **Synchronization**: Adds sync points so if a failure occurs, only data after the last checkpoint needs to be retransmitted

**Protocols:** NetBIOS, RPC, PPTP

---

## 9. Presentation Layer

### Q37. Presentation Layer — Basic Introduction

The **Presentation Layer (Layer 6)** handles data **translation, encryption, and compression**.

**Functions:**

- **Translation**: Converts data formats (e.g., EBCDIC ↔ ASCII)
- **Encryption/Decryption**: Secures data (e.g., SSL/TLS)
- **Compression**: Reduces data size for efficient transmission

> Think of it as the "translator" layer — ensures sender and receiver understand the same data format.

---

## 10. Application Layer

### Q38. DNS (Domain Name System)

**DNS** translates human-readable domain names (e.g., `google.com`) to IP addresses (e.g., `142.250.190.14`).

**How it works:**

1. Browser checks local cache → Host file → DNS resolver
2. Resolver queries: Root Server → TLD Server (.com) → Authoritative Server
3. Returns IP address

**Record Types:** A (IPv4), AAAA (IPv6), CNAME (alias), MX (mail), NS (nameserver)

---

### Q39. WWW (World Wide Web)

The **World Wide Web** is a system of interlinked hypertext documents accessed via the internet using web browsers.

- **Inventor:** Tim Berners-Lee (1989)
- **Components:** URL (address), HTTP (protocol), HTML (content)
- **Not the same as the Internet** — the WWW is a service _on_ the internet

---

### Q40. HTTP (Hypertext Transfer Protocol)

**HTTP** is an application-layer protocol for transmitting hypermedia (web pages).

- **Stateless**: Each request is independent
- **Methods**: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
- **Status Codes**: 200 (OK), 301 (Redirect), 404 (Not Found), 500 (Server Error)
- **HTTPS** = HTTP + TLS/SSL encryption (port 443 vs port 80)

---

### Q41. FTP (File Transfer Protocol)

**FTP** is used to transfer files between a client and server.

- Uses **two connections**: Control (port 21) + Data (port 20)
- Modes: **Active** (server connects back) vs. **Passive** (client initiates both)
- Supports authentication (username/password) or anonymous access
- **SFTP** (SSH FTP) is the secure alternative

---

### Q42. SMTP (Simple Mail Transfer Protocol)

**SMTP** is the protocol for **sending** emails.

- Uses **port 25** (or 587 for secure)
- Push-based protocol (pushes mail to server)
- Works with **POP3/IMAP** for retrieving emails:
  - **POP3**: Downloads and deletes from server
  - **IMAP**: Syncs across devices, keeps on server

---

### Q43. DHCP (Dynamic Host Configuration Protocol)

**DHCP** automatically assigns IP addresses and network configuration to devices.

**DORA Process:**

1. **D**iscover: Client broadcasts "I need an IP"
2. **O**ffer: DHCP server offers an IP
3. **R**equest: Client requests the offered IP
4. **A**cknowledgment: Server confirms the assignment

**Assigns:** IP address, subnet mask, default gateway, DNS server

---

## 11. Network Security

### Q44. What is Network Security?

**Network security** is the practice of protecting a network and its data from unauthorized access, misuse, or theft.

**Core Principles (CIA Triad):**

- **Confidentiality**: Only authorized users access data
- **Integrity**: Data is not tampered with
- **Availability**: Services are available when needed

---

### Q45. Cryptography

The science of **securing communication** by converting plaintext to ciphertext.

- **Symmetric Encryption**: Same key for encrypt & decrypt (AES, DES) — faster
- **Asymmetric Encryption**: Public key + Private key (RSA) — slower, more secure
- **Hashing**: One-way function (SHA-256, MD5) — verify integrity, not reversible

---

### Q46. Types of Encryption (RSA, DES, AES, Diffie-Hellman)

| Algorithm          | Type         | Key Size        | Use Case                                |
| ------------------ | ------------ | --------------- | --------------------------------------- |
| **DES**            | Symmetric    | 56-bit          | Legacy (broken)                         |
| **AES**            | Symmetric    | 128/192/256-bit | Modern standard                         |
| **RSA**            | Asymmetric   | 1024–4096-bit   | Digital signatures, key exchange        |
| **Diffie-Hellman** | Key Exchange | Variable        | Securely share keys over public channel |

---

### Q47. Hash Functions

A **hash function** takes input of any size and produces a **fixed-size output** (hash/digest).

**Properties:**

- **Deterministic**: Same input → same output
- **One-way**: Cannot reverse the hash to get input
- **Collision-resistant**: Hard to find two inputs with the same hash
- **Avalanche effect**: Small input change → drastically different output

**Examples:** MD5 (128-bit, broken), SHA-256 (256-bit, secure), bcrypt (passwords)

---

### Q48. Digital Signatures

A **digital signature** verifies the **authenticity and integrity** of a message.

**How it works:**

1. Sender hashes the message
2. Sender encrypts the hash with their **private key** → digital signature
3. Receiver decrypts with sender's **public key** → verifies the hash
4. If hashes match → message is authentic and unaltered

---

### Q49. Network Security Protocols

| Protocol      | Purpose                              |
| ------------- | ------------------------------------ |
| **SSL/TLS**   | Encrypts web traffic (HTTPS)         |
| **IPSec**     | Secures IP packets (used in VPNs)    |
| **SSH**       | Secure remote login                  |
| **Kerberos**  | Network authentication using tickets |
| **PGP**       | Email encryption                     |
| **WPA2/WPA3** | Wi-Fi security                       |

---

### Q50. Virtual Private Networks (VPN)

A **VPN** creates a **secure, encrypted tunnel** over a public network (internet).

**Types:**

- **Remote Access VPN**: Individual connects to a private network
- **Site-to-Site VPN**: Connects two entire networks

**Protocols:** IPSec, OpenVPN, WireGuard, L2TP

**Benefits:** Privacy, security, bypass geo-restrictions, anonymous browsing

---

### Q51. Network Attacks

| Attack                | Description                                 |
| --------------------- | ------------------------------------------- |
| **DDoS**              | Overwhelm a server with traffic             |
| **Man-in-the-Middle** | Intercept communication between two parties |
| **Phishing**          | Trick users into revealing sensitive info   |
| **DNS Spoofing**      | Redirect users to malicious websites        |
| **ARP Spoofing**      | Link attacker's MAC to a legitimate IP      |
| **SQL Injection**     | Inject malicious SQL queries                |
| **Packet Sniffing**   | Capture and analyze network traffic         |
| **IP Spoofing**       | Fake the source IP address                  |

---

## 12. Network Troubleshooting

### Q52. Ping Command

**Ping** uses ICMP Echo Request/Reply to test connectivity between two devices.

```bash
ping google.com
```

**Output shows:**

- **TTL** (Time to Live): Max hops before packet is discarded
- **RTT** (Round-Trip Time): Time for packet to go and return
- **Packet loss**: % of packets that didn't return

**Uses:** Check if a host is reachable, measure latency, diagnose connectivity issues.

---

### Q53. Delays and Their Types

| Delay Type             | Description                                                            |
| ---------------------- | ---------------------------------------------------------------------- |
| **Transmission Delay** | Time to push all bits onto the link = Packet size / Bandwidth          |
| **Propagation Delay**  | Time for a bit to travel from source to destination = Distance / Speed |
| **Processing Delay**   | Time for router to process packet header                               |
| **Queuing Delay**      | Time packet waits in router's queue                                    |

**Total Delay** = Transmission + Propagation + Processing + Queuing

---

> 📖 **Source:** [TakeUForward — Most Asked Computer Networks Interview Questions](https://takeuforward.org/computer-network/most-asked-computer-networks-interview-questions)
