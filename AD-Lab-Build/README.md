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



