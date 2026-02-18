## OPNsense Setup – From Zero to Working VLAN LAB

This is a summary of my first full deployment of OPNsense in my Home Lab, from installation to working VLAN routing with a managed switch and Proxmox trunk.

1. Installation
I downloaded the OPNsense ISO, created a bootable USB, and installed OPNsense on a Ryzen mini-PC. During installation I assigned WAN (to home router) and LAN (to managed switch). After install I logged into the web UI and confirmed basic connectivity.

2. Creating VLAN Networks
To simulate an enterprise SOC network I created VLANs:
VLAN 10 (MGMT), VLAN 20 (Servers), VLAN 30 (Kali/Attack), VLAN 40 (AP/Clients), VLAN 50 (VMs).

In OPNsense I created VLAN interfaces on the LAN parent, assigned them as new interfaces, gave each a static gateway like 192.168.10.1 / 192.168.20.1 etc., and enabled DHCP per VLAN so machines could get IP addresses automatically.

3. Firewall Rules
By default OPNsense blocks traffic, so for each VLAN interface I added a rule:
PASS → Source: VLAN net → Destination: any.
This allowed devices to reach the router and other networks for testing. Without this rule VLAN machines cannot communicate.

4. Managed Switch Configuration
On the TP-Link T1600 switch I created VLAN IDs (10, 20, 30, 40, 50).  
The port connected to OPNsense LAN was configured as a trunk (tagged for all VLANs).  
Ports for PCs or servers were configured as access ports (untagged in their VLAN, PVID set to that VLAN).  
Tagged ports carry multiple VLANs; untagged ports are single-VLAN devices.

5. Proxmox VLAN Trunk
I created a trunk from the Proxmox host so VMs could run in different VLANs. The Proxmox bridge connected to the trunk port and VMs were assigned VLAN tags, allowing them to communicate through OPNsense just like physical machines.


Conclusion
This setup taught me real networking fundamentals: installing a firewall, creating VLAN segmentation, configuring switch trunking, writing firewall rules, fixing DHCP conflicts, and configuring outbound NAT.

## Part 2
OPNsense WAN + VLAN Internet Access

Goal:  
Allow my offline SOC lab to temporarily access the Internet through OPNsense using one Ethernet cable, so I can update all machines and then disconnect to keep the lab isolated.

Topology:  
Lab VLANs (192.168.10/20/30/40/50) → Switch → OPNsense → Home Router (192.168.1.1) → Internet

Problems I hit:  
- WAN connection unstable → caused by DHCP conflict / duplicate IP.  
- VLAN machines had no Internet → VLAN networks were not NATed.  
- Ping sometimes worked, sometimes failed → routing + ARP instability while WAN was misconfigured.  
- Wi-Fi extender caused extra issues → direct cable to router fixed stability.

Fix:  
- Set stable WAN IP (static or DHCP reservation).  
- Enabled Hybrid Outbound NAT in OPNsense.  
- Added NAT rules for each VLAN subnet (192.168.10/20/30/40/50 → WAN interface).  
- Verified gateway reachability before testing clients.

Extra Work Today:  
Configured a VLAN trunk from Proxmox host, so two VMs on Proxmox now run in a separate VLAN and communicate correctly through OPNsense. This confirmed my switch trunk + VLAN tagging setup works end-to-end.

Result:  
All VLAN machines (including Proxmox VMs) can now reach the Internet through OPNsense.  
I can plug one cable → update all systems → unplug → lab returns to fully offline state.

Lessons learned:  
- Always test WAN gateway first.  
- Every VLAN needs NAT.  
- DHCP conflicts cause random disconnects.  
- Firewall logs don’t mean Internet is actually working.  
- Direct router connection is best for troubleshooting.  
- VLAN trunking from Proxmox works correctly when switch + OPNsense tagging are aligned.

<img width="1365" height="1257" alt="Screenshot from 2026-02-15 15-38-27" src="https://github.com/user-attachments/assets/ec795374-2176-4c88-a3ee-c6966011920e" />
<img width="1908" height="1398" alt="Labopn" src="https://github.com/user-attachments/assets/da5916c5-ce6e-40c7-b3f8-e15cd29f4dd7" />
<img width="1780" height="1304" alt="winruls" src="https://github.com/user-attachments/assets/200acea2-2abc-4f30-a7b0-ada33da35421" />
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/83a0be90-91e9-46ff-a7aa-75508efb53d8" />
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/149aacce-0971-4264-bf08-987b641c643b" />

