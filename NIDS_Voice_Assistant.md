# NIDS Voice Assistant – Project Introduction. I called this Project "SOCRestaurant"

## Overview
This project is an experimental Network Intrusion Detection System (NIDS) voice assistant built inside my home SOC lab.

The goal is to combine network monitoring, detection logic, and simple voice interaction to simulate how a SOC analyst could receive alerts in real time without constantly watching dashboards.

The assistant listens to network events, detects suspicious activity, and announces alerts using voice output.

This project is part of my hands-on training toward SOC Analyst / IT Security roles.

## Lab Environment

The assistant runs inside my isolated SOC home lab:

- OPNsense firewall with VLAN segmentation
- Proxmox host with Windows and Linux VMs
- Kali attacker VM for simulations
- Ubuntu victim machines
- Raspberry Pi packet capture sensor
- Splunk Enterprise for log analysis
- Zeek / tcpdump for network telemetry

All systems are offline from the Internet unless manually connected for updates.

This allows safe attack simulation and detection testing.

## Project Goal

The main goals of this project are:

• Learn how NIDS detection logic works  
• Practice log parsing and alerting pipelines  
• Connect detection events to human-readable notifications  
• Simulate real SOC alert workflows  
• Improve Python scripting skills  

This is not meant to replace real NIDS tools like Zeek or Suricata.  
It is a learning project focused on detection engineering fundamentals.

## How It Works

1. Network traffic is captured using Zeek or tcpdump.
2. Logs are monitored by a Python script.
3. Detection rules identify events like:
   - Port scans
   - Brute force attempts
   - Suspicious connections
4. Alerts are sent to Splunk and spoken by a voice assistant.

Example voice alert:

"Warning. Possible brute-force attack detected from 192.168.1.125 targeting port 22."

## Skills Demonstrated

• Network traffic analysis  
• Basic detection engineering  
• Python scripting  
• Log parsing  
• SOC workflow simulation  
• MITRE ATT&CK mapping (planned next phase)  

## Why This Project Matters

Most SOC learning is theoretical.  
This project forces me to build detection pipelines end-to-end:

Network → Logs → Detection → Alert → Analyst response.

It helped me understand real SOC challenges like false positives, tuning rules, and monitoring multiple VLAN networks.

## Future Improvements

• Add Wazuh integration  
• Map alerts to MITRE ATT&CK  
• Add alert severity scoring  
• Integrate email / Slack notifications  
• Improve voice interaction commands  

This project is part of my ongoing journey from beginner to SOC Analyst.
All experiments are documented in my NetSec-HomeLab repository.

## Let's Rock 
## Day 1

# Phase 1: Stable Detection Pipeline Established

During this phase of the SOCrestaurant project, the primary objective was to establish a stable, end-to-end detection pipeline rather than prematurely optimizing detection logic.

What was achieved
 • Successfully deployed Zeek as a passive network sensor and validated correct traffic visibility by selecting the appropriate listening interface.
 • Built a custom Python-based alerting engine capable of consuming Zeek conn.log telemetry in real time.
 • Integrated local text-to-speech alerts, enabling immediate, human-readable notifications when network activity is observed.
 • Verified the solution in both online (home network) and offline lab environments, confirming that detection depends on traffic flow and sensor placement rather than internet access.
 • Demonstrated reliable detection of network activity, including the appearance of new hosts, confirming correct ingestion and processing of Zeek logs.

Engineering decision

After experimenting with more advanced filtering and baseline logic, the system was intentionally rolled back to a known-good script that reliably alerts on all observed activity.

This decision was made to:
 • preserve a stable and reproducible baseline,
 • avoid introducing multiple changes simultaneously, and
 • ensure that future alert rules are added incrementally and safely, following real SOC change-management practices.

The current version prioritizes correct data ingestion and alert delivery over noise reduction, establishing a solid foundation for controlled rule tuning.

Why this matters

This phase mirrors real-world SOC engineering workflows:
 • Stability is prioritized before optimization.
 • Detection logic is tuned only after telemetry reliability is proven.
 • Rollbacks are treated as a valid and professional decision, not a failure.

By the end of this phase, the project has a working detection and alerting core, which is the most critical prerequisite for any SOC automation or SOAR-style system.

Next steps

The next phase will focus on incremental alert rule development, including:
 • noise suppression (multicast, broadcast, IPv6),
 • baseline-based new device detection,
 • rate-based and behavior-driven alerts.

Each rule will be added, tested, and documented individually to maintain system stability


## Day 2 

## SOC Restaurant – Detection Engine Progress (Session Summary)

Today I significantly advanced my offline SOC lab by transforming it into a functional mini NIDS built on Zeek logs and a custom Python correlation engine.

## What I Built

Fresh-start monitoring mode – Script now ignores old Zeek logs and begins detection only from launch time.
Identifies new IPs in the monitored subnet that are not part of the baseline.
Detects multiple destination ports targeted within a short time window.


Conclusion — Phase 1: Stable – Correlates repeated connection attempts to port 22 and triggers an alert when thresholds are exceeded.
Detection Pipeline – Every alert now includes precise time context.
Inactive devices are removed from tracking after defined inactivity.


### Validation Testing

Detection logic successfully validated using:
Port scan alert triggered within ~10–20 seconds.(- nmap -p 1-100)
Brute force alert triggered within ~1 minute.

### 🎯 Result

The system now performs:
- Stateful tracking
- Threshold-based anomaly detection
- Real-time alerting
- Log parsing from Zeek conn.log
- Practical red team vs blue team simulation inside an isolated lab

Next phase: detection tuning, false-positive reduction, and potential MITRE ATT&CK mapping.

![photo_2026-02-19_00-45-14](https://github.com/user-attachments/assets/bea13edd-ba15-408c-899c-446c0dd51f65)
![photo_2026-02-19_00-45-18](https://github.com/user-attachments/assets/aeff2dcf-8e7a-4fd2-8f5c-3ec31ff1d216)

## Day 3

## SOCrestaurant v1 – Jira Integration Milestone

Today I completed integration between my Python NIDS script and my self-hosted Jira instance in my offline SOC home lab.

## What I Implemented
- Connected detection script → Jira REST API using API token.
- Automatic ticket creation now works for:
  - Unknown device detection
  - Possible port scan
  - Possible brute force attack
- Voice alerts + Jira tickets simulate real SOC workflow.
- Fixed connectivity issue caused by firewall rules (port 8080 was blocked).
- Verified device timeout logic (inactive devices removed after 120 seconds).

## Result
My lab now supports full detection pipeline:
Zeek sensor → Python detection rules → Voice alert → Jira ticket → SOC tracking.

This allows me to practice real SOC tasks:
- Alert triage
- Incident ticket workflow
- Detection tuning
- Network attack simulation with tracking.

## Next Steps
- Add priority levels per rule (High for brute force, Medium for port scan, etc.).
- Build Jira dashboard with auto-refresh.
- Add new detections: ARP spoofing, ICMP anomaly, lateral movement patterns.
- Improve noise filtering per VLAN.

Today’s milestone confirms my SOCrestaurant project can automatically detect attacks and generate incident tickets in a fully offline lab.

<img width="1893" height="1362" alt="Screenshot from 2026-02-24 15-51-36" src="https://github.com/user-attachments/assets/f94fda44-8dcd-4121-bcfb-2cba785a81b9" />
<img width="1881" height="1417" alt="jira2" src="https://github.com/user-attachments/assets/262f6244-288a-4c23-bab2-364a595bd2aa" />
<img width="1850" height="1099" alt="jiraint" src="https://github.com/user-attachments/assets/a9502d24-5896-4674-a3a6-aa3299d39bb4" />
