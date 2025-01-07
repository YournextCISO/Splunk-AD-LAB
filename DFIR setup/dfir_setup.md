
For this Lab I wasn't planning on setting up a DFIR VM but I just had a SANS remnux box around(Yeah mostly malware analysis but we'll just set it up for now). Added it up and change the Network adapter settings too.
One thing we need to configure and take note of will be the hostname and IP address of our VM. To do that ,  change the hostname we need to edit two files: /etc/hostname and /etc/hosts .

edit hostname:

![image](https://github.com/user-attachments/assets/73aa54d3-b5a7-4c3c-b715-576e0e3bf427)

edit etc/hosts:

![image](https://github.com/user-attachments/assets/73e15039-ced5-4fa6-a932-49b91a9a520c)

Set Static IP:
![image](https://github.com/user-attachments/assets/cfe45f7b-77e7-4820-8095-b29927c702e1)

We then reboot the VM so the settings apply.

The final step for network changes is to create a host override record on our firewall. Go to Services >DNS Resolver> General Settings and in the section Host Overrides click on the Add button. Add the following details like on the picture below:

![image](https://github.com/user-attachments/assets/961d7ffb-1b86-4255-b986-e859af40e7af)

We can test connectivity using the ping tool:

![image](https://github.com/user-attachments/assets/07b5c3cd-ed68-4e7c-aeb5-00606ca42985)


