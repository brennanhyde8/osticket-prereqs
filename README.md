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

- mySQL
- HeidiSQL
- PHP
- PHP Manager
- VC Redist
- Rewrite
---

# Creating the Azure Virtual Machine for osTicket

This section documents the creation of a Windows Virtual Machine in Microsoft Azure to host the osTicket help desk application. The virtual machine provides the compute environment required to install IIS, PHP, MySQL, and osTicket.

---

### Virtual Machine Setup

1. Navigate to **Virtual Machines** and select **Create**.
2. Choose **Azure virtual machine**.

---

### Basics Configuration

<p>
<img width="2551" height="1459" alt="Screenshot 2026-02-10 195245" src="https://github.com/user-attachments/assets/36f6faa9-a00f-4b57-a2f0-e5345ae20858" />
</p>

* Select the previously created resource group
* Name the virtual machine "osticket-vm"
* Choose the same region as the resource group
* Select a Windows Server 2019/2022 or Windows 10/11 image
* Choose a size with at least 2 vCPUs and 4 GB of memory
* Set authentication to username and password
* Create administrator credentials

---

### Networking Configuration

<p>
<img width="2548" height="1460" alt="Screenshot 2026-02-10 195345" src="https://github.com/user-attachments/assets/915b46ab-33ba-4b8d-8ed8-84a74b14704c" />
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
<img width="2547" height="1456" alt="Screenshot 2026-02-10 195417" src="https://github.com/user-attachments/assets/c415d80f-bcc1-4edc-a179-54d5efbdca26" />
</p>

1. Review all configuration settings.
2. Select **Review + Create**.
3. Click **Create** to deploy the virtual machine.

The deployment process may take several minutes to complete.


Once connectivity is confirmed, the virtual machine is ready for osTicket prerequisite installation and configuration.

---

# osTicket Deployment on Windows Azure VM (IIS + PHP + MySQL)

This guide documents the installation of **osTicket** on a Windows virtual machine hosted in Azure. The process includes configuring IIS, installing required dependencies, and completing the osTicket web-based setup using Remote Desktop.

---

## 1. Access the Virtual Machine

<p>
<img width="2542" height="1462" alt="Screenshot 2026-02-10 195827" src="https://github.com/user-attachments/assets/c5f9ce58-003b-4cba-a1ec-d11920d10935" />
</p>

* Connect to the Azure virtual machine (osticket-vm) using **Remote Desktop**
* All configuration and installation tasks are performed within the VM

---

## 2. Obtain Installation Files

<p>
<img width="1277" height="770" alt="Screenshot RD5" src="https://github.com/user-attachments/assets/24105e80-2191-4560-848b-91524c20bcce" />
</p>

1. Within the VM, download **osTicket-Installation-Files.zip**
2. Extract the archive to the **Desktop**
3. Verify the extracted directory is named:

   "osticket-Installation-Files"
   ```
This directory contains osTicket and all necessary supporting installers.

---

## 3. Enable Internet Information Services (IIS)

<p>
<img width="1277" height="770" alt="Screenshot RD6" src="https://github.com/user-attachments/assets/527d9dfa-1d9b-4c42-89dd-53fb8a02bacf" />
</p>

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

<p>
<img width="1277" height="770" alt="Screenshot RD7" src="https://github.com/user-attachments/assets/52bec86c-0d7b-49cf-b2e5-b5add40ce3c7" />
</p>

* **PHP Manager for IIS**

  ```
  PHPManagerForIIS_V1.5.0.msi
  ```
<p>
<img width="1277" height="770" alt="Screenshot RD8" src="https://github.com/user-attachments/assets/ea016480-8ecb-4def-9302-b90b23eb3342" />
</p>

* **IIS URL Rewrite Module**

  ```
  rewrite_amd64_en-US.msi
  ```

---

## 5. Install and Configure PHP

<p>
<img width="1277" height="770" alt="Screenshot RD9" src="https://github.com/user-attachments/assets/323a30c9-4a77-455e-af36-68d5da3157d4" />
</p>

1. Create the following directory:

   ```
   C:\PHP
   ```
<p>
<img width="1277" height="770" alt="Screenshot RD10" src="https://github.com/user-attachments/assets/f172df26-9d2e-4238-ad77-bdda7569dd28" />
</p>

2. Extract:

   ```
   php-7.3.8-nts-Win32-VC15-x86.zip
   ```

   into the `C:\PHP` directory
   
   ---
<p>
<img width="1277" height="770" alt="Screenshot RD11" src="https://github.com/user-attachments/assets/0c90f108-065a-4c5d-a266-d3ad40f38282" />
</p>
   
3. Install the required runtime:

   ```
   VC_redist.x86.exe
   ```

---

## 6. Install MySQL Server

<p>
<img width="1277" height="770" alt="Screenshot RD12" src="https://github.com/user-attachments/assets/4714e83c-423d-4583-9a08-396a5e6418c9" />
</p>

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

<p>
<img width="1277" height="770" alt="Screenshot RD13" src="https://github.com/user-attachments/assets/dc54165f-6097-4aaa-9857-4761edadb043" />
</p>

1. Launch **IIS Manager** as an administrator
2. Open **PHP Manager**
3. Register the PHP executable:

   ```
   C:\PHP\php-cgi.exe
   ```
4. Restart IIS by stopping and starting the server

---

## 8. Deploy osTicket Application Files

<p>
<img width="1277" height="770" alt="Screenshot RD14" src="https://github.com/user-attachments/assets/744e99ba-e5f5-4399-99f4-de1350afd98a" />
</p>

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

<p>
<img width="1277" height="770" alt="Screenshot RD15" src="https://github.com/user-attachments/assets/de792156-b0bf-4b25-a808-ae4c3b141d1a" />
</p>

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
