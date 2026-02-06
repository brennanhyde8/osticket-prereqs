<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)

<h2>List of Prerequisites</h2>

- Item 1
- Item 2
- Item 3
- Item 4
- Item 5

<h2>Installation Steps</h2>

<p>
<img width="2543" height="1452" alt="Screenshot 2026-02-06 161151" src="https://github.com/user-attachments/assets/1c2782d4-ad9e-4384-86f7-7c92a0cd3138" />
</p>
<p>
<img width="2536" height="1460" alt="Screenshot 2026-02-06 161451" src="https://github.com/user-attachments/assets/d6ea7480-3147-4e88-ba1c-6eebf8ba7917" />
</p>

**Basics step – osTicket Virtual Machine (Azure)**

In the "Basics" step, you define the core settings for the virtual machine that will host the osTicket help desk system. This includes selecting the Azure subscription and resource group, assigning a name to the VM, choosing the region, and selecting a supported operating system image (such as Ubuntu Server or Windows Server). You also choose the VM size based on expected workload and configure the administrator account and authentication method. These settings establish the identity, location, and initial access configuration for the osTicket server before networking, storage, and security options are configured.

</p>
<br />
<img width="2534" height="1398" alt="Screenshot 2026-02-06 161513" src="https://github.com/user-attachments/assets/5222895f-79a9-4459-9624-be151adfeec8" />
<p>
</p>
<p>
  
**Networking step – osTicket Virtual Machine (Azure)**

In the "Networking" step, you configure how the osTicket virtual machine connects to the network and how users and administrators will access it. This includes selecting or creating a virtual network and subnet, assigning a public IP address if the osTicket web interface must be reachable from the internet, and configuring network security group (NSG) rules to allow only required traffic (such as HTTP/HTTPS for users and SSH or RDP for administrators). Proper networking configuration ensures the osTicket server is accessible, secure, and correctly integrated into the Azure environment.

</p>
<br />

<p>
<img width="2533" height="1400" alt="Screenshot 2026-02-06 161545" src="https://github.com/user-attachments/assets/09545d8e-17e4-4b00-a03f-3ceeb21fa836" />
</p>
<p>
**Review + Create step – osTicket Virtual Machine (Azure)**

In the "Review + Create" step, you verify all selected settings for the osTicket virtual machine, including the subscription, resource group, virtual machine size, operating system, networking configuration, and security rules required to access the osTicket web application and manage the server. Azure runs a validation check to ensure the configuration is correct and complete. Once validation passes, selecting "Create" deploys the virtual machine and the required Azure resources so the server can be prepared for installing and running osTicket.

</p>
<br />

<p>
<img width="850" height="509" alt="Screenshot RD" src="https://github.com/user-attachments/assets/2afe0936-b0e6-46e6-9f3d-861910109c6c" />
</p>
<p>
**Deploying the virtual machine using Remote Desktop**

Deploying the virtual machine using Remote Desktop involves connecting to the newly created Azure virtual machine through the Remote Desktop Protocol (RDP) to perform post-deployment setup and configuration. After establishing the Remote Desktop connection, the administrator verifies the operating system, applies updates, and prepares the server environment for its intended role (such as hosting osTicket). This step ensures the virtual machine is accessible, properly configured, and ready for application installation and management through a remote administrative session.

</p>
<br />

<p>
<img width="850" height="509" alt="Screenshot RD2" src="https://github.com/user-attachments/assets/2aaba9bc-bcfc-4bfc-975f-dfff0b3a6ea3" />
</p>
<p>
**Downloading the osTicket installation file**

Downloading the osTicket installation file involves accessing the official osTicket website from the virtual machine and obtaining the latest stable release of the osTicket software package. The installation file is saved to the virtual machine so it can be extracted and used by the web server during setup. This step ensures that the correct and up-to-date osTicket files are available for installation and configuration on the server.

</p>
<br /p>

<p>
<img width="850" height="509" alt="Screenshot RD3" src="https://github.com/user-attachments/assets/ee5df8c4-467c-4dc0-85a0-fb28c441f02c" />
</p>
<p>
Here is a more formal, documentation-ready version:

**Extracting the osTicket Installation File**

Once the osTicket installation package has been downloaded to the virtual machine, the compressed archive must be extracted to access the application files. Navigate to the download location, right-click the osTicket `.zip` file, and select **Extract All**. Specify a destination folder and complete the extraction process. The extracted directory contains all necessary osTicket installation files, which will be used in subsequent steps to deploy and configure the application on the web server.

</p>
<br /p>
