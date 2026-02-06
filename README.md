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
osTicket Deployment via Remote Desktop
Phase 1: Prerequisites & Environment Setup
  
**Overview**

This project documents the preparation of a Windows-based virtual machine environment for deploying osTicket. All prerequisite services and configurations were completed using Remote Desktop access to ensure a functional and secure installation environment.

**Prerequisites Setup**

**Virtual Machine Configuration**
<p>
<img width="2543" height="1452" alt="Screenshot 2026-02-06 161151" src="https://github.com/user-attachments/assets/8539d908-3388-4bf7-b118-18d1a74b6b39" />
</p>
<p>
<img width="2534" height="1398" alt="Screenshot 2026-02-06 161513" src="https://github.com/user-attachments/assets/8a272573-7420-4de6-a26e-d947a0ee18b4" />
</p>
<p>
<img width="2533" height="1400" alt="Screenshot 2026-02-06 161545" src="https://github.com/user-attachments/assets/730c39de-6dde-4a65-a45e-4b8ae9ead06e" />
</p>

<br /p>

A Windows Server virtual machine was provisioned in Microsoft Azure with sufficient compute, memory, and storage resources to support a web application and database backend. Administrative credentials and networking settings were configured during deployment.

**Remote Desktop Access**

Remote Desktop Protocol (RDP) was enabled to allow administrative access to the virtual machine. A successful RDP connection was established using the VM’s public IP address.

**Web Server (IIS)**

Internet Information Services (IIS) was installed and configured to host osTicket. Required features, including CGI support, were enabled to allow PHP execution.

**PHP Configuration**

PHP was installed and integrated with IIS. Required PHP extensions were enabled to ensure compatibility with osTicket functionality.

**Database Setup (MySQL)**

MySQL was installed as the database backend. A dedicated osTicket database and user account were created with appropriate permissions.

**Networking & Security**

Inbound firewall and network security rules were configured to allow web traffic over HTTP (port 80) and HTTPS (port 443, if applicable).

**File System Preparation**

Directory permissions were configured to allow IIS to read and write required osTicket files.

**osTicket Installation Files**

The osTicket installation package was downloaded and extracted, preparing the application files for placement in the web server’s root directory.

**Status**

✔ Environment fully prepared and ready for osTicket deployment
