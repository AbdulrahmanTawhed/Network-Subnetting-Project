# Enterprise Campus Network Infrastructure & Subnet Optimization

## 📌 Project Overview
This project delivers the architecture, design, and implementation of a secure, multi-site campus network infrastructure. Utilizing a single **Class C block (`192.168.15.0/24`)**, the network is optimized through **Variable Length Subnet Masking (VLSM)** to minimize address wastage, establish distinct broadcast domains, and isolate critical infrastructure segments. 

The design integrates layered routing strategies (Static, Default, and Host-Specific) alongside centralized application services simulated inside **Cisco Packet Tracer**.

---

## 📊 Variable Length Subnet Masking (VLSM) Plan

To support the campus topology without address exhaustion, the address space was engineered around strict host requirements. LAN segments are allocated `/29` masks (allowing up to 6 usable hosts per subnet), while point-to-point serial WAN links utilize highly efficient `/30` masks.

| Subnet Identifier | Network ID | Subnet Mask | Usable IP Range | Broadcast Address | CIDR Block | Functional Assignment / Description |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **LAN A** | `192.168.15.0` | `255.255.255.248` | `192.168.15.1` - `192.168.15.6` | `192.168.15.7` | `/29` | End-User Client Segment A |
| **LAN B** | `192.168.15.8` | `255.255.255.248` | `192.168.15.9` - `192.168.15.14` | `192.168.15.15` | `/29` | End-User Client Segment B |
| **LAN C** | `192.168.15.16` | `255.255.255.248` | `192.168.15.17` - `192.168.15.22` | `192.168.15.23` | `/29` | End-User Client Segment C |
| **LAN D** | `192.168.15.24` | `255.255.255.248` | `192.168.15.25` - `192.168.15.30` | `192.168.15.31` | `/29` | Central Data Center / Server Segment |
| **WAN Link E** | `192.168.15.32` | `255.255.255.252` | `192.168.15.33` - `192.168.15.34` | `192.168.15.35` | `/30` | Core Point-to-Point Router Interconnect |
| **WAN Link F** | `192.168.15.36` | `255.255.255.252` | `192.168.15.37` - `192.168.15.38` | `192.168.15.39` | `/30` | Core Point-to-Point Router Interconnect |
| **WAN Link G** | `192.168.15.40` | `255.255.255.252` | `192.168.15.41` - `192.168.15.42` | `192.168.15.43` | `/30` | Core Point-to-Point Router Interconnect |
| **WAN Link H** | `192.168.15.44` | `255.255.255.252` | `192.168.15.45` - `192.168.15.46` | `192.168.15.47` | `/30` | Peripheral Gateway Link |

---

## 🛠️ Core Technical Implementation Details

### 1. Network Layer & Multi-Tier Routing Architecture
* **Internal Routing & Core Reachability:** Configured standard static routing maps across internal routers to enable seamless, full mesh cross-LAN communication.
* **Optimized Static Host Routing:** Implemented targeted host-specific routes directly pointing toward the central server asset (`192.168.15.26`) on localized nodes to minimize hop processing time.
* **Default Border Routing:** Deployed zero-subnet default routing rules (`0.0.0.0 0.0.0.0`) on all internal edge gateways pointing toward the border ISP gateway (`WE Router`) to cleanly offload out-of-network internet traffic.

### 2. Centralized Application Layer Services
* **Dynamic IP Allocation (DHCP):** Integrated localized DHCP server scopes directly on interface gateways to dynamically distribute leases, including IP blocks, subnet masks, default gateways, and local DNS pointers.
* **Domain Name System (DNS):** Provisioned an enterprise DNS server on host `192.168.15.26` handling forward lookup tables for localized corporate web domains.
* **Application Servers:**
  * **HTTP:** Deployed corporate web portals rendering responsive localized web services.
  * **FTP:** Configured isolated file repositories running user-level access-control credentials for secure document handling.
  * **SMTP / POP3:** Validated an active mail server domain to demonstrate internal peer-to-peer corporate email relay mechanisms.

---

## 📈 Verification, Diagnostics & Results
* **Full End-to-End Reachability:** Conducted complete cross-topology ICMP (Ping) verification audits. Every end-device successfully routes to all internal subnets.
* **Edge / ISP Bound Verification:** Validated edge transit traffic by establishing successful default-route gateway hops from deep internal endpoints directly out to the external ISP simulation.
* **Service Accessibility:** Confirmed stable FTP authentications, seamless internal text mail transmission, and accurate DNS lookup resolution across every individual broadcast domain.

---

## 📂 Repository Contents
* `Project.pkt`: Interactive network simulation schema, topology layout, and interface maps built for Cisco Packet Tracer.
* `Campus_Network_Design_and_Implementation.pdf`: Comprehensive enterprise architectural design blueprints, subnet breakdown parameters, and network verification logs.
