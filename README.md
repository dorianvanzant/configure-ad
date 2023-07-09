<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure and ensure connectivity between the Client and Domain Controller
- Install Active Directory and create an Admin and Normal User Account
- Join the Client to the Domain and Setup Remote Desktop for Non-Administrative Users
  - Attempt to log into the Client as a regular user

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create two Virtual Machines, one using Windows Server 2022, "DC-1," which will serve as the Domain Controller and the other using Windows 10, "Client-1," which will serve as a Client on the network. Ensure they are both on the same Virtual Network. Change DC-1 NIC's Private IP address to Static, as it will be used later as a DNS Server for Client-1. Using Remote Desktop, login to DC-1 and enable ICMPv4 on the local windows Firewall. Login to Client-1 and ping DC-1's private IP address.   
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install Active Directory on DC-1. Promote as a Domain Controller. Setup a new forest. Restart and login. In ADUC, create Organizational Units for Employees and Admins. Create a new employee and add them to the "Domain Admins" Security Group. Logout and log back in as the new employee. They'll be used as the new Admin. Create another employee, and leave them in the Domain User Security Group.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the Azure Portal, set Client-1's DNS settings to the Domain Controller's Private IP Address. Restart Client-1. Login as the original local admin and join it to the Domain. Restart Client-1. Client-1 should now show up in ADUC inside the "Computers" Container. Login to Client-1 as the Admin. System Properties --> Remote Desktop. Allow the Domain Users Security Group to access the client via Remote Desktop. You can now log into Client-1 as a normal, non-administrative user. This can be done to multiple computers at once using Group Policy. Attempt to login to Client-1 as the regular employee you created earlier.
</p>
<br />
