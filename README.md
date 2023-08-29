<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/wz1Mamc.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/LEe0cfL.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qSgCZnG.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/RPZ9ajm.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, we'll create the Domain Controller VM using Windows Server 2022 with 2 vCPUs and name it 'DC-1'. Create the login credentials and store them in Notepad. Click 'Review + Create'. Once it's finished deploying, create another VM using Windows 10 with 2 vCPUs and name it 'Client-1'. Use the same Resource Group, Location, and VNet as 'DC-1'. Click 'Review + Create'. Back in Azure, navigate to the 'DC-1' VM -> Networking -> Network Interface -> IP Configurations. Click on 'ipconfig 1', change from Dynamic to Static, then click 'Save'.
</p>
<br />

<p>
<img src="https://i.imgur.com/UlIDOOi.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we'll ensure connectivity between Client-1 and DC-1. Log in to Client-1 using Remote Desktop and ping DC-1’s private IP address. Open the 'cmd' prompt and type 'ping -t [IP address]' (Continuous Ping). Observe the 'request timed out' responses.
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
<p>
Next, we'll ensure connectivity between Client-1 and DC-1. Log in to Client-1 using Remote Desktop and ping DC-1’s private IP address. Open the 'cmd' prompt and type 'ping -t [IP address]' (Continuous Ping). Observe the 'request timed out' responses. Now, log in to DC-1 and enable ICMPv4 in the local Windows Firewall. Search for 'wf.msc' in the Windows search bar, navigate to Inbound Rules, and sort the list by Protocol. Scroll down to find ICMPv4 and look for 'Core Networking Diagnostics - ICMP Echo Request' (there should be two instances listed). Right-click on each, then select 'Enable Rule' for both. Return to Client-1 and check to see if the ping succeeds. Press 'Ctrl + C' to stop the ping.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
