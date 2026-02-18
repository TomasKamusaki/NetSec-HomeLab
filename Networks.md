OPNsense WAN + VLAN Internet Access (SOC Home Lab)

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

Next step:  
Snapshot OPNsense config, then continue with Wazuh deployment and ATT&CK detection tuning.

Big progress for my SOC home lab 👍
