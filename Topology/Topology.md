## Network Diagram and Lab Setup

The first thing I did was create a network diagram for my lab. This diagram includes all the VMs I plan to use, along with important details like IP addresses, VLANs, subnets, and so on
---

## Lab Use-Cases and Devices

I want my lab to serve a variety of purposes to boost my skills across different areas. Here's a list of what I plan to work on:

- **SIEM (Splunk)**: To learn about security event management and logging.
- **Malware Analysis(future)**: To understand how malware behaves in a controlled environment.
- **Digital Forensics and Incident Response (DFIR)**: For analyzing security incidents and handling forensic investigations.
- **OSINT (Open-Source Intelligence)**: To practice collecting intelligence from publicly available sources.
- **Vulnerability Scanning**: To understand how to find and assess vulnerabilities in systems.
- **Email Forensics**: To learn how to analyze email traffic and detect malicious activity.

---

## List of Devices/VMs for My Lab

Based on these use-cases, I’ve created a list of devices and VMs I will need:

1. **Firewall (pfSense)**: To manage network security and control traffic between VMs.
2. **Windows 10 Host**: For general-purpose use, as well as testing and running different tools.
3. **Windows Server with Active Directory (AD)**: To set up a domain controller and understand AD management.
4. **Kali Linux**: For penetration testing and red team activities.
5. **SIEM (Splunk)**: To ingest logs and monitor network activity, gaining hands-on experience with security event management.
6. **Vulnerability Scanner(will probably install this on the kali vm)**: To perform vulnerability assessments and learn how to identify security weaknesses.



## NETWORK

## Networking Setup for My Home Lab

Now that I’ve decided on the types of hosts and services I want to deploy, it’s time to focus on the networking aspect of the lab. Since this lab will include various VMs for different purposes, such as DFIR, servers, and Kali Linux for simulating outside attacks, I planned out the network structure carefully. For the start, I decided to implement 5 VLANs, each serving a specific purpose:

---

### VLANs Overview

1. **VLAN 1: Management VLAN**
   - This VLAN will be dedicated to management tasks, allowing access to the firewall's web GUI and it will be isolated from other networks to ensure secure management of the environment.

2. **VLAN 10: Corporate WAN (Fake WAN)**
   - This VLAN will simulate an external network (Fake WAN). It will include **Kali Linux**, which will act as a malicious device simulating attacks from the outside.  
   - **Kali Linux** will have access only to **VLAN 20** (the Corporate LAN). It will not be able to reach the real Internet or my personal machines to avoid accidentally spreading malicious scripts or software.

3. **VLAN 20: Corporate LAN**
   - This is where the **Windows Server**, **Windows 10**, and other devices will reside. This VLAN will act as the main corporate network.
   - Devices in this VLAN will have access to the fake internet network (VLAN 10) but will not reach other VLANs directly.

4. **VLAN 50: Security VLAN**
   - This VLAN will contain VMs used as our SIEM and other security-related tasks.
   - The Security VLAN will have network permission to access the **Corporate LAN (VLAN 20)** for gathering logs, files, and emails. However, devices in VLAN 50 will not be able to initiate connections to VLAN 20.
   - This VLAN will also have access to the real Internet to download public tools and perform tool installations and upgrades.

---

### Corporate Domain

  Using the domain **yournextciso.lab**. This domain will be used in the **Active Directory (AD)** setup for managing users, devices, and security policies across the network.

## VLAN SETTINGS
  - Doing this we will also configure static IPs for the hosts in the network

| Name          | Domain           | VLAN | Subnet       | Gateway     |
| ------------- | ---------------- | ---- | ------------ | ----------- |
| Management    | N/A              | 1    | 10.0.1.0/24  | 10.0.1.1    |
| Corporate WAN | N/A              | 10   | 10.0.10.0/24 | 10.0.10.254 |
| Corporate LAN | yournextciso.lab | 20   | 10.0.20.0/24 | 10.0.20.254 |
| Security      | yournextciso.lab | 50   | 10.0.50.0/24 | 10.0.50.254 |


## VMWARE SETTINGS

In VMware, navigate to **Edit > Virtual Network Editor** . From there, click on the **Add Network...** button and create four networks. Name them **vmnet10**, **vmnet20**, **vmnet50**. Set all of them to **host-only**.

For each network, be sure to disable the **Use local DHCP service** option, as we'll be using the firewall as our DHCP server. After that, configure the subnet IPs based on the ones we assigned earlier (or pick your own if you'd like).

![image](https://github.com/user-attachments/assets/8fd15f70-cdea-4cb4-bb79-e04f05ea7647)

   Next is the Pfsense Installation.


