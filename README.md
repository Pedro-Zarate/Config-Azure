# Config-Azure
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

- Step 1 Preparing AD infrastructure in Azure
- Step 2 Depliying Active Directory 
- Step 3 Creating Users with Powershell
- Step 4 Group Policy and Manging Accounts

<h2>Deployment and Configuration Steps</h2>
<p> We will be starting with our resouce group for both our vm, named active-directory-lab this will create our virtual network and subnet 

</p>
<p>
<img src="https://i.imgur.com/GFC1WAl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
  <img src="https://i.imgur.com/vbvFxDm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p> Next we will create the Domain Controller VM (Windows Server 2022) named “DC-1” and our "Client-1" vm under the same resource group of Active-Directory-Lab and in the same region of East-US 2  
  </p>
<br />

<p>
<img src="https://i.imgur.com/seEId6a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <img src="https://i.imgur.com/0Dll1sj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>

<p>
  once both vm have been created, Our network setting will need to be adjusted on the Dc-1 vm. Click on the virtual matchines tab in azure, and next click on Dc-1. 

</p>
<p>
<img src="https://i.imgur.com/1eOtXP3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>click on network settings on the left tab, by clicking on the network interface/ ip configuration tab our ip settings will be available. </p>
<p>
<img src="https://i.imgur.com/RkmLzuQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>  Next Set Domain Controller’s NIC Private IP address to be static: by click on the ipconfig1 setting we will change our configuration allocation to static with the private address of Dc-1 then save. 
 </p>
<p>
<img src="https://i.imgur.com/VHkvIrA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />


<p> Login to dc-1 vm we will be disabling the firewall  </p>
<p>
<img src="https://i.imgur.com/bJnpzbN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p> go to azure and under client-1 vm you will have to redirect the dns settings to the dc-1 vm private ip adress under network settings - dns settings change to custom and input dc-1s private ip adress. dont forget to reset client-1 under vm tab in azure to reboot the system after. </p>

<img src="https://i.imgur.com/16Kyh2B.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t (perpetual ping) & run ipconfig/all </p> 
<img src="https://i.imgur.com/Jy84rmE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qK2GdIZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ZBBcwqJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> We have now successfully Set up our domin controller, setup our client vm, and configuered our ip adress settings for our active directory</p>
