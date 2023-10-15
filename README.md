# Creating-and-Using-Active-Directory
This section outlines the process used in creating and implementing active directory.
<p align="center">
<img src=https://i.imgur.com/scEzmHu.png)</p>



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- A control Virtual Machine (VM1)
- A client VM (VM2)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Windows Server 2022 Data Center 

<h2>Pre-Setup Steps</h2>

- Create Controller "VM1"
- Set NIC Private IP to "Static" for for VM1
- Create Client "VM2"
- Ensure that VM2 is registered to the same virtual network and Resource Group 
- Login to VM1 and allow ICMPv4 on the Local Windows Firewall
- Login to VM2 and ping VM1 (I used Wireshark to view traffic between the VMs) 

<h2>Configuration Steps</h2>

<p>
<img src=https://i.imgur.com/mIY3rGY.png</p>
<p> 
<p>  
<img src=https://i.imgur.com/4W70BSE.png<p>
<p>
<p>
<img src=https://i.imgur.com/vRb7HNv.png
<p>  
- Login to VM1 and navigate to Server Manager via the start menu. Open the "Add Roles and Features" wizard, listed at #2 on main Server Manager page.
<p>  
- Press Next or change settings as applicable until page entitled "Roles" is reached. Select "Active Directory Domain Services" checkbox. Press next, and select features as desired. Once complete, click onward to the Install option and install Active Directory.
<p>  
- Once installation is complete, you will be dropped back to the Server Manager main page. In the top right corner of the window, you will see a flag with a caution symbol. Select the option "promote this server to a domain controller". Select "add a new forest". You will be asked to create a domain name and password. I chose "wolverine.com" just for this example. Once the installation is complete the VM will log out.
<p> 
- Once the log out is finished, login using the new domain user you created. Mine was wloverine.com\mikle1 in this example. Your original login password for VM1 should be used.
<p>
<img src=https://i.imgur.com/d7jFlKc.png
<p>  
<p>
- Navigate to Active Directory Users and Computers via the start menu.  
</p>
<p>
<img src=https://i.imgur.com/o6TzXm7.png
<p>
<p>  
-Select your domain name listed to the left. Right click, select "New" and "Organizational Unit". Create orgainzational units for admins and for your users.
<p>
- Move to your admin unit and right click to select "New" and "User". Provide the information for the administrative user and accept the settings.
<p>
- Right click the newly created admin user and select "properties". Select "member of" tab at the top of the window that opens. Select "add" and input "Domain Admin" into the space provided. Check the name to ensure valid entry. Select apply and ok. This will enable the user to be classified as a administrator in more than just name.  
</p>
-Log off and re-login as the new admin that was just created. It will look similar to the image below.
<p>
<p>
<p>  
<img src=https://i.imgur.com/oBVkkyb.png)</p>
<p>
<p>  
- From here, the DNS settings must be changed to match VM1's private IP address. Restart the VM from Azure and re-login.
<p>  
<p> 
<img src=https://i.imgur.com/inhdRFS.png
<p>
<p>  
- Login to VM2 and right click the start icon to select "system". Select "Rename this PC (Advanced)". Read and press the option "Change". Under "member of" select domain and input domain name. Ex. wolverine.com. In the window that pops up, enter your admin account info as shown above.
</p>
- The VM will want to restart after successfully accessing the domain. Once finished, login as the admin account into VM2. Access the system window once again via the start menu and navigate to the "Remote Desktop" link on the right hand side of the window. Access "Select users that can remotely access this PC". Add, then simply put "Domain Users". Apply the changes. Users can be added on VM1 via the Active Directory Users and Computers window. Create users and test logins.
<p>
- NOTE: Accounts may also be unlocked, passwords may be changed, and other duties performed concerning user accounts via the Active Directory Users and Computers screen in the admin's PC.
