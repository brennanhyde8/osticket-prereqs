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
---

## Creating the Azure Virtual Machine for osTicket

This section documents the creation of a Windows Virtual Machine in Microsoft Azure to host the osTicket help desk application. The virtual machine provides the compute environment required to install IIS, PHP, MySQL, and osTicket.

---

### Virtual Machine Setup

1. Navigate to **Virtual Machines** and select **Create**.
2. Choose **Azure virtual machine**.

---

### Basics Configuration

<p>
<img width="2542" height="1458" alt="Screenshot 2026-02-10 190809" src="https://github.com/user-attachments/assets/3b0d35d4-4841-4a03-bda4-a989b91bbfe0" />
</p>

* Select the previously created resource group
* Name the virtual machine `osticket-vm`
* Choose the same region as the resource group
* Select a Windows Server 2019/2022 or Windows 10/11 image
* Choose a size with at least 2 vCPUs and 4 GB of memory
* Set authentication to username and password
* Create administrator credentials

---

### Networking Configuration

<p>
<img width="2542" height="1463" alt="Screenshot 2026-02-10 191112" src="https://github.com/user-attachments/assets/a9e45507-2f70-46f0-b2bd-7b460e0c31e6" />
</p>

1. Select or create a virtual network and subnet.
2. Assign a public IP address to the virtual machine.
3. Configure the network security group to allow inbound traffic for:

   * Remote Desktop Protocol on TCP port 3389
   * HTTP traffic on TCP port 80
   * HTTPS traffic on TCP port 443 (optional but recommended)

---

### Review and Deployment

<p>
<img width="2554" height="1462" alt="Screenshot 2026-02-10 191155" src="https://github.com/user-attachments/assets/83d613ad-f310-407c-b01b-39df6b11123b" />
</p>

1. Review all configuration settings.
2. Select **Review + Create**.
3. Click **Create** to deploy the virtual machine.

The deployment process may take several minutes to complete.

---

Once connectivity is confirmed, the virtual machine is ready for osTicket prerequisite installation and configuration.

---

# osTicket Deployment on Windows Azure VM (IIS + PHP + MySQL)

This guide documents the installation of **osTicket** on a Windows virtual machine hosted in Azure. The process includes configuring IIS, installing required dependencies, and completing the osTicket web-based setup using Remote Desktop.

---

## 1. Access the Virtual Machine

* Connect to the Azure virtual machine (`osticket-vm`) using **Remote Desktop**
* All configuration and installation tasks are performed within the VM

---

## 2. Obtain Installation Files

1. Within the VM, download **osTicket-Installation-Files.zip**
2. Extract the archive to the **Desktop**
3. Verify the extracted directory is named:

   ```
   osTicket-Installation-Files
   ```

This directory contains osTicket and all necessary supporting installers.

---

## 3. Enable Internet Information Services (IIS)

1. Open **Windows Features**
2. Enable **Internet Information Services**
3. Navigate to:

   ```
   World Wide Web Services → Application Development Features
   ```
4. Enable:

   ```
   CGI
   ```
5. Apply the changes and allow Windows to complete setup

---

## 4. Install IIS Components

From the **osTicket-Installation-Files** directory, install:

* **PHP Manager for IIS**

  ```
  PHPManagerForIIS_V1.5.0.msi
  ```
* **IIS URL Rewrite Module**

  ```
  rewrite_amd64_en-US.msi
  ```

---

## 5. Install and Configure PHP

1. Create the following directory:

   ```
   C:\PHP
   ```
2. Extract:

   ```
   php-7.3.8-nts-Win32-VC15-x86.zip
   ```

   into the `C:\PHP` directory
3. Install the required runtime:

   ```
   VC_redist.x86.exe
   ```

---

## 6. Install MySQL Server

1. Run:

   ```
   mysql-5.5.62-win32.msi
   ```
2. Choose **Typical Installation**
3. Launch the **Configuration Wizard**
4. Select **Standard Configuration**
5. Set credentials:

   ```
   Username: root
   Password: root
   ```

---

## 7. Register PHP with IIS

1. Launch **IIS Manager** as an administrator
2. Open **PHP Manager**
3. Register the PHP executable:

   ```
   C:\PHP\php-cgi.exe
   ```
4. Restart IIS by stopping and starting the server

---

## 8. Deploy osTicket Application Files

1. Extract:

   ```
   osTicket-v1.15.8.zip
   ```
2. Copy the **upload** directory to:

   ```
   C:\inetpub\wwwroot
   ```
3. Rename the folder:

   ```
   upload → osTicket
   ```
4. Restart IIS to apply changes

---

## 9. Launch the Installer

1. In IIS Manager, navigate to:

   ```
   Sites → Default Web Site → osTicket
   ```
2. Click **Browse *:80** to open the installer page

---

## 10. Enable Required PHP Extensions

1. In IIS, open **PHP Manager** for the osTicket site
2. Select **Enable or disable an extension**
3. Enable the following:

   ```
   php_imap.dll
   php_intl.dll
   php_opcache.dll
   ```
4. Refresh the installer page to confirm changes

---

## 11. Prepare osTicket Configuration File

### Rename the Configuration File

```
C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
→
C:\inetpub\wwwroot\osTicket\include\ost-config.php
```

### Adjust Permissions

1. Disable inherited permissions
2. Remove existing entries
3. Add:

   ```
   Everyone → Full Control
   ```

---

## 12. Complete Initial Setup in Browser

* Click **Continue**
* Specify the help desk name
* Configure the default system email address

---

## 13. Create the osTicket Database

1. Install **HeidiSQL**
2. Launch HeidiSQL
3. Create a new session using:

   ```
   Username: root
   Password: root
   ```
4. Connect and create a database named:

   ```
   osTicket
   ```

---

## 14. Finish Installation

In the osTicket installer:

```
Database Name: osTicket
Database User: root
Database Password: root
```

Click **Install Now** to complete setup.

---

## 15. Access the Application

### Administrator Portal

```
http://localhost/osTicket/scp/login.php
```

### End User Portal

```
http://localhost/osTicket/
```

---

## 16. Secure the Installation

1. Remove the setup directory:

   ```
   C:\inetpub\wwwroot\osTicket\setup
   ```
2. Change permissions on:

   ```
   C:\inetpub\wwwroot\osTicket\include\ost-config.php
   ```

   to **Read-only**

---

## 🎉 Deployment Complete

osTicket is now fully operational on a Windows Azure VM, configured with IIS, PHP, and MySQL, and ready for help desk use.

---

If you want, I can also:

* Rewrite it **even more concise**
* Convert it into a **resume project summary**
* Add a **troubleshooting appendix**
* Turn it into a **YouTube narration script**

Just say what’s next 🚀
