# OS Ticket Prerequisites & Installation

In this lab we will be setting up the prerequisites and installing an open source ticketing system called "osTicket"  
The Objective of these labs is to gain understanding of ticketing systems and how they work  

All the necessary files can be found [here](https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Virtual Machines
- MySQL

<h2>Operating Systems Used </h2> 

- Windows 10 Pro, version 22H2 - x64 Gen2

## Configuration Steps
1. Create an Azure Virtual Machine
2. Connect to the VM
3. Install IIS with CGI
4. Install dependencies
5. Register PHP with IIS manager
6. Load osTicket configuration file
7. Configure file permissions
8. Install & configure HeidiSQL
9. Finalize osTicket installation 

<h2>Deployment and Configuration Steps</h2> 

### Create an Azure Virtual Machine

We will Create a Windows 10 VM with 4vCPUs  

Click on "Create"  


![Pasted image 20250313050651](https://github.com/user-attachments/assets/1d4105aa-bc08-4686-8647-c13eaf6a5969)

Configure the following in the highlighted areas in the picture below:

| Selection             | Configuration                           |
| --------------------- | --------------------------------------- |
| Resource group:       | OSTicket                                |
| Virtual machine name: | OSTicket-vm                             |
| Region                | I chose US east                         |
| Image:                | Windows 10 Pro, version 22H2 - x64 Gen2 |
| Size:                 | Standard_D2s_v3 - 2 vcpus, 8 GiB memory |
| Username              | LabADMIN                                |
| Password              | osTicketPassword123!                    |


Be sure to check "*I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights.*"  

Create the VM:  

![10](https://github.com/user-attachments/assets/5d03385e-0fb9-4922-b32a-2ad397e2abee)


### Connect to  the VM:

Username: `LabADMIN`  
Password: `osTicketPassword123!`  

![3](https://github.com/user-attachments/assets/1a569a50-301f-4ee2-9b79-a3a7845c4b97)


### Installing IIS with CGI

Next we will be installing and enabling IIS (Internet Information Services) with CGI
To do this navigate to the Control Panel

![4png](https://github.com/user-attachments/assets/90104521-dc56-4535-907e-f8c07cdd294e)


 Click on Programs> Turn Windows Features On or Off

![Pasted image 20250313054637](https://github.com/user-attachments/assets/bef5dc7f-2b55-44a1-aa56-a34f9981a120)

 Tick Internet Information Services box
 
 Navigate to World Wide Web Services> Application Development Features and tick CGI box


![Pasted image 20250313055122](https://github.com/user-attachments/assets/91c784cd-8458-4ee9-837a-fdd02a5a5047)

### Verify IIS has been installed

Navigate to the web browser and type http://127.0.0.1/ you should see this screen:

*This address is the loopback address we have created a website hosted on the internal loopback address*

![Pasted image 20250313055435](https://github.com/user-attachments/assets/ba2a6cd2-f5f0-438a-8e61-1e3ded145c6a)

### Installing dependencies

#### Install PHP manager for IIS

All the necessary files can be found [here](https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0) open this link within the VM and download the files and unzip them to the desktop

Install PHPManagerForllS_V1.5.O

*Click through all prompts as necessary*

![Pasted image 20250313060044](https://github.com/user-attachments/assets/1f601558-2794-4e95-8e5a-2333ea9c5d51)


![Pasted image 20250313060632](https://github.com/user-attachments/assets/38be9458-e5e0-4593-a5a2-895086ace18f)


#### Install "rewrite_amd64_en-US"

Next install "rewrite_amd64_en-US"

*Click through all prompts as necessary*

![Pasted image 20250313060742](https://github.com/user-attachments/assets/7e9761ef-f153-47b6-b4c9-49dc3da6401e)


![Pasted image 20250313060853](https://github.com/user-attachments/assets/4c373444-0c95-415c-af3a-4c6db683518f)


#### Create a directory on C drive named PHP

Navigate to `C:` > Create a folder named `PHP`

![Pasted image 20250313061042](https://github.com/user-attachments/assets/2342c8c5-465d-4036-a74d-cc56d2126003)


unzip the contents  of "php-7.3.8-nts-Win32-VC15-x86" into the directory we just created

![Pasted image 20250313061247](https://github.com/user-attachments/assets/b103520b-4200-4010-a955-77257af04b97)


PHP folder will look like this after: 
![Pasted image 20250313061418](https://github.com/user-attachments/assets/265b14b8-6c2f-471b-977a-3c78091a41c5)


#### Next install "VC_redist.x86"

Next install "VC_redist.x86"

Click through all prompts as necessary

![Pasted image 20250313061526](https://github.com/user-attachments/assets/b7a9318e-853b-4f88-97bb-8e266adfb30d)


![Pasted image 20250313061607](https://github.com/user-attachments/assets/250742ef-1d53-48fd-82a9-ed6d32ff4636)


#### Install "mysql-5.5.62-win32"

![Pasted image 20250313061704](https://github.com/user-attachments/assets/49e29025-6af7-474b-bb75-a029ba8fb0b9)


When you get to this screen choose "Typical" and install

![Pasted image 20250313061800](https://github.com/user-attachments/assets/5912623a-4f81-468f-bf29-88af1f50b2b7)


Tick "launch the MySQL Instance Configuration Wizard" and click finish

![Pasted image 20250313061846](https://github.com/user-attachments/assets/27794559-d6b7-440b-a7f2-f96c35408496)


Click "Standard Configuration"

![Pasted image 20250313062105](https://github.com/user-attachments/assets/38c2eb11-c504-47aa-ba0e-9a1ca7a3586f)


Configure root password as: `osTicketPassword123!`  

![Pasted image 20250313062301](https://github.com/user-attachments/assets/e2dbc651-fa99-41a6-b5bd-17f6a5bbc1ab)

#### Register PHP with IIS manager

Open IIS manager run as admin

![7](https://github.com/user-attachments/assets/dbbb7338-4e8d-4561-b012-41b13c7c77f9)


Click on "PHP manager"  

![Pasted image 20250313063120](https://github.com/user-attachments/assets/a8e27bbd-e1a5-4616-9f09-6a237d814bb7)


Click on "Register new PHP version"

![Pasted image 20250313063207](https://github.com/user-attachments/assets/65830c14-0678-414a-b736-c148f31a598f)


Next configure the path `C:\PHP\php-cgi.exe` and click ok 

![Pasted image 20250313063329](https://github.com/user-attachments/assets/98a41d33-57a8-4db2-bba8-912a05b5802e)



Restart IIS for the change to take effect

![Pasted image 20250313063523](https://github.com/user-attachments/assets/6747c5af-857a-4969-bb14-226e9e172e7a)


### Install OSTicket v1.15.8

Extract the zipped files 

![Pasted image 20250313063721](https://github.com/user-attachments/assets/fc83dd23-2df6-481d-b21f-855701fc5064)


It should look like this:

![Pasted image 20250313064213](https://github.com/user-attachments/assets/a6b06ecb-e13a-41a0-9758-a50b33c38086)



Copy the "upload folder" to `c:\inetpub\wwwroot` then rename "upload" to `osTicket`

![Pasted image 20250313064325](https://github.com/user-attachments/assets/0087caa8-69bc-46cc-a77b-4386cf9ab208)

Restart IIS for the change to take effect

![Pasted image 20250313063523](https://github.com/user-attachments/assets/b9d062d6-05c8-49ab-ac62-e0e83c2d3b8e)


On IIS go to osticket and then click "Browse"

![Pasted image 20250313064808](https://github.com/user-attachments/assets/6f14c1fd-4989-45c2-9deb-89ce80774bef)


You should be met with the osTicket installer: 

As you can see by the red Xs we still have a bit more to configure 

![Pasted image 20250313064852](https://github.com/user-attachments/assets/8d2ee7ab-ee48-4922-80ef-2ea11d59ce36)

#### Enable PHP Extensions

Go back to IIS and Select osTicket > PHP Manager   

![Pasted image 20250313165524](https://github.com/user-attachments/assets/6238347a-fae4-4f8c-885e-57602f6a9f99)


Click on "Enable or disable an extension"

![Pasted image 20250313165618](https://github.com/user-attachments/assets/7eb1e3e3-a9d6-4db9-9fda-59bdddfd78a7)


Right click > enable on the following .dll files
- php_imap.dll
- php_intl.dll
- php_opcache.dll

![Pasted image 20250313165936](https://github.com/user-attachments/assets/29fdc3b8-4cff-4062-920e-991b3a3d9216)


Once your done it should look like this:

![Pasted image 20250313170211](https://github.com/user-attachments/assets/5e26433f-859a-48ae-a20b-67ae42ef67ff)


Now we can go back to our web browser and refresh to see if the changes updated

The two red Xs remaining are not necessary for osTicket to function properly for our purposes we wont be enabling them

It should look like this:

![Pasted image 20250313170707](https://github.com/user-attachments/assets/58e5268a-638c-4012-b06d-9f33f8669f31)



#### Rename `ost-sampleconfig.php`

Next we will navigate to: `C:\inetpub\wwwroot\osTicket\include` 
Rename`ost-sampleconfig.php`to `ost-config.php`

![Pasted image 20250313171115](https://github.com/user-attachments/assets/3ce22f25-5663-45e0-893b-9601816d6bf3)

Renamed:

![Pasted image 20250313171148](https://github.com/user-attachments/assets/31d3a47a-a4f6-4be4-9c33-85c9828ca9ec)



#### Assign permissions to `ost-config.php`

Right click on `ost-config.php` and click Properties

![8](https://github.com/user-attachments/assets/4f2261ab-a420-4bd3-9289-2622e7644db3)


Go to the securities tab and click advanced  

![Pasted image 20250313172029](https://github.com/user-attachments/assets/1608fde9-aa19-4c5c-b748-25c16209b8e6)


Click "Disable inheritance" and then click "Remove all inherited permissions from this object."

![Pasted image 20250313172209](https://github.com/user-attachments/assets/076c1728-7972-4578-be90-0db8a2154f1b)


Now we will add new permissions click add and then click "select a principal"

![Pasted image 20250313172441](https://github.com/user-attachments/assets/6381496e-addc-4539-af7d-9abd5ec32e2d)


Now we will add everyone 

>[!CAUTION]
> **This is for lab purposes only and done for brevity this should not be done on a real production environment**  
> *Enabling  permissions for everyone is bad security policy I did this to keep the lab concise* 


![Pasted image 20250313172553](https://github.com/user-attachments/assets/6780b167-ddab-4461-9b1a-f89ed6b58045)


Check "Full control" and then ok 

![Pasted image 20250313172819](https://github.com/user-attachments/assets/48ee9478-e4d7-445b-ab40-8d2abce5db58)


Click apply to finalize 

![Pasted image 20250313172917](https://github.com/user-attachments/assets/54373c1b-cc6e-4d3c-94b0-e9b0d73291b7)


### Next install & Confiure HeidiSQL

![Pasted image 20250313173556](https://github.com/user-attachments/assets/f02d9fcd-e78b-40e5-a8f8-bf70bc5b44aa)


After you finish installing launch HeidiSQL
 
Click "new" then for password:  `osTicketPassword123!`  
Then click "Open"

![Pasted image 20250313173937](https://github.com/user-attachments/assets/e6cc680e-e690-40ce-b646-d4b3190967d8)



Right Click on "Unnamed" > Create new > Database 

![Pasted image 20250313174539](https://github.com/user-attachments/assets/1053301a-252d-459e-8622-c72eca363f0f)


Then name it `osTicket` and Click ok 

Note: You must name it exactly `osTicket` with the T capitalized or the configuration will not work 

![Pasted image 20250313174332](https://github.com/user-attachments/assets/1127e6f9-2b3e-4fc9-aae3-b76c2c7b931e)

### Finalize osTicket installation

Now back on the web browser we will click "continue" to continue the install 

Configure the following sections:

> [!NOTE]
> Configure your own names and email the following is what I configured make sure to fill out all the following selections
>
> Username/Password as well as The MySQL Sections should be the same as mine


| Selection      | Configuration             |
| -------------- | ------------------------- |
| Helpdesk Name  | Rob's Helpdesk            |
| Default Email  | example-email@gmail.com   |
| First Name     | Rob                       |
| Last Name      | Gaughan                   |
| Email Address  | example-email-2@gmail.com |
| Username       | labAdmin                  |
| Password       | osTicketPassword123!      |
| MySQL Database | osTicket                  |
| MySQL Username | root                      |
| MySQL Password | osTicketPassword123!      |



![Pasted image 20250313174959](https://github.com/user-attachments/assets/26e9db14-c5ce-4df4-af2e-5f747e876bf7)



![Pasted image 20250313175410](https://github.com/user-attachments/assets/5fb69155-680a-4eeb-bd74-0b2fdc142108)



Now if we navigate to: http://localhost/osTicket/  

We will be greeted by the customer facing portal 

![Pasted image 20250317053047](https://github.com/user-attachments/assets/405b2548-1748-4df4-8745-c162cba8fd95)



If we navigate to http://localhost/osTicket/scp/login.php  
We will be greeted by the employee/admin login page  
We can use the following credentials to login to the admin portal   

| Selection | Configuration        |
| --------- | -------------------- |
| Username  | labAdmin             |
| Password  | osTicketPassword123! |

![Pasted image 20250317053218](https://github.com/user-attachments/assets/540eda21-9c23-4430-abb7-25ac529a9a95)

Thats it for this lab we have successfully installed osTicket!

In the next lab we will configure different roles within OS ticket as well as configuring SLAs (Service Level Agreements)
