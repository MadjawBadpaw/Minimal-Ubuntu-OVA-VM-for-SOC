***Minimal Ubuntu 22.04 Clean VM OVA for SOC/Cybersecurity Projects**

**limk** {}

**Overview**

This Virtual Machine (VM) contains Ubuntu 22.04 LTS pre-configured for cybersecurity learning, testing, and SOC-style projects.
Clean environment: No personal files, history, or logs.
Ready for use in VirtualBox or other OVF-compatible hypervisors.
Includes essential tools for network monitoring, intrusion detection, and security automation.

*Contents*

Operating System: Ubuntu 22.04 LTS

**Installed Tools:**

Wireshark – Network protocol analyzer for packet inspection
Nmap – Port scanning and network discovery
Remmina – Remote desktop client (RDP, VNC, SSH)
Suricata – High-performance network IDS/IPS
Zeek (formerly Bro) – Network security monitoring and logging
Shuffle – Security automation/orchestration platform
Wazuh Agent – Security monitoring agent for centralized logging
Python 3 & pip – For scripting and automation
Other tools – Curl, net-tools, Git, etc.

**Network & VM Configuration**
Network Adapter: NAT by default; MAC addresses stripped for safe sharing
Optional: Add a bridged adapter for local network testing
IP Assignment: Static IP recommended for consistent testing

Example Netplan Static IP Setup

network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.56.10/24]
      gateway4: 192.168.56.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]


Apply changes:
sudo netplan apply


**Importing the OVA**

Download the OVA from MegaNZ link. {}
Open VirtualBox → File → Import Appliance → Choose OVA
Review Appliance Settings:
Vendor Name: Yugam Thakur
Product Name: Ubuntu 22.04 Clean VM
Version: 1.0
Description: Clean Ubuntu 22.04 VM for cybersecurity projects
MAC Address Policy: Strip all MAC addresses
Manifest file: Keep checked
Include ISO files: Leave unchecked
Finish the import


***Working with Installed Tools***

**Wireshark**
Capture live network traffic:
sudo wireshark

**Nmap**

Scan ports and detect hosts:
nmap -sV 192.168.56.1

**Remmina**
Connect to other machines via RDP, SSH, or VNC.

**Suricata**

Monitor network traffic and generate alerts:
Config: /etc/suricata/suricata.yaml

*Start/stop:*

sudo systemctl start suricata
sudo systemctl stop suricata

**Zeek**

Network monitoring and logging:
Logs location: /usr/local/zeek/logs/

Start Zeek on interface:
sudo zeek -i enp0s3 (enp0s3 instead of wlan0 etc because its a VM)

**Shuffle**

Security automation platform for SOC workflows:
Web interface accessible via browser on VM
Integrates alerts from Wazuh, Suricata, and Zeek

**Wazuh Agent**
Single agent for centralised monitoring, add Wazuh server IP in config file at <MANAGER-IP> location.
Centralized log monitoring
Config: /var/ossec/etc/ossec.conf
Useful for SOC practice and automated alerting
VM Upgrade & Maintenance

**Wazuh Server**
Use Wazuh Server for log indexing monitoring, you can use them in:
1)AWS EC2 for wazuh server.(Free Tier)
2)Another device with wazuh server configured.
3)Same device with wazuh server(localhost=127.0.0.1) 


Upgrade Ubuntu release:
sudo do-release-upgrade


**⚠️ Upgrading may affect pre-configured tools or scripts.**

**Recommendations:**

Use snapshots before major changes.
Keep the VM isolated from your host when testing network monitoring or SOC tools
For sharing or team projects, provide a fresh OVA export after customizations

References & Resources:

Ubuntu 22.04 Docs
Wireshark User Guide
Nmap Reference
Suricata Docs
Zeek Docs
Shuffle Docs
Wazuh Docs
