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
