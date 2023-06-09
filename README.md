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

- Create a Domain Controller(DC-1) and Client(Client-1) in Azure.
- Install Active Directory on DC-1
- Create an Administrative Account
- Connect Client-1 to DC-1
- Create Multiple Users and log into CLient-1 with additional user

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/CAOPFHo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
<br />

<p>
<img src="https://i.imgur.com/UY8IDzP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Azure create Windows Server VM and name it DC-1. Create a client VM. Set the DC-1 NIC(Network Interface Card) from dynamic ip to static so the ip address stays the same. Go to Virtual Machines, click on DC-1> Networking> Network Interface> IP Configurations> Click on the Private IP Address Number, where it says dynamic, change it to static and save.
</p>
<br />

<p>
<img src="https://i.imgur.com/OBJ75GJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
</p>
<br />

<p>
<img src="https://i.imgur.com/tbPBrvc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Make sure there is connectivity between the Server and Client. Enable ICMPv4 on the DC-1 Local Firewall. Log into DC-1 using RDP. Type firewall into the search and click on Windows Defender Firewall with Advanced Security> Inbound Rules, click on the Protocol column to sort. Find ICMPv4. Right click on both Core Networking Diagnostics Echo Requests and click enable rule. RDP into CLient-1 and ping DC-1's private ip address to test connectivity.
</p>
<br />

<p>
<img src="https://i.imgur.com/jCSfds2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
</p>
<br />

<p>
<img src="https://i.imgur.com/stMJThb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

<p>
<img src="https://i.imgur.com/JZDXnvb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to DC-1. Pull up Server Manager from the start menu. Click add roles and features. Click next button to server roles and check "Active Directory Domain Services". Next all the way through then click install. Click on the flag in upper right hand corner with Yellow caution triangle, click promote this Server to Domain Contoller. Check Add a new forest. Create a domain name mydomain.com. Create password. Next to install option. Then click install and computer will restart. You will have to remote back in.
</p>
<br />

<p>
<img src="https://i.imgur.com/cSHrySJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
When remoting back into DC-1 select more options and change the log in to mydomain.com\labuser.
</p>
<br />

<p>
<img src="https://i.imgur.com/r4dUNEq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click Start and type in Active Directory Users and Computers. Right click mydomain.com> new> Organizational Unit. Create two organizational units. Name one _Employees and the other _Admins.
</p>
<br />

<p>
<img src="https://i.imgur.com/qj8gORR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next Practice creating an Administrative Account. Right click _ADMIN select New> User. Now add the "Jane Doe" account to a member of Domain Admins. Right click on Jane Doe from the _ADMIN folder. Select Properties and go to the Member Of tab. Click Add. Type domain and select check names. Select Domaini Admins> Ok> Apply. Now we will log out as labuser and log back in as Jane Doe.
</p>
<br />

<p>
<img src="https://i.imgur.com/6CCgogf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

<p>
<img src="https://i.imgur.com/IgX6Je3.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

<p>
<img src="https://i.imgur.com/UQRLuJx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Join Client-1 to DC-1. In Azure set Client-1's DNS settings to the DC's Private IP Address. In Azure go to Virtual Machines> Client-1> Networking> Network Interface: Client> DNS servers. Click custom and enter DC-1's private ip address. Restart Client-1. In Client-1 right click start> System> Rename This PC(Advanced)> Change> Click domain bubble and enter mydomain.com click ok. Use the Administrative account created. mydomain.com\jane_admin. Computer will restart. Log back under the Jane Admin account. Right Click Start> System> Remote Desktop> Add. From here type "domain users" and click check names, select ok.
</p>
<br />

<p>
<img src="https://i.imgur.com/C6wgHFp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

<p>
<img src="https://i.imgur.com/A2MOsTw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

<p>
<img src="https://i.imgur.com/mp2oFv7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next create a bunch of additional users. Log into DC-1 as jane_admin. Open powershell_ise as an administrator(right click from start and select run as administrator). You can create new accounts from Active directory I will use a powershell name generator script. Select new script. Paste chosen script. Click run. While the script is creating users go back to Active Directory right click the _EMPLOYEES file created earlier. Refresh and select(double click) a random created user. Go to the Accounts tab and copy the Display name. 
</p>
<br />

<p>
<img src="https://i.imgur.com/0NleT7S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
</p>
<br />
<p>
<img src="https://i.imgur.com/CHKUCPr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to Client-1 (log out if logged in) log in as the selected new user. Finished!!
</p>
<br />

