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

---

## 💻 Infrastructure & Virtual Assets

### 🖥️ Host System (Physical)
A high-performance workstation ensures stable virtualization and smooth telemetry processing.

| Component | Specification |
| :--- | :--- |
| CPU | Intel Core i9-12900K (16 Cores / 24 Threads) |
| Memory | 128 GB DDR5 RAM |
| Storage | 4 TB NVMe SSD |
| Hypervisor | Oracle VirtualBox |
<img width="1218" height="315" alt="VM List" src="https://github.com/user-attachments/assets/18e7c533-33e3-4c5d-a9c3-4b1050aac63b" />

### 🛠️ Virtual Machine Roles & Specifications
The lab environment consists of three primary nodes within an isolated virtual network.

<img width="627" height="174" alt="VM Spec Table" src="https://github.com/user-attachments/assets/797d5dc9-cee9-447a-9985-b17e25da90ad" />

> **Security Onion (SIEM/IDS)**
> Acts as the central nervous system for the lab, providing comprehensive visibility through its integrated stack (Elasticsearch, Logstash, Kibana, Suricata, and Zeek).

> **Windows 11 (Endpoint)**
> A fully patched Windows 11 endpoint configured to simulate a typical enterprise workstation. It generates system telemetry using Sysmon, which is forwarded to the SIEM for security monitoring and analysis.

> **Kali Linux (Security Testing)**
> A dedicated platform for future offensive security testing and network auditing.

---

## 🏗️ Architecture & Design
The lab is built using a virtualized architecture to ensure isolation from the primary host network while maintaining high performance for security tools.
<img width="903" height="626" alt="SOC Home Network Diagram" src="https://github.com/user-attachments/assets/0b409c4e-03e5-42c3-ba87-f00b6b6c91de" />

*   **Virtualization Platform**: Oracle VirtualBox
*   **Network Topology**: A segmented virtual network was established to facilitate secure communication between the victim endpoints and the central monitoring stack.

### 🌐 Network Configuration Details
To maintain a secure and functional environment, the following networking rules were implemented:

*   **Infrastructure Isolation**  
    Hosted all VMs inside a dedicated virtual network to maintain isolation.
*   **Subnet Management**  
    Used VirtualBox’s default gateway (10.0.2.2/24) and kept all VMs within the same subnet.
*   **Static IP Addressing**  
    Manually assigned static IP addresses to all nodes to ensure persistent log forwarding and stable communication between agents.    
*   **Internal Communication**  
    Assigned Adapter 1 on each VM to the NAT Network for internal communication.
*   **SIEM Connectivity**  
    Configured the SIEM VM with a second network adapter connected to the internet.
*   **Management Access**  
    The second adapter allows the host machine to access the SIEM management console.
*   **Endpoint Security**  
    The other two VMs are fully isolated from the internet and only communicate within the internal network.

### 🧪 Connectivity Validation
To verify the integrity of the segmented network, I conducted cross-node connectivity tests between the attack node, the victim, and the SIEM.


| Test Direction | Connectivity Proof |
| :--- | :--- |
| **Kali ➔ Windows 11** | <img src="https://github.com/user-attachments/assets/5d69e3bf-dea3-4861-b8fe-51b1851f37c8" width="450"> |
| **Windows 11 ➔ Kali** | <img src="https://github.com/user-attachments/assets/6bc3c3e5-844b-4119-8c33-ece57b0ac501" width="450"> |
| **Windows 11 ➔ SIEM** | <img src="https://github.com/user-attachments/assets/3ad9f0bf-cc30-43f9-a182-44284fe13a65" width="450"> |

---

## 🚀 Telemetry & Data Pipeline
The core of this lab is the automated collection and analysis of security events. This pipeline ensures that activity on the endpoint is captured and forwarded to the central monitoring stack.

<img width="450" height="764" alt="SOC Lab Pipeline" src="https://github.com/user-attachments/assets/1d7a19a0-e897-439b-8cbe-5bc71dbf947a" />

### 🔍 Endpoint Visibility
To achieve deep visibility into system events, I implemented a dual-layered telemetry approach:

*   **Sysmon (System Monitor)**  
    Installed on Windows 11 to provide granular logging of process creations, network connections, and changes to file creation times.
*   **SwiftOnSecurity Configuration**  
    Applied a customized version of the sysmonconfig-expert.xml to reduce noise and focus on high-fidelity security events.

#### ✅ Endpoint Verification

| Test Step | Visual Proof |
| :--- | :--- |
| **Sysmon Installation** | <img src="https://github.com/user-attachments/assets/519b518f-dd1b-49ac-bfb4-bc743d2751fb" width="500"> |
| **Functionality Check** | <img src="https://github.com/user-attachments/assets/7bdadd94-ab9c-475a-80c7-0474662da9a0" width="500"> |
| **Event Log Example**   | <img src="https://github.com/user-attachments/assets/3eaf4dd2-d095-49c9-abce-cf6bed47db94" width="500"> |

---

### 📦 Data Ingestion
The movement of data from the source to the analyst console is handled by the following components:

*   **Elastic Agent**  
    Deployed on the Windows 11 workstation to facilitate the secure transfer of logs and telemetry to the Security Onion management node.
*   **Network Monitoring**  
    Configured the virtual network adapters to ensure the Security Onion instance could capture and inspect traffic across the virtual segment.

#### ✅ Pipeline Verification


| System Status | Visual Proof |
| :--- | :--- |
| **Fleet Management Console** | <img src="https://github.com/user-attachments/assets/713c4a3c-7ecc-4ade-87d7-a9d389686939" width="600"><br><em>Confirmation of healthy status for Windows 11, Security Onion, and Fleet Server nodes.</em> |

---

## 📚 References & Resources
The following resources and documentation were instrumental in the design, deployment, and configuration of this SOC home lab environment.

*   **Security Onion Documentation**  
    [Official Documentation](https://docs.securityonion.net)
*   **Sysmon (Microsoft Sysinternals)**  
    [Tool Documentation and Download](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
*   **Elastic Agent & Fleet**  
    [Installation and Configuration Guide](https://www.elastic.co/guide/en/fleet/current/elastic-agent-installation.html)
*   **Windows 11 Enterprise Evaluation**  
    [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise)
*   **Kali Linux**  
    [Official Virtual Machine Images](https://www.kali.org/get-kali/#kali-virtual-machines)
*   **Oracle VirtualBox**  
    [Hypervisor Download Page](https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html)
*   **SwiftOnSecurity Sysmon Config**  
    [Expert Configuration XML Repository](https://github.com/SwiftOnSecurity/sysmon-config)
