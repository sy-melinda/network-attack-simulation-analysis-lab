# Network Attack Simulation and Analysis Lab

## Overview

This project documents a controlled university cybersecurity lab examining three network-based attacks: TCP SYN flooding, ARP cache poisoning and ICMP redirect spoofing.

Each attack was reproduced in an isolated virtual environment so that its network behavior and security impact could be observed. The results were then analyzed from a defensive perspective, with appropriate mitigation strategies identified for each technique.

> **Ethical Scope:** All traffic generation and attack simulation were performed in an isolated and authorized university lab environment. The techniques documented in this repository are presented strictly for educational and defensive purposes.

## Lab Objectives

- Observe the behavior of a TCP SYN flood.
- Understand how half-open TCP connections can affect service availability.
- Analyze the relationship between SYN flooding and denial-of-service attacks.
- Observe how a forged ARP reply can poison an ARP cache.
- Examine how ICMP redirect messages can manipulate network routing.
- Identify the security risks associated with each attack.
- Recommend appropriate defensive and mitigation measures.
- Document technical evidence without exposing personal or sensitive information.

## Tools and Environment

- Linux virtual machines
- VMware
- Wireshark
- Netwag/Netwox packet-generation tools
- TCP/IP networking utilities
- ARP utilities
- ICMP utilities

---

## 1. TCP SYN Flood Analysis

### Attack Technique

A normal TCP connection begins with a three-way handshake:

1. The client sends a `SYN` packet.
2. The server responds with `SYN-ACK`.
3. The client completes the connection within an `ACK`.

During a SYN flood, a large number of connection requests are sent without completing the final acknowledgement. The server may retain these incomplete sessions as half-open connections, consuming resources intended for legitimate clients.

### Observing the SYN Flood

The controlled SYN-flood scenario was observed within the isolated lab network.

![TCP SYN flood traffic](assets/screenshots/01-tcp-syn-flood-traffic.png)

**Observation:** The victim received numerous TCP packets with the `SYN` flag, but the corresponding connections were not completed with final acknowledgements.

**Result:** Multiple half-open connections were created, demonstrating how a SYN flood can consume the server's connection-tracking resources and interfere with legitimate service availability.

### Severity and DoS Classification

A SYN flood is a denial-of-service attack because its objective is to reduce or prevent access to a network service. If the attack is distributed across many source systems, it may become a distributed denial-of-service attack.

The severity depends on:

- The number and frequency of SYN packets.
- The server's available memory and connection backlog.
- The duration of the attack.
- The effectiveness of network filtering and rate limiting.
- Whether the traffic originates from one or many sources.
- The importance of the affected service.

### Defensive Recommendations

Potential defences include:

- Enabling TCP SYN cookies.
- Increasing the server's connection backlog where appropriate.
- Reducing the timeout for incomplete connections.
- Applying rate limits to excessive SYN traffic.
- Using stateful firewall and intrusion-prevention controls.
- Monitoring sudden increases in half-open connections.
- Alerting on abnormal SYN-to-ACK ratios.
- Using upstream DDoS protection for internet-facing services.





