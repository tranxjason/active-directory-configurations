<p align="center">
  <img src="https://github.com/user-attachments/assets/adebd874-547d-4066-9f2a-2502e63f2f57"/>
</p>

<h1>Active Directory Configurations</h1>
In this lab I will now be configuring Active Directory and allowing a client to join the domain as well as creating user accounts.
<br />

<h2>Environment and Technologies Used</h2>

- <b>Microsoft Azure (Virtual Machines/Compute)</b> 
- <b>Remote Desktop</b>
- <b>Active Directory Domain Services</b>
- <b>PowerShell</b>

<h2>Operating Systems Used</h2>

- <b>Windows Server 2022</b>
- <b>Windows 10 Pro</b> 

<h2>Deployment and Configuration</h2>

In this lab I create two VMs in the same VNET. One will be a Domain Controller, the other will be a Client machine. I change the DC to a static IP because its offering Active Directory services to the client machine. Client machine will be joined to the domain. This will control the DNS settings on the client machine, the client machine will use the DC as its DNS server.

![configuration](https://github.com/user-attachments/assets/7e432df2-d8f4-4334-afbf-95750552d756)

DC-1 has to have a static Private IP Address. Client one will connect to DC-1 to ensure connectivity I will try to ping DC-1 from Client-1. At first the ping will not work correctly. I have to enable ICMPv4 on the firewall on DC-1. Now I can ping DC-1 successfully from Client-1

![windows defender](https://github.com/user-attachments/assets/01936776-13a3-4268-99f4-44fbd504843d)
![admin command prompt](https://github.com/user-attachments/assets/1a80449a-ecd6-43e7-827d-20c64317893a)

Now I will log back into DC-1 to install AD Users & Computers. Promote the VM to DC, setup a new forest as "mydomain.com" afterwards restart then log back into DC-1 as user: "mydomain.com\labuser". Now I should be able to run AD Users & Computers as shown below.

![mydomain](https://github.com/user-attachments/assets/8aa88b2e-7646-4fe2-9a24-fa1c2c50e70e)

I start creating Organizational Units (OU). First an OU named _EMPLOYEES. Another OU named _ADMINS. Then created a user named Jane Doe, she is going to be an Admin so her username will be Jane_admin. Lastly added Jane to the domain admins security group.

![janedoe1](https://github.com/user-attachments/assets/1098f866-a051-4df8-8000-3596f69f3ac1)
![janedoe2](https://github.com/user-attachments/assets/6a1ccd76-a871-4a48-8606-2e148dadb164)

Now I can use Jane_admin as the administrator account. Now I will join Client-1 to the domain (mydomain.com) from the azure portal I will change client-1's DNS settings to the DC's Private IP address. After that, restart Client-1 from within the Azure portal. Picture below shows verification that client-1 is on the DC-1 DNS.

![dns servers](https://github.com/user-attachments/assets/545ce952-b0e0-429c-8751-46016ec1555e)
![command dns line](https://github.com/user-attachments/assets/780e98e7-f4f7-42a0-b8ca-d63f455ea7d3)

Join Client-1 to the domain in order to do so navigate to system settings and go to about. Off to the right select rename this pc (advanced). From there select to change the domain. Enter "mydomain.com" after that enter credentials from mydomain.com\labuser. Computer will restart and then client-1 will be a part of mydomain.com.

![mydomain client 1](https://github.com/user-attachments/assets/5b3f1c11-7834-47d8-be20-c4cbb2f56fdb)

Client-1 is now a part of the domain. Now I will set up remote desktop for non-administrative users on Client-1. I have to log into Client-1 as an admin and open system properties. Click on "Remote Desktop", allow "domain users" access to remote desktop. After completing those steps I should be able to log into Client-1 as a normal user.

![mydomain users](https://github.com/user-attachments/assets/d93ba380-086f-4ed9-b646-79560eee042e)

Lastly to verify that normal users can RDP into Client-1 I will use a script to generate thousands of users into the domain. I will input the script in powershell, after the users are created I will select one and RDP into Client-1.

![rdp client 1](https://github.com/user-attachments/assets/b81133f0-dac6-4acf-aa6e-b6605aa09081)
![domain users](https://github.com/user-attachments/assets/b9cb038a-bde7-405f-a449-6e1d9532b661)
![command line users](https://github.com/user-attachments/assets/f09a84de-1a01-436d-bdd1-b6691de06b70)

The Powershell script created a user with the username "bab.hubo" I am able to login to Client-1 with his credentials as a normal user.

<h2>Lessons Learned</h2>

This project enhanced my understanding of Active Directory configuration, including domain controller setup, user and group management, and domain joining. I learned how DNS and firewall settings affect connectivity and how to enable domain-wide access via Group Policy and Remote Desktop. It also strengthened my skills in automation using PowerShell to efficiently manage large user accounts
