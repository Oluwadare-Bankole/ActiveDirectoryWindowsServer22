# ActiveDirectoryWindowsServer22

<h2>Description</h2>
This will be an Active Directory Lab that simulates a corporate network. There will be a virtual windows 2022 Server that acts as a Domain Controller for our a virtual Client. We will make the necessary Configurations on this Domain Controller for our end clients to receive an ip address and be able to access the internet

<h2>Virtual Machine Specifications</h2>

Virtual Box(Hypervisor used):
https://www.virtualbox.org/wiki/Downloads
<br />
VM1 - Windows 20222 Server - https://info.microsoft.com/ww-landing-windows-server-2022.html
<br />
VM2 - Windows 10 - https://www.microsoft.com/en-us/software-download/windows10
<br />

Please download the virtualbox hypervisor and the isos from the links above

<h2>Network Topology</h2>
<img src="https://i.imgur.com/Gwgffdz.png" height="80%" width="80%" alt="Active Directory Topology"/>

<h2>Domain Controller Installation</h2>
Open VirtualBox,
Select the new icon and input the name of the Virtual Machine. In my case I am selecting  Windows 2022 since we are using Windows 2022

<img src="https://i.imgur.com/RTJ8Xnd.png" height="80%" width="80%" alt="Domain Controller setup"/>

You should now be able to see the newly created VM specification.(disregard my kali linx VM as that is unrelated to this lab) Select the Settings button as highlighted in the below image.
<img src="https://i.postimg.cc/jqXCN50n/image.png" height="80%" width="80%" alt="Domain Controller setup"/>

Select the Advanced option under the General Tab. Ensure the Clipboard and Drag'n'Drop are set to bidirectional
<img src="https://i.postimg.cc/bw7H3PLf/image.png" height="80%" width="80%" alt="Domain Controller setup"/>

Go to System -> Processor -> Modify the number of CPUs to be more than 1 if your Workstation allows for it!
![image](https://github.com/user-attachments/assets/509669c1-ed30-44d7-b178-2b02d29f0937)

<img src="https://i.postimg.cc/jqXCN50n/image.png" height="80%" width="80%" alt="Domain Controller setup"/>

You should now be able to see the newly created VM specification.(disregard my kali linx VM as that is unrelated to this lab) Select the Settings button as highlighted in the below image.
<img src="https://i.postimg.cc/jqXCN50n/image.png" height="80%" width="80%" alt="Domain Controller setup"/>
