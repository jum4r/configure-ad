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
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Domain Controller (DC-1) and Install Active Directory (AD)
- Create Admin & Normal User in AD
- Connect Client-1 to DC-1 DNS
- Conigure Remote Desktop for Non-Admin Users on Client-1 

<h2>Deployment and Configuration Steps</h2>

<h3>Setting up Resources in Azure</h3>

<p>
<img src="https://i.imgur.com/wz1Mamc.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, we'll create the Domain Controller VM using Windows Server 2022 with 2 vCPUs and name it 'DC-1'. Create the login credentials and store them in Notepad. Click 'Review + Create'.
</p>
<p>
<img src="https://i.imgur.com/LEe0cfL.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qSgCZnG.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once it's finished deploying, create another VM using Windows 10 with 2 vCPUs and name it 'Client-1'. Use the same Resource Group, Location, and VNet as 'DC-1'. Click 'Review + Create'.
</p>
<p>
<img src="https://i.imgur.com/RPZ9ajm.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back in Azure, navigate to the 'DC-1' VM -> Networking -> Network Interface -> IP Configurations. Click on 'ipconfig 1', change from Dynamic to Static, then click 'Save'.
</p>
<br />

<h3>Ensuring Connectivity between VMs</h3>

<p>
<img src="https://i.imgur.com/Eem450C.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we'll ensure connectivity between Client-1 and DC-1. Log in to Client-1 using Remote Desktop and ping DC-1’s private IP address(Yours may be different). Open the 'cmd' prompt and type 'ping -t [IP address]' (Continuous Ping). Observe the 'request timed out' responses.
</p>
<p>
<img src="https://i.imgur.com/SSnGysk.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, log in to DC-1 and enable ICMPv4 in the local Windows Firewall. Search for 'wf.msc' in the Windows search bar, navigate to Inbound Rules, and sort the list by Protocol. Scroll down to find ICMPv4 and look for 'Core Networking Diagnostics - ICMP Echo Request' (there should be two instances listed). Right-click on each, then select 'Enable Rule' for both.
</p>
<img src="https://i.imgur.com/kTSv4cW.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Return to Client-1 and check to see if the ping succeeds. Press 'Ctrl + C' to stop the ping.
</p>
<br />

<h3>Installing Active Directory</h3>

<p>
<img src="https://i.imgur.com/DJLQz9h.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/A7VraCl.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
Return to DC-1 and install Active Directory by clicking 'Add roles and features' in Server Manager. While installing, you'll reach a step where you're asked to create a password. This feature won't be used, so just input a simple password. Progress through the installation process by clicking 'Next' until you reach the Server Roles section where you'll choose to install Active Directory Domain Services. Continue with the installation process until it completes.
</p>
<p>
<img src="https://i.imgur.com/6QDJPiV.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/fRYQ7YO.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
After completion, return to Server Manager, click the exclamation mark to promote this VM to Domain Controller. In Deployment Configuration, choose 'Add a new forest'. Input 'mydomain.com' or your chosen domain name. Keep clicking 'Next' until installation is done and DC-1 restarts. To log in to DC-1, use 'mydomain.com[username]' or your chosen domain name
</p>
<br />

<h3>Creating an Admin & Normal User Account in AD</h3>

<p>
<img src="https://i.imgur.com/H09kFoN.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/MySHYNV.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Server Manager, navigate to Tools, then choose Active Directory Users and Computers (ADUC). In the left pane, right-click on mydomain.com, select New, and opt for Organizational Unit (OU). Name the first one "_EMPLOYEES" and create another named "_ADMINS".
</p>
<p>
<img src="https://i.imgur.com/p0n2IXN.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/lCNByzC.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
Choose the newly created "_ADMINS" OU, right-click, and pick New, followed by User. Use "Mary Jane" for the name field, and input "mary_admin" under 'User logon name'. Proceed to set a password, uncheck 'User must change password at next login', and check 'Password never expires'. Make sure to take note of these login info.
</p>
<p>
<img src="https://i.imgur.com/01fDHjR.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/1wkO1kv.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right-click on Mary Jane, then select Properties. Navigate to Member Of, click Add, and enter 'Domain Admins'. Click 'Check Names', then press OK. Finally, apply the changes to grant Mary Jane admin privileges.
</p>
<br />

<h3>Connecting Client-1 to your domain (mydomain.com)</h3>

<p>
<img src="https://i.imgur.com/zT6WgYP.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/BqBlist.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
On your personal PC, access the Azure Portal, then go to Virtual Machines -> DC-1. Copy the Private IP seen after scrolling down. Proceed to Virtual Machines -> Client-1 -> Networking -> Network Interface: [number] -> DNS servers. Select Custom, paste the DC-1 Private address, and Save. Return to Azure Portal, go to Virtual Machines -> Client-1, and click Restart.
</p>
<p>
<img src="https://i.imgur.com/a4PQnPR.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/L17uKuT.png" height="20%" width="20%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into Client-1 using the initial local admin account. Right-click the Start button, then select System. Proceed to Rename this PC -> Change -> Choose Domain, and input 'mydomain.com'. Enter the Domain Admin credentials (e.g., mydomain.com\mary_admin) along with the password. Allow time for a confirmation popup regarding the Domain change, which could be hidden behind other open windows. Click OK when the restart prompt for Client-1 appears. Client-1 should close at this point.
</p>
<br />

<h3>Configure Remote Desktop for Non-Admin Users on Client-1</h3>

<p>
<img src="https://i.imgur.com/JutPOSV.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log back into Client-1 as mydomain.com\mary_admin. Right-click the Start button, then choose System. Click Remote Desktop, and under User Accounts, click 'Select users that can remotely access this PC'. Click 'Add', then type Domain Users, press 'Check Names', and click OK. Now you can log into Client-1 as a regular non-admin user.
</p>
<br />

<h3>Creating Additional Non-Admin Users for Client-1 Access</h3>

<p>
<img src="https://i.imgur.com/FTsZRbK.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log in to DC-1 as mary_admin if not already open. Open the <a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1">PowerShell Script</a>, copy the raw data. On DC-1, Windows Search "powershell ise," right-click and Run as Administrator. In the PowerShell window, click New Script, paste the PowerShell Script, and then click Run.
</p>
<p>
<img src="https://i.imgur.com/fsP9o8R.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
After completion, go to ADUC and navigate to _EMPLOYEES to observe the created users. Choose any user, right-click the name, then select Properties -> Account tab to copy the logon name. Close Client-1 if still open. Log in to Client-1 using mydomain.com[chosen user] with the password 'Password1' as is the same for all the created users. Once you've successfully logged in as a regular user on Client-1, you have effectively confirmed Active Directory functionality.
</p>
<br />
