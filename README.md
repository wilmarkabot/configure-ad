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
Let's change our DC-1 VM's Private IP Address from dynamic to static, and to do that go to dc-1 vm and under networking go to network settings, then click on the Network Interface/ IP Configuration,
and then, Click ipconfig1, after that you will see a radio botton in the right corner on dynamic and static. check the static and that's it.
</p>
<p>
<img src="https://i.imgur.com/ZwowkFX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
After we configure DC-1 IP address from dynamic to static
we will proceed to our client vm and change the DNS settings to DC-1 Private IP address
because when we create a Windows VM the default Virtual Network or Vnet DNS is From Microsoft or Azures DNS Server
so basically what where going to do is to change that and point our Client-1 DNS server to our Domain Controller Private IP address.
and to do that go to Client-1 vm and under networking go to network settings, then click on the Network Interface/ IP Configuration,
and then, in the left side option bar choose DNS Settings, then click Custom, then paste the private ip address of your Domain Controller.
</p>
<p>
<img src="https://i.imgur.com/aHNcnen.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
after that our next task is
to log in to our Domain Controllers VM and disable the Windows Firewall to test the connectivity of the client and the domain controller so to do that go to your pc's remote desktop connection then log.in 
to the Domain Controller VM then run wf.msc or just search windows firewall in the search bar then click on the windows firewall properties then just turn it off.
</p>
<p>
<img src="https://i.imgur.com/CO1efuo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
now we will attempt to ping DC-1's private IP address from our Client VM, to do that log.in to your clients VM then open powershell ping your domain controllers private IP address.
</p>
<p>
<img src="https://i.imgur.com/SaM4G29.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
after we created the Domain Controller or the DC-1 VM and the Clients VM and configure it so that they can communicate to each other we will now proceed in installing Active Directory so what is active directory? is a directory service developed by Microsoft for Windows domain networks. It is a centralized system that manages and organizes information about network resources such as users, computers, groups, and other devices. Active Directory enables administrators to securely manage access to resources and enforce security policies across a network.
<br />
Next Promote DC1 as an actual domain controller, this means like were gonna install active directory in it but were gonna configure it to become a domain controller we call it New Forest in our domain.
so here we are going to use markwheelsdomain.com.
</p>
<p>
<img src="https://i.imgur.com/Qf9nEam.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/shhK8gX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
After Installing our Active Directory and Promoting DC1 as an actual domain controller next we will create a Domain admin user within the domain. so what we are going to do is 1st we will make Organizational Unit.<br />
1. hit start / windows administrative tools / AD users and Computers<br />
2. right click marksdomain.com / new / organizational unit / _EMPLOYEES<br />
3. create another one / _ADMINS<br />
4. click _ADMINS/ in the folders page right click and click new / click user / Firstname: Jane / Last name: Tarz / Userlog: janetarz_admin /next /password: / uncheck change pass at next logon/ never do this in real life but for this tutorial we will do it instead. check Password never expire/next/finish<br />
This account is not admin yet! so we will add this account to the build in domain admin security group so let do that.<br />
1. in admin right click jane account / go to properties/member of/click add/in the check names type domain admins/click check names /ok/apply/ok
now this account is now a domain admin
now lets logout and login again as marksdomain.com\janetarz_admin
</p>
<p>
<img src="https://i.imgur.com/yGem89q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
After Making our admin user and make it an actual admin user account we will install RAS/NAT (Remote Access Server/Network Address Translation) The purpose of this is when we will make a windows 10 client it can communicate or allow it to connect with our Private Virtual Network but still be able to access the internet through the Domain Controller. so we will install it so 1st.<br />
1. open server manager dashboard/ click add roles and features/next/ Under Server Roles: check Remote Access/ next/ Under Role Services: check Routing/ add features/ next/ install<br />
2. After that in the Upper right click on Tools/ Routing and Remote Access/ right click DC (local)/Configure and Enable Routing and Remote Access/ next/ check NAT/ next/ check use this public interface to connect to the internet/ select the _INTERNET_/ next/ Finish / if you see the DC local color is green it is good.<br />
So we configured it Perfectly.
</p>
<p>
<img src="https://i.imgur.com/Pa5FtxY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/D19jusl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />
