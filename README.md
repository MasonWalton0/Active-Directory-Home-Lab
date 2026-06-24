# Active Directory Home Lab — Small Office Simulation

## Project Overview
This project is a fully functional home lab built using Oracle VirtualBox to simulate a small office IT environment. The goal was to practice real-world IT helpdesk and system administration tasks including user account management, Group Policy, and network shared folders. All documented with screenshots.

---

## Technologies Used
- **Oracle VirtualBox** — Virtual machine platform
- **Windows Server 2022** — Domain Controller (DC02)
- **Windows 11 Pro** — Client workstation (Client02)
- **Active Directory Domain Services (AD DS)** — User and policy management
- **Group Policy Management** — Enforcing IT policies across the domain
- **DNS** — Internal domain name resolution

---

## Lab Architecture
```
office.local Domain
│
├── DC02 (Windows Server 2022)
│   ├── Active Directory Domain Services
│   ├── DNS Server
│   ├── Group Policy Management
│   └── Shared Folder (CompanyShare)
│
└── Client02 (Windows 11 Pro)
    └── Joined to office.local domain
```

### Network Configuration
| Machine | Role | IP Address |
|--------|------|------------|
| DC02 | Domain Controller / DNS | 192.168.1.1 |
| Client02 | Employee Workstation | 192.168.1.2 |

Both VMs are connected via a VirtualBox **Internal Network** named `officelab`.

---

## Active Directory Structure
**Domain:** `office.local`

**Organizational Unit:** `Employees`

| Name | Username | Status |
|------|----------|--------|
| John Smith | jsmith | Active |
| Jane Smith | jsmith2 | Active (renamed from Jane Doe) |
| Mike Johnson | mjohnson | Disabled (terminated) |
| Sarah Connor | sconnor | Active (Sales group) |

**Groups:**
- `Sales` — Contains Sarah Connor

---

## IT Scenarios Practiced

### 1. Password Reset
**Scenario:** John Smith forgot his password and called the helpdesk.

**Actions Taken:**
- Opened Active Directory Users and Computers
- Right clicked John Smith → Reset Password
- Set temporary password and enabled "User must change password at next logon"

**Result:** John Smith was able to log in and set a new password on his next login.

---

### 2. Disabling a Terminated Employee
**Scenario:** Mike Johnson was let go and IT was notified to revoke access immediately.

**Actions Taken:**
- Opened Active Directory Users and Computers
- Right clicked Mike Johnson → Disable Account

**Result:** Mike Johnson's account was immediately disabled and he can no longer log into any company systems.

---

### 3. Unlocking a Locked Account
**Scenario:** Jane Doe entered her password incorrectly too many times and got locked out.

**Actions Taken:**
- Opened Active Directory Users and Computers
- Right clicked Jane Doe → Properties → Account tab
- Checked "Unlock account"

**Result:** Jane Doe's account was unlocked and she could log back in.

---

### 4. Onboarding a New Hire
**Scenario:** Sarah Connor joined the Sales team and needed an account and access.

**Actions Taken:**
- Created new user account (sconnor) in the Employees OU
- Created a Security Group called "Sales"
- Added Sarah Connor to the Sales group

**Result:** Sarah Connor had a working domain account and was added to the correct department group.

---

### 5. Renaming a User Account
**Scenario:** Jane Doe got married and changed her last name to Smith.

**Actions Taken:**
- Right clicked Jane Doe in Active Directory → Rename
- Updated full name to Jane Smith and logon name to jsmith2

**Result:** User account was updated to reflect the name change without losing any account data.

---

### 6. Group Policy — Restricting Control Panel Access
**Scenario:** IT decided employees should not have access to system settings.

**Actions Taken:**
- Opened Group Policy Management
- Created a new GPO called "Restrict Control Panel"
- Navigated to User Configuration → Policies → Administrative Templates → Control Panel
- Enabled "Prohibit access to Control Panel and PC Settings"
- Linked the GPO to the Employees OU
- Ran `gpupdate /force` on the client machine to apply immediately

**Result:** When John Smith tried to open Control Panel on Client02, he received the message: *"This operation has been cancelled due to restrictions in effect on this computer. Please contact your system administrator."*

---

### 7. Shared Company Folder
**Scenario:** The company needed a shared network drive for all employees to access files.

**Actions Taken:**
- Created a folder called `CompanyShare` on DC02 at `C:\CompanyShare`
- Right clicked → Properties → Sharing → Advanced Sharing
- Shared the folder and gave `Domain Users` Full Control permissions
- Accessed the share from Client02 using `\\DC02\CompanyShare`
- Created a test file inside the shared folder

**Result:** John Smith was able to access, read, and write files to the shared company drive from his workstation.

---

##  Screenshots

All screenshots are documented in the `/homelab2` folder in this repository and follow this naming convention:

| Screenshot | Description |
|-----------|-------------|
| Screenshot 1 | VirtualBox Opened, No VMs Yet |
| Screenshot 2 | Creating DC02 VM, Name and ISO Selected |
| Screenshot 3 | DC02 VM Summary |
| Screenshot 4 | Windows Server 2022 Setup Started on DC02 |
| Screenshot 5 | Selected Windows Server 2022 Standard Evaluation Desktop Experience |
| Screenshot 6 | Windows Server 2022 Installing |
| Screenshot 7 | Windows Server 2022 Installation Complete, Setting Admin Password |
| Screenshot 8 | Windows Server 2022 Login Screen |
| Screenshot 9 | Windows Server 2022 Desktop and Server Manager Open |
| Screenshot 10 | Renaming Server to DC02 |
| Screenshot 11 | Active Directory Installation Succeeded |
| Screenshot 12 | Setting Up New Forest office.local |
| Screenshot 13 | Recovery Password Set |
| Screenshot 14 | Server Restarted, Logged into OFFICE Domain |
| Screenshot 15 | Active Directory Users and Computers Open |
| Screenshot 16 | Organizational Unit called Employees |
| Screenshot 17 | Creating New User John Smith  |
| Screenshot 18 | New User John Smith Created in Employees OU |
| Screenshot 19 | Three Employees Created in Active Directory |
| Screenshot 20 | Password Reset for John Smith |
| Screenshot 21 | Mike Johnson Account Disabled (Terminated Employee) |
| Screenshot 22 | Unlocking Jane Doe Account |
| Screenshot 23 | New hire added Sarah Connor added to sales group |
| Screenshot 24 | Jane Doe Renamed To Jane Smith |
| Screenshot 25 | Client02 Windows 11 VM Created |
| Screenshot 26 | Windows 11 Client02 Desktop Ready |
| Screenshot 27 | Client02 Successfully Pinging DC02 |
| Screenshot 28 | Windows 11 Successfully Upgraded to Pro |
| Screenshot 29 | Client02 Successfully Joined to office.local Domain |
| Screenshot 30 | Client02 Login Screen Showing Domain Login Option |
| Screenshot 31 | User John Smith Forced to Change Password on First Login |
| Screenshot 32 | John Smith Password Successfully Changed on First Login |
| Screenshot 33 | John Smith Successfully Logged into Client02 as Domain User |
| Screenshot 34 | Group Policy Management Console Open |
| Screenshot 35 | Desktop Wallpaper Group Policy Object Created |
| Screenshot 36 | Desktop Wallpaper Group Policy Configured |
| Screenshot 37 | Desktop Wallpaper Policy Linked to Employees OU |
| Screenshot 38 | Group Policy Successfully Blocking Control Panel Access for John Smith |
| Screenshot 39 | CompanyShare Folder Created and Shared on DC02 |
| Screenshot 40 | John Smith Successfully Accessing CompanyShare Network Folder from Client02 |
| Screenshot 41 | File Created in CompanyShare by John Smith |
---

##  Key Skills Demonstrated
- Installing and configuring **Windows Server 2022**
- Setting up **Active Directory Domain Services**
- Creating and managing a **Windows domain**
- Managing **user accounts** (create, disable, unlock, rename, reset password)
- Creating and linking **Group Policy Objects (GPOs)**
- Configuring **network shared folders** with permissions
- Setting up **VM networking** in VirtualBox
- Joining a **Windows 11 client** to a domain
- Basic **troubleshooting** in a virtual lab environment

---

##  Purpose
This lab was built to develop and demonstrate practical IT skills relevant to roles such as:
- IT Helpdesk Technician
- Desktop Support Analyst
- Junior System Administrator
- IT Support Specialist

---

*Built and documented by Mason Walton— June 2026*
