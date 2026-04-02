# Case Study: AI Prompt Injection Detection & Analysis

## Project Overview
This project simulates a real-world Prompt Injection attack against a locally hosted AI chatbot. The goal of this exercise was to demonstrate the full "Detection Lifecycle"—from environment setup and custom IDS rule engineering to forensic correlation using SIEM telemetry.
<img width="1242" height="432" alt="Network Diagram" src="https://github.com/user-attachments/assets/c71bd61c-2362-4e3a-8f7a-f47e97651073" />

## 1.1 Connectivity Verification
The first step was to ensure the integrity of my SOC Home Lab. I verified that the Windows VM and Security Onion were actively communicating. I confirmed the SIEM was running in a healthy state, and Elastic showed all systems as healthy as well. Next, I confirmed Sysmon logs were successfully being indexed and visible when using the Hunt interface.

## 1.2 Target Environment Setup
In order to simulate a modern attack surface, I deployed a lightweight Python-based AI chatbot on the Windows VM.
Purpose: This script was adapted from open-source documentation to serve as the vulnerable endpoint for the prompt injection simulation. This aided in viewing the telemetry of the prompt injection and offered better visibility into the full attack cycle.
Configuration: The basic AI chatbot was set up on port 5000 to mimic a web-integrated LLM interface. In the script, there is a "system prompt" which contains a "secret key" to determine if the hack was successful.

## 1.3 Custom Detection Engineering (Suricata)
I integrated a custom detection signature into the Suricata IDS engine. While the core engine handles the automated collection of network metadata (IP headers, timestamps, and flow data), I developed the specific rule logic required to inspect the http_client_body. This ensured that any HTTP POST request containing "jailbreak" phrases like "ignore" would be flagged and categorized as a high-priority event.
