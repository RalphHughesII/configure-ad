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
<p>
<br />
  <img src="https://i.imgur.com/rTZ1nuw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>  
    
 - Go back to Client-1 to see the ping succeed



  <h3>Install Active Directory</h3>

  - Go back to DC-1 and install Active Directory Domain Services
     - Click add roles and features in Server Manager
     - Click next for the first three windows, click "Active Directory Domain Services", click add features, click next three times and click install
     - Click close after completing installation
     - Click the yellow triangle on upper right corner and click "promote this server to a domain controller"
     - Select "Add a new forest" and type "mydomain.com\username" in text box

<p>
<br />
<img src="https://i.imgur.com/lxPwPPV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
   - Click next, create password, click next through next 5 windows and click install
   - Reconnect to DC-1 as user "mydomain.com" if it automatically restarts

<h3>Create Admin and Normal User Accounts in Active Directory</h3>

  - Click the start menu and type "Active Directory Users"
  - Open "Active Directory Users and Computers"
  - Right click "mydomain.com", select "new" and click "Organizational Unit"
  - Type "_EMPLOYEES and click ok
  - Right click "mydomain.com", select "new" and click "Organizational Unit"
  - Type "_ADMINS and click ok
  - Right click "Admins", highlight "new" and select "user"
  - Name the account "Jane Doe".  User logon name: "jane_admin" and click next
  - Create a password and uncheck "user must change password at next logon".  Click next


<p>
<br />
<img src="https://i.imgur.com/Uho80Tp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

 - Right click Jane Doe, click properties, click member of, click add, type domain, click check names, select domain admins, click ok, click apply and click ok

</p>
<br />
<img src="https://i.imgur.com/ZE7t2JQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 - Log out of the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
   
 <p>
<br />
<img src="https://i.imgur.com/T8FBBIy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 - Use jane_admin as your admin account from now on

</p>
<br />

<h3>Join Client-1 to your domain (mydomain.com)</h3>

 - Go back to Azure Portal and set Client 1's DNS settings to the DC's Private IP address
    - In azure type "virtual machine" in search box, click DC-1
    - Click network settings and copy the Private IP address
    - Search for virtual machines, click enter and select Client-1
    - Click network settings, click client-1 network interface
      
<p>
<br />
<img src="https://i.imgur.com/96duvAN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

 - Click "DNS Servers", click Custom, type DC-1 dns server address and click save
 - In azure type "virtual machine" in search box, click Client-1, click restart
 - Open remote desktop connection and connect to Client-1
 - Right click start menu, click system, click Rename this PC, click change, click Domain and type "mydomain.com".

<p>
<br />
<img src="https://i.imgur.com/7fJg316.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

 - Login using Jane Doe's account

<p>
<br />
<img src="https://i.imgur.com/FQfVSto.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

 - Click ok and click ok to restart
 - Open remote desktop connection and connect to Client-1
 - Login using Jane Doe's account

 <h3>Configuring Remote Desktop for non-administrative users on Client-1</h3>

 - Right click start menu, click system, click Remote Desktop and click "select users that can remotely access this PC", click add, type "domain users", click check 
   names and click ok.

<p>
<br />
<img src="https://i.imgur.com/q4iOuMN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
   
 - Log off of Client-1 and log back in using jane_admin(without needing to input mydomain.com)

<p>
<br />
<img src="https://i.imgur.com/CTiC8Sk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

 - Notice that you are able to successfully login using jane_admin
   
