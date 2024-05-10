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

<h2>Prerequisites </h2>

- Create a Windows Server Virtual Machine using Azure and name it DC-1 
- Create a Windows 10 Virtual Machine using Azure and name it Client-1
- Set the Domain Controller's NIC private IP address to be static

<h2>Deployment and Configuration Steps</h2>

<h3>Ensure Connectivity between Client-1 and DC-1</h3>

 - Login to Client-1 using remote desktop connection and ping DC-1's IP address with ping -t
 - Login to DC-1 and enable ICMPv4 on the local windows Firewall
    - Click Windows icon on lower left corner of Window, type "wf.msc" and press enter
    - Click "Inbound Rules", click protocol and enable all icmp rules

  <img src="https://i.imgur.com/rTZ1nuw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
    
    
 - Go back to Client-1 to see the ping succeed

  <h3>Install Active Directory</h3>

  - Go back to DC-1 and install Active Directory Domain Services
     - Click add roles and features in Server Manager
     - Click next for the first three windows, click "Active Directory Domain Services", click add features, click next three times and click install
     - Click close after completing installation
     - Click the yellow triangle on upper right corner and click "promote this server to a domain controller"
     - Select "Add a new forest" and type "mydomain.com\username" in text box

<p>
<img src="https://i.imgur.com/lxPwPPV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
   - Click next, create password, click next through next 5 windows and click install
   - Reconnect to DC-1 as user "mydomain.com" if it automatically restarts

<h3>Create Admin and Normal User Accounts in Active Directory</h3>

  - Click the start menu and type "Active Directory Users"
  - Open "Active Directory Users and Computers"
  - Right click "mydomain.com", select "new" and click "Organizational Unit"

<p>
<img src="https://i.imgur.com/fhPDWOi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
