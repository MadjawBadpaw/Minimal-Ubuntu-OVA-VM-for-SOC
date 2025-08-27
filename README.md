# Minimal-Ubuntu-OVA-VM-for-SOC
Ubuntu 22.04 Clean VM for Cybersecurity Projects:
Overview:

This Virtual Machine (VM) contains Ubuntu 22.04 LTS pre-configured for cybersecurity learning, testing, and SOC-style projects.
It is a clean environment:

No personal files or history.

All logs and temporary files cleared.

Ready for immediate use in VirtualBox or other OVF-compatible hypervisors.

The VM includes essential tools for network monitoring, intrusion detection, and security automation, along with example configurations.

Contents

Operating System: Ubuntu 22.04 LTS

Tools Installed:

Wireshark – Network protocol analyzer for packet inspection.

Nmap – Port scanning and network discovery.

Remmina – Remote desktop client (RDP, VNC, SSH).

Suricata – High-performance network IDS/IPS for monitoring network traffic.

Zeek (formerly Bro) – Network security monitoring and logging framework.

Shuffle – Security automation/orchestration platform for SOC workflows.

Wazuh Agent – Security monitoring agent for centralized logging.

Python 3 & pip – For scripting and cybersecurity automation.

Other tools – Curl, net-tools, Git, etc., for network testing and scripting.

Network & VM Configuration

Network Adapter: NAT by default; MAC addresses stripped for safe sharing.

Optional: Can add a bridged adapter for local network testing.

IP Assignment:

Static IP recommended for consistent network testing.

Can configure in /etc/netplan/01-netcfg.yaml or via VirtualBox host-only/NAT settings.

Sample Netplan Static IP Setup
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

Importing the OVA

Download the OVA from Google Drive.

Open VirtualBox → File → Import Appliance → Choose OVA.

Review Appliance Settings:

Vendor Name: Yugam Thakur

Product Name: Ubuntu 22.04 Clean VM

Version: 1.0

Description: Clean Ubuntu 22.04 VM for cybersecurity projects.

Select MAC Address Policy: Strip all MAC addresses

Keep Manifest file checked; leave ISO files unchecked.

Finish the import.

Working with Installed Tools
1. Wireshark

Capture live network traffic.

Run with root privileges:

sudo wireshark


Useful for analyzing network attacks or suspicious traffic.

2. Nmap

Scan ports and detect hosts:

nmap -sV 192.168.56.1

3. Remmina

Connect to other machines using RDP, SSH, or VNC.

Pre-configured for network testing.

4. Suricata

Monitors network traffic in real-time.

Generates alerts and logs for suspicious activity.

Configuration: /etc/suricata/suricata.yaml

Start/stop Suricata:

sudo systemctl start suricata
sudo systemctl stop suricata

5. Zeek

Network monitoring and analysis platform.

Logs network activity for security investigation.

Default logs located at /usr/local/zeek/logs/.

Start Zeek on an interface:

sudo zeek -i enp0s3

6. Shuffle

Security orchestration and automation platform.

Integrates with alerts from Wazuh, Suricata, Zeek, etc.

Web interface accessible via browser on the VM (default port configurable in setup).

7. Wazuh Agent

Sends system logs to a Wazuh server for monitoring.

Configuration at /var/ossec/etc/ossec.conf.

Useful for SOC practice and automated alerting.

VM Upgrade & Maintenance

Update packages:

sudo apt update && sudo apt upgrade -y


Upgrade Ubuntu version:

sudo do-release-upgrade


⚠️ Upgrading may affect pre-configured tools or scripts.

Recommendations for Use

Use snapshots before major changes.

Keep the VM isolated from your host when testing network monitoring or SOC tools.

For sharing or team projects, provide a fresh OVA export after any customizations.

References & Resources

Ubuntu 22.04 Official Docs

Wireshark User Guide

Nmap Reference

Suricata Docs

Zeek Docs

Shuffle Documentation

Wazuh Docs
