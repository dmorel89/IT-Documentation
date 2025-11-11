How to Get Started with Windows Server 2022 (Hands-on project)

# How to Get Started with Windows Server 2022 (Hands-on project)

## **🖥️What is Windows Server** ?

 Windows Server: Enterprise Backbone for IT Infrastructure
Windows Server is a robust, enterprise-grade operating system developed by Microsoft to support and manage corporate IT environments. Unlike consumer-focused platforms like Windows 10 or 11, Windows Server
is engineered for centralized administration, scalability, and security across networks.

Windows Server acts as the central nervous system of a business’s IT infrastructure—coordinating devices, users, and services to ensure seamless operations. My experience with it has laid the foundation for deeper
learning in network administration, virtualization, and cloud integration.

- Various Versions of Windows Server  
Windows Server 2003, 2008 & R2, 2012 & R2, 2016, 2019 and 2022.
![Screenshot](images/screenshot01.jpg)


As a Level 1 Helpdesk Technician, I’ve worked with Windows Server to support and maintain critical infrastructure components:

🔐 User & Resource Management
Active Directory (AD): Created and managed user accounts, groups, and organizational units. Supported password resets, access control, and login troubleshooting.

Group Policy (GPO): Applied and troubleshot policies to enforce security settings, desktop configurations, and software restrictions across multiple machines.

📁 File Sharing & Security
Configured shared folders with NTFS and share-level permissions to ensure secure access.

Implemented firewall rules and software restrictions to maintain endpoint security and compliance.

🌐 Network Services
Supported DNS and DHCP configurations to ensure devices could locate each other and receive IP addresses dynamically.

Assisted in Remote Desktop Services (RDS) setup for remote access and support.

Monitored and maintained Windows Management Instrumentation (WMI) for system health and inventory reporting.

🧠 Virtualization & System Roles
Deployed and managed virtual machines using Hyper-V, optimizing resource usage and isolating environments for testing and training.

Participated in the configuration of server roles such as File Services, 
Print Services, and Backup Solutions to support business continuity.

# Setting up Windows Server 2022 on a Virtual Machine

1. **Download VirtualBox or VMware Workstation Pro**
   - Download Windows host (for Windows) & Extension Pack
   - Download VMware Workstation Pro on the official website (Browser)
     *(32 or 64bit depending on your computer)*  
   - **Download Windows Server 2022 ISO file** *(Free trial 180 days)*
![Screenshot](images/screenshot02.jpg)
---

2. **Open your Workstation and click on Create a New Virtual Machine**
   - Click on Typical *(Recommended)* ➝ Installer disc image file *(Browse the Downloads folder on your PC and click on the ISO file you just downloaded)*  
   - Guest Operating System *(Windows)*  
   - Name the Virtual Machine ➝ Specify Disk capacity *(by default it's 80GB)* ➝ Ready to Create Virtual Machine and Finish

---
3. **Power on the Virtual Machine**
   - During the booting process, quickly press any key to boot from CD or DVD to load the ISO.  
     If you miss it, shut it down and power again. Keep pressing any key to boot.

## Installing Windows Server 2022

- The ISO file will prompt Server operating system setup. Click on **Next** ➝ **Install Now**
- Select the operating system you want to install  
  *(Windows Server 2022 Standard Evaluation - Desktop Experience)* ➝ **Next** ➝ Accept terms & conditions ➝  
  Custom: Install Microsoft Server operating system only ➝  
  Installing Microsoft Server operating system...
![Screenshot](images/screenshot03.jpg)
### After Installing
- **Username**: administrator *(only default)*
- **Password**:  
- **Re-enter Password**
---
### 3. Renaming the Server to Something Simple

- Navigate to **File Explorer** ➝  
  Right click on **This PC** ➝ **Properties** ➝ **Advanced System Settings** ➝  
  Computer Name tab ➝ Click **Change** ➝ Enter new computer name *(e.g., Server2022)* ➝  
  Click **OK** (it will prompt to restart the machine) ➝  
  **Restart Now**
![Screenshot](images/screenshot04.jpg)
---
### 4. Create Active Directory Domain Services

- Navigate to **Server Manager** from the **Start Menu** ➝  
  On the top right, click **Manage** ➝ **Add roles and features**
![Screenshot](images/screenshot05.jpg)
**Before you begin:**
1. Open **Server Manager**.
2. Click **Next**.
3. Select **Role-based or feature-based installation**.
4. Click **Next**.
5. Click on **Active Directory Domain Services**.
6. Click **Add Features**.
7. Click **Next**, then **Install** (wait for it to succeed).
8. Click **Promote this server to a domain controller**.
9. Select **Add a new forest**.
10. Enter the **Root domain name** (e.g., `Njikason.com`).
11. Create a password (e.g., `Password@123`).
12. Click **Next**.
13. Wait for **Prerequisites check**.
14. Click **Install** — it will restart your computer.

> **Note:** Active Directory Users & Computers are now installed in the server.

---
## Creating a Static IP for Server 2022

1. In the search bar, type **Control Panel**.
2. Go to **Network and Internet**.
3. Click **View network status and tasks**.
4. Click **Change adapter settings**.
5. Right-click **Ethernet** > Select **Properties**.
6. Click on **Internet Protocol Version 4 (TCP/IPv4)**.
7. Select **Use the following IP address** and configure the static IP.
![Screenshot](images/screenshot59.jpg)
> In a **corporate environment**, Windows Server usually has a **static IP address**.
---
## whoami command

- Displays the fully qualified Domain Name (Fqdn) of the currently logged- in user, includes domain hierarchy in the output.
- whoami /fqdn
![Screenshot](images/screenshot537.jpg)

## VM Network Configuration

- Change the **virtual machine network** from **NAT** to **Host-only** so that the **VM** can talk to each other on the same network.
![Screenshot](images/screenshot06.jpg)

---
## Adding a Computer to a Domain (Windows) rules

* To enforce/practice with Windows Server (group policy, Active Directory users & Computers, Troubleshooting Skills )

* If it's a new install, for home lab (Renaming the PC will be easy to remember the Computer)  
Click on the Active File Explorer → Properties → change Settings → Computer name → Rename the Computer → Restart the Computer
![Screenshot](images/screenshot60.jpg)

---

* Navigate to your Control panel → Search & type Control Panel → View network status & tasks → change adapter
Settings → Ethernet → Properties → Disable IPv6 → Click on (TCP/IPv4) → Use the following IP address and click ok  
Use ping command to try and reach your Windows Server
![Screenshot](images/screenshot61.jpg)

**pinging the server**
![Screenshot](images/screenshot62.jpg)

---
# Now join the Computer to the Domain  

Click on the File Explorer → Right click on This PC → Properties → Domain or Workgroup (Win 11) → Advance Settings (Win10) → member of Domain  
administrator *username* (capitalp123) and password  
The Computer has been joined to the domain
![Screenshot](images/screenshot64.jpg)

---

* Logged in with the account (username) I created on Active Directory and now I can manage this account, reset password, disable account & apply group policies to the Computer.

![Screenshot](images/screenshot63.jpg)

# Shared Drive Permissions & User Account Creation
---
## Shared Drive Permissions

- **Creating a shared folder** for Sales, HR & Finance.  
  - Disable inheritance for each group (so each group has custom permissions and can't access the other groups folders).

### Steps to Create a Shared Folder:
1. Navigate to **Server Manager** → **File and Storage Services** → **Shares**.
2. Right-click on blank space → **New Share** → **SMB Share - Quick**.
![Screenshot](images/screenshot187.jpg)
3. Click **Next** → **Share Name**: `Njikason` → **Other Settings** → **Permissions** → **Next**.
4. Confirm and **Create**.
![Screenshot](images/screenshot189.jpg)

> To confirm the share drive is created:

- Navigate to **File Explorer** → **This PC** → **Local Disk (C:)** → **Shares** → `Njikason` folder.
![Screenshot](images/screenshot190.jpg)
- Create folders inside `Njikason` for:
  - HR  
  - Sales  
  - Finance  
![Screenshot](images/screenshot191.jpg)
---
## Creating User Accounts in Active Directory Users and Computers

### Steps to Create User Accounts:
1. Navigate to **Active Directory** → **Users** → **New**.
2. Scroll down to **Users** → Create a **Username** and **Password** to change at their next logon.
3. Created user accounts for:
   - Bob Smith  
   - Billy Barnes  
   - Holly Cross
![Screenshot](images/screenshot192.jpg)
# Configuring Shared Folder Permissions & Network Drive Mapping

## Disable Inheritance for Each User

1. Navigate to the folder for **HR**, **Sales**, or **Finance**.
2. Right-click on **Sales** → **Properties** → **Security** → **Advanced Settings**.
3. Click **Add** → **Select Principal** → Add **Bob Smith** → Click on **Modify** → Click **OK**.
![Screenshot](images/screenshot193.jpg)
## Remove Default Users, Keep Only Required Users

- Disable inheritance.
- Remove all users, leaving only **Administrators** and **Bob Smith**.
- Set **Bob Smith** as the owner.
- Click **Apply** and **OK**.
![Screenshot](images/screenshot194.jpg)
> Apply the same format to **HR** and **Finance** folders:
- Add only **Billy Barnes** for HR.
- Add only **Holly Cross** for Finance.
- Disable inheritance in each case.

---
## Logging into Each User PC

1. Log into **Bob Smith’s PC** using the assigned **username** and **password**.
![Screenshot](images/screenshot197.jpg)
2. Navigate to file explorer then **This PC** → In the **search bar**, type:

 \\\Server2022\Njikason

> Try accessing other folders:

- You will get an error saying "You don’t have access to this folder."
![Screenshot](images/screenshot195.jpg)
---
## Mapping a Network Drive for Bob Smith

1. Right-click on **This PC** → Select **Map Network Drive**.
    
2. Select **Drive (Z:)**.
    
3. In the **Folder** field, enter the path:

`\\Server2022\Njikason\Sales`

4. Click **Finish**.
![Screenshot](images/screenshot196.jpg)
![Screenshot](images/screenshot198.jpg)
![Screenshot](images/screenshot199.jpg)

---
