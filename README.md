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

<h2>Deployment and Configuration Steps</h2>

- Setup Domain Controller in Azure
- Setup Client-1 in Azure



<p>
In This Lab First is we will make a Windows Server Virtual Machine in Microsoft Azure, We will use Windows Server 2022 and we will name it DC-1
Before that Create a Resourse Group named Active-Directory-Lab then we will also Create a Virtual Network named Active-Directory-VNet after Creating this two components proceed in creating our Virtual Machine Server.
</p>
<p>
<img src="https://i.imgur.com/Wy1fiXf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
After we created our Windows Server VM let proceed to creating our Client VM. To do that 1st Go to your Microsoft Azure portal, then Click Create VM, then Choose the Windows 10 VM, and named it Client-1
then enter username and password and attach it to the same region as the Windows Server and Virtual Network and then click create. 
</p>
<p>
<img src="https://i.imgur.com/LT7Ipwm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Let change our DC-1 VM's Private IP Address from dynamic to static, and to do that go to dc-1 vm and under networking go to network settings, then click on the Network Interface/ IP Configuration,
and then, Click ipconfig1, after that you will see a radio botton in the right corner on dynamic and static. check the static and that's it.
</p>
<p>
<img src="https://i.imgur.com/ZwowkFX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<p>
<img src="https://i.imgur.com/Wy1fiXf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

