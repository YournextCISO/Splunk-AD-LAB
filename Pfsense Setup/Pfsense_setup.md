## PFSENSE

Pfsense is a great Opensource tool which can both act as a firewall and a router in our enterprise environment. You can download pfSense from the official website [here](https://www.pfsense.org/download/).

### Virtual Machine Specifications

For my lab setup, I configured the virtual machine with the following specifications:

- **CPU**: 1 vCPU
- **RAM**: 512MB
- **HDD**: 20GB
- **NICs**: 6 virtual NICs, configured as follows:
  - **Bridged**
  - **vmnet1**
  - **vmnet10**
  - **vmnet20**
  - **vmnet50**

The brideged interface there will serve to route outbound traffic towards the internet.

## Installation

#### Step 1 : Select installation file
![image](https://github.com/user-attachments/assets/8df55577-08a2-4c14-9e53-245e605d08f0)

--- 
#### Step 2: Configure network to add VLANS
![image](https://github.com/user-attachments/assets/89de045a-eb7b-4858-8134-910f79dd050c)


