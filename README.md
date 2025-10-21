
# Network Monitor (CS-250 Assignment 2)

**Author:** Hamna Shah  
**Course:** CS-250 – Object-Oriented Programming  
**Topic:** Stacks and Queues in Network Monitoring  
**Language:** C++17  
**Platform:** Linux (requires root privileges)

---

##  Overview
This project implements a **Network Monitoring System** using **custom Stack and Queue** data structures in **C++17**.  
It captures, filters, and replays live network packets through **raw sockets** on a Linux interface.  
The system demonstrates practical use of **Stacks (LIFO)** and **Queues (FIFO)** for managing packet flow and protocol parsing.

---

##  Features
- Raw socket capture using `AF_PACKET`
- Supports Ethernet, IPv4, IPv6, TCP, and UDP layers  
- Custom-built Stack and Queue (no STL containers)  
- Multi-threaded design (capture, filter, replay, backup)
- Source/Destination IP-based filtering  
- Replay retry mechanism (up to 2 attempts)  
- Oversized packet skipping and counting  
- Randomized, formatted packet display logs  
- 60-second timed capture demo  

---

##  Core Data Structures
### Queue (FIFO)
Used for ordered packet flow between stages:  
`Capture → Filter → Replay → Backup`

### Stack (LIFO)
Used for protocol layer dissection:  
`Ethernet → IPv4/IPv6 → TCP/UDP`

Both structures are implemented manually using **linked lists and mutex locks** for concurrency safety.

---

##  Build Instructions
To compile:
```bash
g++ -std=c++17 -pthread network_monitor_final.cpp -o network_monitor_final

To run:
sudo ./network_monitor_final <interface> <src_ip> <dst_ip>

Example:
sudo ./network_monitor_final enp0s1 * *
sudo ./network_monitor_final enp0s1 10.0.0.5 10.0.0.9
