# SOC-Home-Lab

## Project Overview
This project documents the design and deployment of a dedicated Security Operations Center (SOC) home lab. The primary objective was to build a controlled environment capable of generating, collecting, and analyzing security telemetry. This infrastructure serves as the foundation for future threat hunting, incident response, and attack simulation exercises.

## 🎯 Lab Design Goals
The primary objective of this project is to architect and deploy a fully functional **SOC monitoring environment**, serving as a controlled baseline for offensive and defensive operations.

### 🛠️ Technical Objectives
*   **🌐 Infrastructure Isolation**: Segmented virtual network using **VirtualBox** to ensure 100% isolation from the host.
*   **🔍 High-Fidelity Telemetry**: Advanced monitoring via **Windows 11 Enterprise** + **Sysmon** (SwiftOnSecurity config).
*   **📦 Centralized Log Aggregation**: Data pipeline using **Elastic Agent** shipping to **Security Onion**.
*   **🕵️ Traffic Inspection**: Deep packet inspection and signature-based detection via the Security Onion stack.
*   **⚔️ Adversary Simulation**: Integrated **Kali Linux** node for controlled attack simulations.

## Host Computer & VM Specs

Four total machines if we include the host machine.

Host Machine:
CPU: i9-12900K 16 Cores
Mem:  128 GB
Drive:  4 TB SSD
Hypervisor:  Oracle Virtual Box

<img width="627" height="174" alt="VM Spec Table" src="https://github.com/user-attachments/assets/92cbf5d5-7888-4198-ade0-8b572d2ff84f" />

Security Onion - Acts as the central nervous system for the lab, providing comprehensive visibility through its integrated stack (Elasticsearch, Logstash, Kibana, Suricata, and Zeek).

Windows 11 – A fully patched Windows 11 endpoint configured to simulate a typical enterprise workstation. It generates system telemetry using Sysmon, which is forwarded to the SIEM for security monitoring and analysis.

Kali Linux (Security Testing) - A dedicated platform for future offensive security testing and network auditing.
