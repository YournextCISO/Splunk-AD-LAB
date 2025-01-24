# Home Lab Active Directory Setup: Project Overview

This project series I will go  through the process of building a home lab to learn about Active Directory (AD) and enhance my skills for both blue and red team roles Here are some of the things we will be setting up:

1. **Set Up Active Directory (AD)**: Build and configure  Active Directory environment to understand how domain management works.
2. **Splunk**: Set up Splunk to ingest telemetry from  Windows Server and target Windows machine.
3. **Pfsense**: Acting ous the firewall (future implementation)
4. **Red Team and Blue Team Exercises**: 
   - Use **Kali Linux** for red team (attacking) activities, such as a brute-force attack on AD users.
   - Practice blue team skills by creating alerts,dashboards and reports in Splunk based on telemetry data.

## Project Steps

### Part 1: **Planning**
- Creating a diagram to visualize of the  setup. This will be helpful for us to visualize our very own virtual enterprise.

### Part 2: **Setup & Installation**
- Install and configure the following using **VMware**:
  - Windows Server 2022
  - Windows 10
  - Kali Linux
  - Splunk (on Ubuntu Server)
  - Pfsense (future implementation toassign Vlans too)
- Create snapshots for easy troubleshooting and experimentation.

### Part 3: **Telemetry and Logging**
- Install **Sysmon** for logging and **Splunk** for querying and monitoring telemetry.  
- Create alerts, reports, and dashboards .  

### Part 4: **Active Directory Configuration**
- Configure Active Directory on Windows Server, promote it to a domain controller, and join  target PC to the domain.  
- Create domain users for testing.

### Part 5: **Security Testing**
- Use Kali Linux to launch a brute-force attack on one of the domain users.
- Use **Atomic Red Team** to run tests and analyze the resulting telemetry in Splunk.
---

# TOPOLOGY


![ADlab](https://github.com/user-attachments/assets/4c40f92c-56e6-4cc6-bbcf-d1efcf34fbd9)


## Future Plans

- learning in security operations and creating more advanced security scenarios.
- Hardening our environment and setting up correct detection rules
- Setting up threat intel and SOAR automation
---

## Acknowledgements

I would like to thank the following individuals for their valuable resources used during the creation of this project:

- [Facyber](https://facyber.me/).
- [MYDFIR](https://www.youtube.com/@MyDFIR).
