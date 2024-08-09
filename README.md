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

![Active Directory Topoogy-revised drawio](https://github.com/user-attachments/assets/6c35e581-469d-4931-a7fa-560455ed6ef6)



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

Select Storage, select the Icon that looks like a disk then select the smaller disc icon next to the optical drive drop down menu. From this drop down menu select the Windows server that you have downloaded. Mine is named SERVER_EVAL_x64FRE_en-us.iso

![image](https://github.com/user-attachments/assets/4100f133-b1e9-4ad7-ac13-cf9c52cf3ead)


Click OK to save the settings. After doing this, boot the virtual machine. You will eventually land at the following page. Ensure you select something that has Desktop Experience

![image](https://github.com/user-attachments/assets/4d9bb875-0619-4744-ad1b-6a61d73d2bd5)

Accept the agreements

![image](https://github.com/user-attachments/assets/444dbb1d-eb5a-4f79-9fc3-c115b5b69877)

Sekect the custom install option

![image](https://github.com/user-attachments/assets/57cdc985-08b7-456d-9e35-a482b684dde8)

Select Next on the screen where the drives are present

Wait for this screen to finish

![image](https://github.com/user-attachments/assets/e5ab2f37-677e-4ddc-851a-1b6d64434b33)

It will take about 30 minutes from here to finish loading. Once doe, you should be at this page

![image](https://github.com/user-attachments/assets/d4cc8d15-4a79-44e6-885a-dd2b46f69d0c)


Specify your password for the default Administrator. I'm making mine my name and the current year but it can really be anything

![image](https://github.com/user-attachments/assets/7573b16c-4836-4d86-bfb1-5bd6a00dd20f)

You should be at the home screen now

![image](https://github.com/user-attachments/assets/a7bd5b7e-7a51-45fd-a7ee-e58eb1fc4d23)

Select the input menu at the top -> Keyboard -> Insert Ctrl + ALT + DEL
Login with the previously created password

A pop-up on the right side of the screen may indicate the option to allow this computer to be discoverable by other devices on the network, select yes

The server manager dashboard may open upon first launch, feel free to close it

Select the Devices menu -> Insert Guest Addition

![image](https://github.com/user-attachments/assets/e94174ee-e139-47e2-bc2c-f07bc6dddd6b)

Select the File explorer button at the menu bar, in the window that pops up select "This PC", then doubleclick the CD Drive Virtualbox guest additions

![image](https://github.com/user-attachments/assets/a9dd7e4b-74a3-4765-9a1f-844087d01439)

Proceed with the installation steps and you should get to a step that looks like this

![image](https://github.com/user-attachments/assets/bacf131e-eac2-43a6-b34d-44971a332fcf)

Select the I want to manually reboot later option. After doing this select the shutdown option from the menu

![image](https://github.com/user-attachments/assets/76c467db-8578-4a54-a7a1-9f3c99cef9ec)

Once it shuts down, restart the VM by doubleclicking the VM name

<h2>Configure Network Adapters</h2>

Once the VM has started back up, select the small network icon in the bottom right corner then select the Network and Internet Settings

![image](https://github.com/user-attachments/assets/dac37ddc-03e7-4b21-a028-067cb3963cdf)


Select the Change Adapter options

![image](https://github.com/user-attachments/assets/45e845c1-ca3e-4665-a6e7-30ac994bf666)

There should be a page that has 2 network adapters

![image](https://github.com/user-attachments/assets/6a3f805b-9a85-4e35-a07c-619111c6a6eb)

One of these adapters will connect to your home network while another will connect to the internal virtualbox network. This is showcased in the diagram

To identify which is which, right click one of these adapters then select the status. We can confirm that it has internet connectivity by looking at the IPv4 connectivity row and seeing "Internet"

![image](https://github.com/user-attachments/assets/fce37d6f-f864-4344-b1ba-6743551d893c)


We can also select the details button and observe that the Ipv4 address is a valid IPv4 address on a private IP address range

We can right click on this ADAPTER and rename it to INTERNET for easier identification purposes
For the other Adapter we can right click on it and name it to Internal

![image](https://github.com/user-attachments/assets/28ab2266-6f20-453d-9c09-ee0c16c81b45)

We can proceed with renaming this PC now. Start by Right clicking the Start menu then selecting system

![image](https://github.com/user-attachments/assets/12ddddc9-9345-41ce-b601-8063314b0b36)

On the following page you should have the option to rename this workstation. I renamed my workstation to DC2024. After changing the name the Workstation should restart

Log back into the workstation

Select the network icon in the bottom right corner, then select network and internet settings
Right click the internal adapter, select properties 

![image](https://github.com/user-attachments/assets/a2e49393-1e96-446b-ad75-70f4955c6e75)


Double click the Ipv4 option

![image](https://github.com/user-attachments/assets/9f073497-43f4-4f52-abda-6fbac687d5f8)


Configure the following IP and DNS values

![image](https://github.com/user-attachments/assets/f17d8f83-5574-42e6-b647-8b5198f5c534)


Select OK

<h2>LETS INSTALL ACTIVE DIRECTORY</h2>

Open the Server Manager Dashboard if it is not open already. It looks like this:

![image](https://github.com/user-attachments/assets/40e3fbda-0519-405b-a5fe-fa3bf20fb2ac)

Select the Add Roles and Features

![image](https://github.com/user-attachments/assets/bf2f4aba-5cd7-4b6b-9d1e-5cbf0dc48421)

Select Next and next again until you get to the following page:

![image](https://github.com/user-attachments/assets/c7fe5be6-0461-4090-9063-d535a2a79651)

The Server you have created should be present there. Click Next, you should be at a screen that looks like this

![image](https://github.com/user-attachments/assets/ba174a6f-5b76-489b-824d-2714c23d6127)


Select the Active Directory Domain Services, this should pop up

![image](https://github.com/user-attachments/assets/bac644e2-8c9d-4ad8-ad51-b0ede7e979b8)


Select the Add Features. Click next then next again. Once you are here press install

![image](https://github.com/user-attachments/assets/b7f68982-7e57-4320-aa3a-11b7fafe42ff)

Wait for the installation to finish. Once it is done, there should be a yellow triangle in the corner. Select it

![image](https://github.com/user-attachments/assets/3b12c90d-bdff-45c5-bcf1-0fe968e1369e)

Select the Promote this server toa  domain controller

![image](https://github.com/user-attachments/assets/e57761bd-ff6c-4711-a5e5-cb62a9dff7fe)

In the Deployment Configuration, select the "Add a new forest" and specify an arbitrary domain name

![image](https://github.com/user-attachments/assets/72d9de9e-56c2-41de-834c-dcc932060312)

Enter arbitrary password

![image](https://github.com/user-attachments/assets/7496ef50-8f5b-444d-9228-c18036d38085)

Continously click next until you are able to install, then install

![image](https://github.com/user-attachments/assets/8dc9ccd8-78ad-4723-883a-87cfd3d7a0d0)

After it installs you should be able to log back in. You will notice that the login prompt has your name

![image](https://github.com/user-attachments/assets/79c2c3f7-6b47-4e43-99b4-590d2909623b)

Log back in
Were going to create a domain account for our admin

Press the start menu -> Active Directory Users and Computers

![image](https://github.com/user-attachments/assets/edea2d4a-943b-4d9f-8109-6526dca907f3)

Once it opens, you should see your domain on the left hand side. Right click it and create a new organizational unit

![image](https://github.com/user-attachments/assets/2b614656-5645-495c-bb77-ca586d6601f1)


Name it ADMINS

![image](https://github.com/user-attachments/assets/adc292c7-901a-4095-9c9a-4694d623938c)

You should see it appear under your domain, create a new User by right clicking the newly created organizational unit

![image](https://github.com/user-attachments/assets/177d64ae-3529-4d5c-8095-65359e6dee3e)

In the following page you want to provide your account information then a login name. I specifed the nomenclature a-obankole

![image](https://github.com/user-attachments/assets/1390342a-47e9-4f24-a9e7-e838898304c9)

Select Next, then define the password. Deselect the User must change password at next logon and select the Password never expires. My Password was Password1

![image](https://github.com/user-attachments/assets/06c92d06-311c-45a5-9597-08deb706cd95)

You should see the user in the admins group. Lets make it an admin. Right click and select properties for the user

![image](https://github.com/user-attachments/assets/117249ea-0591-48e4-93ab-e9fa285feb26)

Select the Members of tab

![image](https://github.com/user-attachments/assets/dc7b7a3e-eb07-468a-b0c2-dca682102a87)

Select the Add button


Enter Domain Admins in the Object names box then check names. It should be highlighted the picture below

![image](https://github.com/user-attachments/assets/276e6f58-ac68-4dc1-bee7-b24519c9a0d0)

Select OK, you should then see that the User is a part of the Domain Admins. Apply then select OK.
You can test this by signing out of the Domain Controller and logging on with the newly created account. When signing in, select the other user option to specify your account

![image](https://github.com/user-attachments/assets/868d9baf-6a57-4a36-9cd1-1ddbb1f58402)

<h2>Configuring Remote Access Storage and Network Address Translation</h2>

Select Add Roles and Features

![image](https://github.com/user-attachments/assets/0f8ce149-e6d2-489d-be6f-df017bfe8570)

Select Next, select your server once again, select the checkbox for the Remote Access(it may say RAS connection Manager Administration Kit)

![image](https://github.com/user-attachments/assets/5ebc2d0b-9692-4eed-8b58-fb82f8f81dbd)

Select Routing, the Add Features checkbox may come up. If so, select the Add features

![image](https://github.com/user-attachments/assets/838a3365-af76-4cbc-b7fc-8d3719840d12)

![image](https://github.com/user-attachments/assets/507a98b6-6ed2-4b0b-b9d3-8382df4a2e1d)

Continously click Next until you get to the install. Complete the install

Afterwards select the Tools in the Top right corner then selecting Routing and Remote Access

![image](https://github.com/user-attachments/assets/1672b837-9250-448b-962f-528061823108)


Right click your domain controller then select the Configure and Enable Routing and Remote Access

![image](https://github.com/user-attachments/assets/f297f5e8-bd49-42b7-8b4b-240b76b7a3c5)


Once it opens select next, then select the "NAT" option

![image](https://github.com/user-attachments/assets/02e80641-f72a-450b-a562-80f77cc53743)

On the following page, we are looking to make use of our defined interfaces. If the Network interfaces are not populated in the box, select cancel and reselect the routing and remote access again

![image](https://github.com/user-attachments/assets/9183e3e6-7e64-4513-a9c6-7963d1379b30)

Select the Internet interface to connect to the Internet

![image](https://github.com/user-attachments/assets/eb2cc23e-7329-415b-9300-c3b7afe188b8)

Select Next, then select Finsh

Once done it should look like this:

![image](https://github.com/user-attachments/assets/1eb32035-4596-4244-80a4-31087bb03b7b)

<h2>Setup DHCP Server</h2>

This will allow our clients to get a dhcp ip to browse the internet. As shown in the diagram, this will be a function of the domain controller

<img src="https://i.imgur.com/Gwgffdz.png" height="80%" width="80%" alt="Active Directory Topology"/>

Select the Add Roles and Features, continuously select Next. Select the DHCP Server option, then select the Add Features in the box that pops up

![image](https://github.com/user-attachments/assets/91695f7e-bf1f-49e2-ad87-a1b5f89af65a)

![image](https://github.com/user-attachments/assets/0484689b-ba64-474e-bb7e-04e0a8dbccaa)


Proceed with the Install

![image](https://github.com/user-attachments/assets/a1e9cd6a-e9a6-4b6d-be01-42dbf6d3af65)


Once the installation Is finshed, select the tools in the right corner then select DHCP. The screen should look like this

![image](https://github.com/user-attachments/assets/5053726c-4f75-49a8-a9f5-f84b872e6207)


Expand the drop-down arrow, then right click the ipv4 option and select New scope

![image](https://github.com/user-attachments/assets/05708a1a-874f-4a9c-b017-7b8ce38348eb)

Click Next
We're going to define the scope now. Specify these IP address ranges

![image](https://github.com/user-attachments/assets/44464505-05c9-46cf-b92c-03585271f874)

No need for any exclusions

![image](https://github.com/user-attachments/assets/6c9ac519-b3c0-43b9-a42e-b0fd04c7b34a)

Define number of days for lease

![image](https://github.com/user-attachments/assets/128c7732-c731-4f7b-92a3-46e548708d3d)

Yes we want to configure options so the clients know where to go

![image](https://github.com/user-attachments/assets/85663a23-c285-4355-b6d4-7cf6d2ae0866)


Specify the IP of the Default gateway as your IP

![image](https://github.com/user-attachments/assets/a8153337-c534-437b-93e3-fd735af90079)

Specify the Domain's Internal NIC as your DNS Server. Enter it in the IP address field and select Add

![image](https://github.com/user-attachments/assets/98b7e487-9f57-4b0e-9234-287b4cf1ae06)

Select Next and select finish

Once back at the dhcp menu, right click the dhcp server name and click authorize

![image](https://github.com/user-attachments/assets/aeb7319a-2a2f-40c9-b310-1e8e9a1be13b)

After authorizing, right click the same menu again and click refresh. The Ip addresses should turn green

![image](https://github.com/user-attachments/assets/70f35dd9-869d-451d-95c9-4884e165a76f)

Go back to dashboard and select configure this local server

![image](https://github.com/user-attachments/assets/5375d5e7-811f-42b7-8fa2-8c7a0f996d69)

Selec the IE Enhanced Security Configuraton 

![image](https://github.com/user-attachments/assets/8ff7b83b-5c83-46d9-9f64-38d576b02069)

Turn it off for users and administrators

![image](https://github.com/user-attachments/assets/b81bc327-9561-474f-9775-d96fc1ac84f6)

<h2> Create a large number of users </h2>

Download a script and accompanying files that can create many users. 

In the notepad with the names, Add your name to the very top

![image](https://github.com/user-attachments/assets/f44f1c26-36fb-48dd-bbfb-388494096011)


Open Windows Powershell ISE as an administrator

![image](https://github.com/user-attachments/assets/bd3f917c-5a1d-4a5b-aee9-d77a4e49aab8)


Set the execution policy to unrestricted to execute script

![image](https://github.com/user-attachments/assets/15b905ff-0cec-4e27-b210-87d7c4f2a7b0)


A Warning will pop up, say Yes to all

![image](https://github.com/user-attachments/assets/02472e71-1875-4d11-8b56-75b2b4ac6464)


We can open the Active Directory Users to see the current Organizational Units in the defined Domain

![image](https://github.com/user-attachments/assets/a65a522d-44a8-4d41-96f1-f935d1828d0d)

Observe the Organizational units that are currently present

![image](https://github.com/user-attachments/assets/bdf3904f-985e-49ab-a741-bde8f61e4c10)


Back to Powershell, cd to the location of the script, I'm currently logged in as my administrator personal account

cd C:\Users\a-obankole\Desktop\AD_PS-master

![image](https://github.com/user-attachments/assets/c2865084-bfef-4e06-98ae-347e4a3d30da)


Run ls to verify we are in the right directory

![image](https://github.com/user-attachments/assets/b0965fa9-e5cf-4e20-8ac0-03f934067b43)


Select the play button to run the script:

![image](https://github.com/user-attachments/assets/80582838-5d22-487f-98af-e70ac1147d2b)


A Warning will appear, Select the Run Once option

![image](https://github.com/user-attachments/assets/02d3215e-68fa-4218-a45c-4bb737b0fa0f)


The Script will run for some time but you should see the following on your screen

![image](https://github.com/user-attachments/assets/d32f3ea6-fc0b-47c0-b812-262fe6f79796)


Verify that the _USERS organizational unit has been created and there are users(You may need to right click your domain and select refresh)

![image](https://github.com/user-attachments/assets/50bd9099-9a1a-424b-97e1-34b789a88b59)


You can even search for yourself by doing a find

![image](https://github.com/user-attachments/assets/17f08fa2-fe34-4b19-8c3a-6bb6b0eafc94)


![image](https://github.com/user-attachments/assets/fe557b1c-0644-43e8-aa6f-4f81ca5ee4b8)

<h2>Create the Windows Client VM</h2>

Select New from VirtualBox

Specify the VM name, Microsoft windows and Windows10

![image](https://github.com/user-attachments/assets/b00f9a52-4b43-4ae5-a363-8beaa44d323a)


Allocate enough RAM and Processors

![image](https://github.com/user-attachments/assets/a2cb49ea-dd35-4510-b3ba-217ef0cc30ca)


Allocate enough disk space

![image](https://github.com/user-attachments/assets/e81c2ae9-3288-4f0a-9a75-79ca3beee655)


Finish

![image](https://github.com/user-attachments/assets/6acc93ac-c8fe-4c28-9687-8380eea61f51)


Go into the settings of the Client1

![image](https://github.com/user-attachments/assets/029dac67-922c-4122-8113-32b0cf4fe4ae)


Go to Advanced and change the shared clipoard and drag'n'drop settings

![image](https://github.com/user-attachments/assets/75bcd3c7-6e0e-4ee1-9f67-412e5e6388f5)


Go to Network and change the Adapter to the Internal Network

![image](https://github.com/user-attachments/assets/7173ee10-f2cf-402e-8067-15c708f4eb85)


After this click ok.

Doubleclick the Client1 and you should see this screen

![image](https://github.com/user-attachments/assets/69195bdd-a35d-4cad-b99d-5fb47bac43f9)


Add the windows 10 ISO that was previously downloaded

![image](https://github.com/user-attachments/assets/1bff3e89-3f03-457d-bdc4-60f03bac7a99)


Select the mount and retry boot

You should be met with this screen:

![image](https://github.com/user-attachments/assets/18726728-a4d5-489d-b97a-14ed4546bd3b)


Select Next then select Install now

![image](https://github.com/user-attachments/assets/8d7ba996-74ed-4696-a306-58b98a7286ca)


Select the "I don't have a Product Key"

![image](https://github.com/user-attachments/assets/871db461-0e3c-45e3-8ad0-dcd097b912ae)


Choose Windows 10 Pro

![image](https://github.com/user-attachments/assets/ad709769-4ccc-4efe-b4ef-fcba0d4a8bbd)

Accept the terms and agreement. Select the Custom Install of windows

![image](https://github.com/user-attachments/assets/40b2f389-f984-4c61-a98f-02c27049241b)

Select next( We don't need to format an already empty drive)
![image](https://github.com/user-attachments/assets/7a854db9-a3ad-4b94-9017-28e974ff83d9)


Begin the installation, this will take some time:

![image](https://github.com/user-attachments/assets/93a3557d-a091-4f2d-8660-77de6be85977)

Select the proper region:
![image](https://github.com/user-attachments/assets/18997c9a-80cb-46f2-b0e5-cd5014b07811)


Select the right keyboard layout and proceed accoridngly

Select the "Setup for personal use"
![image](https://github.com/user-attachments/assets/c2dc3e76-ab8c-4dff-ba26-f10843375492)


Select the Limited experience, if it asks you to make an email you can select offline mode
![image](https://github.com/user-attachments/assets/86c1f7d1-2c0d-438f-bbf6-8697f2a22121)


Once here, create the username 
![image](https://github.com/user-attachments/assets/ee94a46f-d490-4212-86f6-c2d6d15eccb2)

No Password needed
So click next
![image](https://github.com/user-attachments/assets/21b7628e-f113-4b79-8f86-091c251076c7)


Turn all of these off

![image](https://github.com/user-attachments/assets/399497e9-a804-4c30-b98f-9ec82dddd855)


We are pretty much just proceeding through the workflow. Skipping and not accepting anything.



Once it boots up, select the Start menu and open command prompt
![image](https://github.com/user-attachments/assets/90c0bd4f-8242-4eda-8bbb-d1cd0dd3fecd)

Enter ipconfig to confirm what the gateway IP is and that we recieved an IP via DHCP
![image](https://github.com/user-attachments/assets/62d4023d-0820-4554-ac2c-56811d2857bb)

Looking at ipconfig \all you can see more information regarding the hostname and configured IP address
![image](https://github.com/user-attachments/assets/9c48e738-169c-4f3c-9868-9fb0ac449e15)


Going back to the dhcp settings on the Domain Controller, we see the lease for our device in question
![image](https://github.com/user-attachments/assets/48ffa6dc-6d0d-4811-b5f5-039ddf8eef4a)

From the computer we can ping different resources such as google or the defined domain
![image](https://github.com/user-attachments/assets/8e304b97-f2ef-40a6-b0a4-f0c685971c55)

<h2>Rename the Client Hostname</h2>

Right click the menu and press system. Scroll down and choose the advanced option to rename this PC
![image](https://github.com/user-attachments/assets/a7689e5d-7f26-4cad-8f84-0dedc77afc0c)


Select the Change button on the pop-up then change the compute name and the Domain
![image](https://github.com/user-attachments/assets/44551455-685e-40e6-bfa4-bab4066bd0d4)

Login with your domain account

![image](https://github.com/user-attachments/assets/f2e32428-1a7e-4088-aac3-b99b7b5d097e)


You should be met with the following:

![image](https://github.com/user-attachments/assets/80d23093-42ea-43a0-9b25-97c93debdfbb)


It will ask you to restart after selecting ok, continue with restart


Looking back at the DHCP leases in our domain controller, we can see the newly specified name on the proper domain
![image](https://github.com/user-attachments/assets/73f34e19-873a-4fe8-a140-17e78ddb610a)


Looking at computers in the Active Directory Users and computers
![image](https://github.com/user-attachments/assets/f4f132c0-8adb-4f34-8c23-83977b21a3bd)




At this point and we are done












