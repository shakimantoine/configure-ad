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



<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1 – Setup the Domain Controller (DC-1)

In Azure:

Create a Resource Group.

Create a Virtual Network and Subnet.

Create a Windows Server 2022 VM named DC-1.

Username: labuser

Password: Cyberlab123!

After creation:

Set DC-1’s NIC Private IP to static.

Log into DC-1 and disable Windows Firewall (for connectivity testing).
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 2 – Setup the Client Machine (Client-1)

In Azure:

Create a Windows 10 VM named Client-1.

Username: labuser

Password: Cyberlab123!

Attach it to the same region & VNet as DC-1.

After creation:

Set Client-1’s DNS to DC-1’s Private IP.

Restart Client-1 from the Azure Portal.

On Client-1:

Log in and ping DC-1’s private IP → verify success.

Run ipconfig /all in PowerShell → confirm DNS = DC-1 private IP.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 3 – Enable Remote Desktop for Domain Users

Log into Client-1 as mydomain.com\jane_admin.

Open System Properties → Remote Desktop.

Allow Domain Users to access Remote Desktop.

Verify that a non-admin domain user can log into Client-1.

(Normally this would be automated with Group Policy.)
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 4 – Create Additional Users in AD and Test Login

On DC-1:

Log in as jane_admin.

Open PowerShell ISE as Administrator.

Paste and run the user creation script : https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1.

Verify in Active Directory Users and Computers (ADUC) → accounts appear in _EMPLOYEES OU.

Attempt login on Client-1 with one of the new accounts (use the password from the script).
</p>
<br />

