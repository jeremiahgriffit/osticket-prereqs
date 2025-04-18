<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- PHP Manager for IIS
- MySQL Database
- osTicket (latest stable release)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Microsoft Azure Subscription
- Windows 10 Virtual Machine (with IIS enabled)
- PHP Manager for IIS
- MySQL Database (v5.7+ recommended)
- osTicket Installaton Files (download from official site)

<h2>Installation Steps</h2>

<p>
<img src="https://private-user-images.githubusercontent.com/200851135/423409820-1d4105aa-bc08-4686-8647-c13eaf6a5969.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDQ5OTE2ODcsIm5iZiI6MTc0NDk5MTM4NywicGF0aCI6Ii8yMDA4NTExMzUvNDIzNDA5ODIwLTFkNDEwNWFhLWJjMDgtNDY4Ni04NjQ3LWMxM2VhZjZhNTk2OS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOFQxNTQ5NDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wZDg3ZjNjYmFhYWYxNzc4M2Y0OGUwMmU2YzZiNjkyZmZmZjAwNmJkODRjYzg5ZjY5M2Q1YTVmYTUyNzk4NWRmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.seeZVaqmWTVnyniqH22KofIsWUygkB7FGeu9h_OwU4A" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To start the process of installing osTicket on a Windows 10 virtual machine, create a VM in Microsoft Azure, create a VM is operational, connect to it using RDP and confirm that the system is completely up to date. Now open "Turn Windows Features On or Off" and find Internet Information Services (IIS) in the list. Select it and enable it, along with a feature called CGI, which is necessary for osTicket to function properly. Next, download to the server and install PHP Manager for IIS. After installing it, you'll need to configure PHP itself. It's highly recommended that you use version 7.3 or higher when doing this.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, grab the latest stable version of osTicket from the official website and download it. Extract the files into the C:\inetpub\wwwroot\osTicket folder. You will find a file named ost-config.php.sample in that folder. Rename it to ost-config.php. You will also need to find a command line interface, MySQL Workbench, or some other way to execute MySQL commands to perform the next steps. Create a new database named osticket. Then create a new MySQL user who has full privileges to that database. You can use the following example commands to create the user and set privileges. (The commands should all be executed inside MySQL Workbench or the command line interface.)
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the last stage, go to a browser and enter the following URL: http://<your_vm_ip>/osTicket. You should see the web installer for osTicket. The installer will ask for some required information, such as your Helpdesk Name, Admin Username, Email, and MySQL database credentials. Remember to input the database name, user, and password that you set up earlier. After hitting "Install Now," the server will do its thing and configure osTicket. That might take a minute or two. Once it's done, the installer will instruct you to remove the /setup directory for security purposes before you can finally log into the admin dashboard for osTicket and start using your help desk.
</p>
<br />
