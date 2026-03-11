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
