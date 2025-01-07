![image](https://github.com/user-attachments/assets/5380f4ad-3a4a-48e4-b259-989e017f4ddf)## PFSENSE

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

### Step 3: Power on the VM. Select Accept > Install > Auto (ZFS) > Install > Stripe.
![image](https://github.com/user-attachments/assets/12b943f5-d534-423a-b048-9617aa3384db)

---
#### Step 4: Select Partition Scheme
![image](https://github.com/user-attachments/assets/8e1b9257-966c-4427-a0dd-4118be7c1002)

![image](https://github.com/user-attachments/assets/81aa638c-4de6-4da6-9871-6cca04773e75)


--- 
#### Step 5: Commit and when installation finishes , Reboot.
![image](https://github.com/user-attachments/assets/c35b4e2b-fd4f-4bd4-b67d-cd58059997e2)


![image](https://github.com/user-attachments/assets/73a4d288-7871-4be9-ab18-bf0cac39a9cc)

#### Step 6: Interface Configurations 
After pfsense must have started up and shown the menu screen, press 1 to assign the interfaces.

![image](https://github.com/user-attachments/assets/d6712f34-c78d-4252-b567-16d8e4b6b639)

- Choose 1 > N:

  ![image](https://github.com/user-attachments/assets/733224ab-5bc0-4a95-9c9b-569d95d4e5d1)

- Enter em0, em1, em2, em3 and em4 respectively > Y.

  ![image](https://github.com/user-attachments/assets/0bd9af58-53f5-4392-8a25-7c054188e76f)


### pfSense Network Interfaces and IP Addresses , with dhcp range from 50-100


| **Interface**       | **IP Address**       |
|---------------------|----------------------|
| **WAN**             | 192.168.1.50/24   or leave default dhcp   |
| **Management**      | 10.0.1.50/24         |
| **Corporate WAN**   | 10.0.10.254/24       |
| **Corporate LAN**   | 10.0.20.254/24       |
| **Security**        | 10.0.50.254/24       |


Remember the lab network config is like so :

| Name          | Domain           | VLAN | Subnet       | Gateway     |
| ------------- | ---------------- | ---- | ------------ | ----------- |
| Management    | N/A              | 1    | 10.0.1.0/24  | 10.0.1.1    |
| Corporate WAN | N/A              | 10   | 10.0.10.0/24 | 10.0.10.254 |
| Corporate LAN | yournextciso.lab | 20   | 10.0.20.0/24 | 10.0.20.254 |
| Security      | yournextciso.lab | 50   | 10.0.50.0/24 | 10.0.50.254 |


When at the main menu of the CLI,press 2 and start assigning the IP addresses above to the respective ports i.e em0-em4. For em0 serving as the WAN interface make sure not to configure by dhcp and set the gateway IP to that of your network provider's router:

![image](https://github.com/user-attachments/assets/c7e3c17e-96a8-4877-b1eb-64cc490067d2)



#### That is how it will look at the end and with the WAN ip set we can how access the interface through a web browser  https://10.0.1.50 :

![image](https://github.com/user-attachments/assets/fda25662-e004-4416-9b3d-d36588cd24ee)


### Do same for em2-4: 

![image](https://github.com/user-attachments/assets/ab20948f-5050-4578-8fbd-7922bea4ca9a)


### How it should look :


![image](https://github.com/user-attachments/assets/3110590e-8ff2-4f40-be81-9640421aeee4)


Login to pfsense using the LAN ip set earlier , username -admin password -pfsense :

![image](https://github.com/user-attachments/assets/6f988171-bbee-4642-8562-774b57500da4)



## Configuration 
  #### Interfaces
First, you will need to assign all interfaces to the pfSense. This can be done by going to Interfaces > Interface Assignments . Since we did most of the work on the CLI, we just need to adjust the names and then make some few changes. 

The next step is to enable and configure each interface with the correct description and IP address. Open each interface according to the instructions below:

Enable: Checked
Description: $NETWORK_NAME_VLAN<VLAN_NUMBER>
IPv4 Configuration Type: Static IPv4
IPv6 Configuration Type: None
MAC Address: leave empty
MTU: leave empty
MSS: leave empty
Speed and Duplex: Default
IPv4 Address: The IP address of the interface from the previous table. Mask set to /24
IPv4 Upstream gateway: None (only WAN interface should have configured this field)
Block private networks: unchecked (this field should be checked for WAN interface only)
Block bogon networks: unchecked (this field should be checked for WAN interface only)


Your configuration should look something like the picture below:


![image](https://github.com/user-attachments/assets/68e73a8b-187e-4abb-83cc-32bcb66bfc8f)


![image](https://github.com/user-attachments/assets/596b04aa-59c2-4cb2-a8b1-44ceeb1fe68c)


After each change done on the interfaces click the save button. So the final results looks like this :
![image](https://github.com/user-attachments/assets/1b615140-d8d1-44a4-a39d-1856ad925bfe)

## Basic Configurations
Let’s configure some basic configurations like DNS servers, domain name, timezone, etc.

Go to System > General Setup and configure the following fields:

Hostname: Set whatever you would like to call your firewall. Named mine pfsense_firewall
Domain: yournextciso.lab
DNS Servers:  8.8.8.8 and 8.8.4.4
Timezone: Etc/UTC
Theme: I prefer a dark theme, but for the sake of this guide, I will use the light one
Click on the Save button at the bottom of the screen.

Then go to **System > Advanced > Admin Access:**

Protocol: HTTPS (SSL/TLS)
Secure Shell Server: Enable

**Firewall Rules**
We will now configure firewall rules to allow/restrict specific traffics between the networks. For the beginning, we will allow all traffic, but at some point, we might restrict the access and allow only specific traffic/ports/services to pass.

### **WAN**
This interface should have default rules that come with enabling fields Block private networks and Block bogon networks during initial configuration:

![image](https://github.com/user-attachments/assets/1ff15565-b70f-4a89-ac97-49ebf5e0fb52)


### MANAGEMENT LAN
 We will disable the IPv6 rule and the rest should be like in the picture below:
 ![image](https://github.com/user-attachments/assets/f7f5d2b6-6cb4-4cf4-9ca6-41f91d7b3501)


### CORPORATE WAN
Here we will allow all traffic toward the Corporate LAN network and Corporate WAN network. Everything else will be blocked by default as there is a default rule “deny all” that denies all traffic. That invisible rule is placed at the end of each interface’s firewall rules:
![image](https://github.com/user-attachments/assets/261d0bd2-d152-4dcc-8115-139576ffebf9)

### CORPORATE LAN

This interface should have the same rules as the CORPORATE_WAN interface. This is because we want to simulate its access to the “internet”
![image](https://github.com/user-attachments/assets/feb85f0f-91ea-4dd2-857f-dff1ec0d7ceb)

### SECURITY
The security network should not have access to WAN, Management, and Corporate WAN networks, but should have access to everything else:
![image](https://github.com/user-attachments/assets/274df3bf-7c56-4269-b7f1-10802503e265)


### Outbound
In order to allow security network access to the internet and simulate other networks’ access to the internet through the fake WAN, we need to set up the rules as on the picture below, in Firewall > NAT > Outbound:
![image](https://github.com/user-attachments/assets/6011859a-24c1-4530-aa86-316ec6b6b0d3)


You can read more about the configuration of outbound NAT and related settings in the pfSense documentation [here](https://docs.netgate.com/pfsense/en/latest/nat/outbound.html#outbound-nat).


# Next up is setting up the DFIR VM in this case Remnux. I used a SANS remnux VM for this and I just changed the network adapter .
