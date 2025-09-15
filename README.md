# 🔐 SYN-ARP Attacker and ARP Detector Tool

This project demonstrates **SYN Flood** and **ARP Spoofing** attacks, and provides a custom **ARP Spoofing Detection Tool**. Implemented in **Python 3** with `scapy`, the repo is intended for controlled, educational use in a lab environment to understand attack mechanics and detection techniques.

---

## 📌 Project Overview
- **SYN Flood Attack**: Overloads TCP connection tables by abusing the TCP three-way handshake (Denial of Service).
- **ARP Spoofing Attack**: Sends forged ARP messages to associate the attacker’s MAC with a victim IP, enabling Man-in-the-Middle (MitM) interception.
- **ARP Spoofing Detection Tool**: Monitors local ARP cache for anomalies (duplicate MAC entries) and alerts the user in real time.

---

## ⚠️ Safety & Legal Notice
This repository is intended **only for educational and defensive purposes** on networks and systems you own or have explicit permission to test. Launching attacks on networks or devices without authorization is illegal and unethical. Use responsibly.

---

## 🛠️ Features
- CLI tools to run **SYN Flood** and **ARP Spoofing** attacks with configurable options.
- Randomized IP & MAC spoofing for SYN Flood payloads to simulate attack traffic.
- Uses `nmap` and local network parsing to discover hosts and target IPs.
- ARP Detection script that inspects the ARP table and reports possible ARP poisoning in real-time.
- Integration with Wireshark for traffic inspection and verification of attack behavior.

---

## 🖥️ System Requirements
- Linux-based attacker environment (e.g., Ubuntu)
- Victim environment (e.g., Raspberry Pi OS) — recommended to run in VM (VirtualBox)
- Python 3.6+
- `scapy`, `keyboard` (for detection script)
- `nmap` and `wireshark` for scanning and analysis

---

## 📊 Expected Results
- SYN Flood: Victim shows many half-open TCP connections; service may be denied for legitimate clients.
- ARP Spoofing: Attacker can capture victim HTTP requests (if not using HTTPS); victim ARP cache gets poisoned.
- Detection: `arp_detection.py` reports duplicate MAC entries and prints an alert with the suspected MAC address.

---

## 🔧 Implementation Notes
- Attacker script uses `ifconfig` output parsing and `nmap -sP` (ping scan) to enumerate hosts and determine CIDR.
- SYN flood function crafts Ethernet/IP/TCP layers with randomized source IPs and MAC addresses using Scapy's `sendp()` for layer-2 injection.
- ARP spoofing function constructs ARP packets with `psrc` set to router IP and `pdst` set to victim IP to poison ARP caches.
- Detection script parses `arp -a` output and flags repeated MAC addresses across ARP entries.

---

## 🧩 Future Work
- Add automatic mitigation (block IP/MAC, insert static ARP entries).
- Implement rate-limiting thresholds to detect SYN flood and automatically respond.
- Convert detection to a system daemon with logging & alerting (e.g., email/SMS).
- Provide hardened cross-platform deployment and better CLI argument parsing.
