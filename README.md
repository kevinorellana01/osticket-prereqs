<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

You can find all the necessary installation files for this project below:  
[Download Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure subscription
- Azure Virtual Machine with the following configuration:
  - OS: Windows 10
  - vCPUs:4
  - Name: osticket-vm
  - Username:
  - Password:
- Remote Desktop Client

<h2>Installation Steps</h2>

### Step 1: Create and Configure the Azure Virtual Machine
  - Log in to the Azure portal and create a Virtual Machine with the specified configuration.
  - Connect to the VM using Remote Desktop with the provided credentials. 
<p>
<img width="1100" alt="Screenshot 2025-01-22 at 6 09 14 PM" src="https://github.com/user-attachments/assets/97604944-1227-4896-b062-002080c397f2" />
<img width="455" alt="Screenshot 2025-01-22 at 7 22 15 PM" src="https://github.com/user-attachments/assets/d72ce60a-c8dc-43c8-8271-e87a70c26452" />

### Step 2: Prepare the Virtual Machine
  - Inside the VM, download [osTicket-Installation-Files.zip](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD) to the desktop.
  - Extract the files into a folder named `osTicket-Installation-Files` on the desktop.
<img width="426" alt="Screenshot 2025-01-22 at 7 38 43 PM" src="https://github.com/user-attachments/assets/ac871ef0-3fe0-41e2-a2e8-90721517b404" />
<img width="439" alt="Screenshot 2025-01-22 at 7 39 23 PM" src="https://github.com/user-attachments/assets/c98e2504-11ed-448e-ab18-270397d5ecff" />

### 3. Install and Enable IIS with CGI
1. Open **Control Panel** -> **Programs** -> **Turn Windows features on or off**.
2. Enable the following:
   - **Internet Information Services (IIS)**
   - **World Wide Web Services** -> **Application Development Features** -> **[X] CGI**
<img width="294" alt="Screenshot 2025-01-22 at 7 41 22 PM" src="https://github.com/user-attachments/assets/ef80b743-f12e-4036-9c61-144694f3d1cd" />
<img width="296" alt="Screenshot 2025-01-22 at 7 41 40 PM" src="https://github.com/user-attachments/assets/1c3ca1e3-deb3-4c00-851b-e026576a516d" />


### 4. Install Required Components
From the `osTicket-Installation-Files` folder, perform the following installations:
1. Install **PHP Manager for IIS** (`PHPManagerForIIS_V1.5.0.msi`).
2. Install **Rewrite Module** (`rewrite_amd64_en-US.msi`).

<img width="380" alt="Screenshot 2025-01-22 at 7 42 50 PM" src="https://github.com/user-attachments/assets/50bd067d-1759-4d5c-b181-9ec0e61b0707" />
<img width="347" alt="Screenshot 2025-01-22 at 7 44 02 PM" src="https://github.com/user-attachments/assets/787882bb-ce07-406e-b96b-fc0e120cbb54" />
<img width="349" alt="Screenshot 2025-01-22 at 7 44 35 PM" src="https://github.com/user-attachments/assets/9416dd52-867f-4f50-9b1b-cf0cfb7a5561" />


### 5. Set Up PHP
1. Create the directory `C:\PHP`.
2. Extract `PHP 7.3.8` (`php-7.3.8-nts-Win32-VC15-x86.zip`) into the `C:\PHP` folder.
3. Install **VC_redist.x86.exe**.

### 6. Install MySQL
1. Install **MySQL 5.5.62** (`mysql-5.5.62-win32.msi`) with the following configuration:
   - Choose **Typical Setup**.
   - Launch the **Configuration Wizard** after installation.
   - Select **Standard Configuration**.
   - Set MySQL credentials:
     - Username: `root`
     - Password: `root`

### 7. Configure IIS
1. Open IIS as an Administrator.
2. Register PHP:
   - Open **PHP Manager** in IIS.
   - Register `C:\PHP\php-cgi.exe`.
3. Reload IIS:
   - Open IIS.
   - Stop and Start the server.

### 8. Install osTicket
1. Extract `osTicket v1.15.8` (`osTicket-v1.15.8.zip`) from the `osTicket-Installation-Files` folder.
2. Copy the `upload` folder to `C:\inetpub\wwwroot`.
3. Rename the folder from `upload` to `osTicket`.
4. Reload IIS.
5. In IIS:
   - Navigate to **Sites** -> **Default** -> **osTicket**.
   - On the right-hand side, click **Browse *:80**.
6. Address missing extensions:
   - Navigate to **PHP Manager** in IIS.
   - Enable the following extensions:
     - `php_imap.dll`
     - `php_intl.dll`
     - `php_opcache.dll`
7. Refresh the osTicket site in your browser.

### 9. Configure osTicket
1. Rename `ost-config.php`:
   - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
   - To: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`
2. Assign permissions to `ost-config.php`:
   - Disable inheritance -> Remove all permissions.
   - Add new permissions: `Everyone -> Full Control`.
3. Continue setup in the browser:
   - Name your help desk.
   - Set a default email for receiving customer emails.

### 10. Set Up the Database
1. Install **HeidiSQL** from the `osTicket-Installation-Files` folder.
2. Open HeidiSQL and create a new session:
   - Username: `root`
   - Password: `root`
3. Create a database named `osTicket`.
4. Complete the setup in the browser:
   - MySQL Database: `osTicket`
   - MySQL Username: `root`
   - MySQL Password: `root`
   - Click **Install Now!**

### 11. Post-Installation Cleanup
1. Delete the `C:\inetpub\wwwroot\osTicket\setup` folder.
2. Set `C:\inetpub\wwwroot\osTicket\include\ost-config.php` to **Read-only** permissions.

### 12. Access osTicket
- Admin Panel: [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)
- End-User Portal: [http://localhost/osTicket/](http://localhost/osTicket/)

## Conclusion
Following these steps, you should have a fully functional osTicket installation. Enjoy managing your help desk with osTicket!

