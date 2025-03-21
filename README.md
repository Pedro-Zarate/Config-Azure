# Config-Azure
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
  Once both vm have been created, Our network setting will need to be adjusted on the Dc-1 vm. Click on the virtual machine tab in azure, and next click on Dc-1. 

</p>
<p>
<img src="https://i.imgur.com/1eOtXP3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>Click on network settings on the left tab, by clicking on the network interface/ ip configuration tab our ip settings will be available. </p>
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


<p> Go to azure and under client-1 vm you will have to redirect the dns settings to the dc-1 vm private ip adress under network settings - dns settings change to custom and input dc-1s private ip adress. dont forget to reset client-1 under vm tab in azure to reboot the system after. </p>

<img src="https://i.imgur.com/16Kyh2B.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t (perpetual ping) & run ipconfig/all </p> 
<img src="https://i.imgur.com/Jy84rmE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qK2GdIZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ZBBcwqJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> We have now successfully Set up our domin controller, setup our client-1 virtual machines dns to our Dc-1'private ip adress. </p>


- Step 2 Depliying Active Directory 

<p> Setting up active directory, log into DC-1 and install AD through server manager - add roles and features </p>

<img src="https://i.imgur.com/xXILZ3E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Select active directory domain services then continue to click on next </p>

<img src="https://i.imgur.com/YoRfllg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<p> Active Directory is now installed </p>
<img src="https://i.imgur.com/bvBVG6P.png " height="80%" width="80%" alt="Disk Sanitization Steps"/>


<p> login to Dc-1 to promote it as the main domain controller by setting up a new forest (mydomain.com)  </p>

<img src="https://i.imgur.com/Y8QY6Ix.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/IuY42Jm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/MIOUpgz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/zZDMkx5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Shff5i2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Now log into dc-1 with your domain username </p>
<img src="https://i.imgur.com/OPEgPlb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<p> Open active directory Users and computers and create a new organizational unit </p>
<img src="https://i.imgur.com/cB5Cag6.png " height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Name it _EMPLOYEES </p>

<img src="https://i.imgur.com/6YOTXs6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Create a second folder and name it _ADMINS </p>

<img src="https://i.imgur.com/ch2ejQ9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Inside admins folder create a new user </p>
<img src="https://i.imgur.com/KIs9EXN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ncQcZmv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Once the user is created open the users properties and set the users member of group to domain admins </p>

<img src="https://i.imgur.com/XTzUo8i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Now we can log in as an admin under this user </p>


<img src="https://i.imgur.com/6rWD7y8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> Join Client-1 to the domain </p>
<img src="https://i.imgur.com/d7JYh7u.png " height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/uQhz9sa.png " height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p> Login to Dc-1 (Domain Controller) to verify Client-1 shows up in Active Directory users and computers </p>
<img src="https://i.imgur.com/gqLFHS5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 

<p> create a new organizational unit and name it _CLIENTS then drag over the Client-group over to the new _CLIENTS folder to keep it organzied  </p>

<img src="https://i.imgur.com/6PwizCY.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/eFzG8LY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 

<p> Setup remote desktop for non-administrative users on Client-1 by loggin back into client-1 and using the admin user name  </p>

<img src="https://i.imgur.com/Q8EWr6b.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 


<p> Open system properties
Click “Remote Desktop”
Allow “domain users” access to remote desktop
You can now log into Client-1 as a normal, non-administrative user now
  </p>

<img src="https://i.imgur.com/EBpKrd2.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 

<!--- come back and add the script repo to the ancore tag below  -->
-Step 3 Creating Users with Powershell


<p> Create a bunch of additional users and attempt to log into client-1 with one of the users </p>
<p> Login to DC-1 as jane_admin
Open PowerShell_ise as an administrator
Create a new File, save it  and paste the <a href="https://github.com/Pedro-Zarate/Generate-names-AD-users/blob/main/Generate-Names-Create-Users.ps1"> script </a>  into it
Run the script and observe the accounts being created
 </p>

<p> When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES)
 </p>

 <img src="https://i.imgur.com/Bhrjtqt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 

-Step 4 Group Policy and Manging Accounts

<p>We will need to configure the account lockout policy in active directory on Dc-1 first, open run and type gpmc.msc, press enter.
This will open the policy management console.
</p>

 <img src="https://i.imgur.com/i0mNlTW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 

<p> Create or edit a group policy object

1. Navigate to the group policy objects section.
2. Right-Click Group Policy Object and select new to create a new GPO, or right click an existing GPO and edit to modify it.
   Give the new GPO a descriptive name (Account Lockout Policy) we will be editing the current policy.
</p>
 <img src="https://i.imgur.com/arYIqn8.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 

<p> Navigate to the account lockout policy settings 
  1. Inside the group policy management editor, expand the following 
    Computer configuration > Policies > Windows Settings > Security Settings > Account Policies 
</p>
 <img src="https://i.imgur.com/xQlU1Lz.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 


<p> Configure account lockout policy settings 
  1. Change the Account lookout duration
  2. update the group policy ( wait for it to automatically update or on the client-1 machine you can run gpupdate/force on Command Prompt to manually update.
</p>

 <img src="https://i.imgur.com/pAhslpB.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 



<p> Dealing with account lockouts </p>

<p> Now we can try and lock out one of our users by attempting a wrong password 5 time locking us out.
</p>

 <img src="https://i.imgur.com/ZrAwVO5.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 <img src="https://i.imgur.com/9sYK1W8.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 

<p> we will unlock this account by loging back into our domain controller account (Dc-1) 
Open Active directory and looking for the user once the user is found click on the user to unlock account, you can also reset passwords from this window </p>

 <img src="https://i.imgur.com/O1xNuYo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 

 <p> Now we have successfully unlocked the account   </p>


 <img src="https://i.imgur.com/lLt2buB.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 


Enabling and Disabilling Accounts And Password Resets 

<p>  open Active Directory in the domain controller DC-1vm right click on the _Employees folder to search for the user account you want to disable or rest password. </p>
1. Disabilling
 <img src="https://i.imgur.com/GUiAnPl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
2. Password Reset 
 <img src="https://i.imgur.com/jLDVTNn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 























