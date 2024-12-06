<h1>Active Directory Lab Build</h1>

<h2>Lab Requirements</h2>
1 Windows Server, 2 Windows Workstations
<br />
60 GB Disk Space

16 GB Ram

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>VMWare</b>

<h2>Links</h2>

- <b>Windows 10 ISO:</b> [https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise)
- <b>Windows Server 2022 ISO:</b> https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022





<h2>Lab walk-through:</h2>

<p align="center">
<h3> Downloading Windows 10 and Windows Server 2022 ISO </h3> 
  Head to the links provided above and download the ISO's. You do not need to provide valid information when you register. 




![ISO](/AD-Lab-Build/Images/iso.png)

<h3>Setting up the Domain Controller</h3>

I am using VMware but you can use VirtualBox if you already have that installed.

Select "Create a New Virtual Machine."

Select the Server 2022 ISO file and leave the default options but do not press "Finish." On the last screen, remove the checkmark to power on the virtual machine and then select "Finish."

Edit the virtual machine settings and change the memory to between 4GB and 8GB and remove the floppy disk.

![Server](/AD-Lab-Build/Images/server.png)

Go ahead and power on the virtual machine.

Continue through the setup and select "Windows Server 2022 Standard Evaluation (Desktop Experience)."

![desk](/AD-Lab-Build/Images/serverdesk.png)


Select Next until you reach a section asking about installation type. Select "Custom" > "New" > "Apply" > "Okay." Press Next and wait for the installation to complete.

Once the server reboots, you will be asked to create a password for the administrator. Add a password and select "Finish."

Login to the admin account.

We are now going to name the computer.

Type "Name" in the search bar and select "View your PC name."

Rename the PC to whatever you'd like and reboot.

Now we need to make this server a domain Controller. Select "Manage" > "Add Roles and Features" and install ADDS.

Select "Promote this server to a domain controller."

![dc](/AD-Lab-Build/Images/dc.png)

Select "Add a new forest" and name it whatever you'd like.

Continue through the setup and add a password. Keeping selecting "Next" and then "Install." The Domain Controller will reboot after a couple minutes.

We now need to set up certificate services. Select "Manage" > "Add Roles and Features" and install Active Directory Certificate Services.

![adcs2](https://github.com/user-attachments/assets/db3a2155-b202-438c-a42e-4f3e9208ce90)


Once that is completed, select "Configure Active Directory Certificate Services."

Select "Next" > check "Certification Authority" > leave everything else as default. Then reboot the server.

<h3>Setting up Users</h3>

![windows](https://github.com/user-attachments/assets/bdbe9a0e-d9e9-4244-ba7e-400a4eecafb4)

You will be doing this twice for 2 Windows Workstations. On VMWare, select "Create a new virtual machine." </b>

Browse and select the recently downloaded Windows 10 Iso file. </b>

Do not worry about the product key, just press Next. </b>

You can leave the default disk capacity. </b>

Make sure to uncheck "Power on this virtual machine after creation." </b>

Select Close and then Finish.</b>

Click "Edit virtual machine settings" and remove the Floppy drive. </b>

You can now start the Windows 10 virtual machine. Make sure to press a key when it launches to boot into the ISO. </b>

You will be presented with the Windows Setup. </b>
<br />
<br />
<img src="https://i.imgur.com/sHJ01jQ.png"/>
<br />
<br />

Select Next > Install Now > Agree to the license terms > Next > Custom > New > Apply > Next.</b>

Windows will now begin installing and will restart when completed.</b>

Select your Region and Keyboard layout.</b>

Press "Domain join instead" and add a name for the user, as well as a password. </b>

Fill out the security questions. </b> 

Choose your preferred privacy settings. (preferably no) </b> 

Select Accept. </b>

Select Not Now for Cortana. </b>

Once Windows is fully installed, rename the pc and reboot.

<h3>Setting up the Users/Groups/Policies</h3>

Let's return to the Windows Server. Select Tools > Active Directory Users and Computers.

![admin](https://github.com/user-attachments/assets/c99d0d21-a262-4e38-9dc8-c272be0a3e96)

Right click on the Administrator and select "Copy." We are going to create our domain admin.

Name the user and make sure that the logon name is first inital last name. Add a password and uncheck password never expires.

Make another copy of the Admin, but this time its going to act as an service account.

I created a SQL Service account with an easy password.

Now we are going to create 2 users for the workstations. Right click the blank white space and select New > Users.

Create the users the same way we did earlier for the admin account.

We are going to create a file share.

![share](https://github.com/user-attachments/assets/e9b4f595-7514-4959-bce1-27f403dd10d6)

Select File and Storage Services > Shares > New Share. Name the share and leave everything as default.

Next, we are going to fully set up the service account. Look at the photo below and adjust the domain name and domain controller name as needed.

![Screenshot 2024-12-06 083021](https://github.com/user-attachments/assets/8829d7ef-628a-4a2b-aa8b-f7c6947c3600)

You should see "Updated Object" if done correctly.

Finally, we are going to set up group policies.

Search "Group Policy Management."

Right click your .local and create a GPO. Name it "Disable Windows Defender." Then right click the GPO and edit it.

![Screenshot 2024-12-06 115929](https://github.com/user-attachments/assets/b8155566-e9cd-40f0-aff8-2102b6ab582e)

Under Computer Configuration, select Policies > Administrative Templates > Windows Components and select Microsoft Defender Antivirus.

Double click "Turn off Microsoft Defender Antivirus" Select Enable > Apply > Okay.

Exit out of the window. Right click "Disable Windows Defender" and select "Enforced."

<h3>Adding Workstations to the Domain</h3>

On the server, search cmd to open the command prompt. Type ipconfig and write down the IPv4 address.

![ipv4](https://github.com/user-attachments/assets/b946067c-66c1-4ec6-8791-6657de79b303)

Next, go to one of your workstations and right click the network symbol on the bottom right. Select Open Network & Internet Settings > Change adapter options > Ethernet0 > Properties > IPv4. Under preferred DNS server, write down the IPv4 address of the server. Press okay.

Next, type domain in the search bar and select Access Work or School > Connect > Join this device to a local Active Directory domain.

Write down your domain name with the admin credentials. Click next and restart the workstation. Do this for both.

We now have our DC and 2 workstations.
