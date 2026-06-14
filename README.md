# Lab 1 — Active Directory

## Overview

This lab focused on building a basic Active Directory environment using a Windows Server virtual machine in Microsoft Azure. The goal was to practice core identity and access management skills used in IT Support, System Administration, Cloud, and Security roles.

Active Directory is used by organizations to centrally manage users, computers, groups, permissions, and security policies.

---

## Objective

Deploy a Windows Server 2022 virtual machine in Azure and configure it as an Active Directory Domain Controller for lab practice.

---

## Tools Used

* Microsoft Azure
* Windows Server 2022
* Remote Desktop
* Active Directory Domain Services
* Active Directory Users and Computers
* Group Policy Management
* PowerShell
* GitHub
* Loom

---

## Lab Environment

| Item              | Details                            |
| ----------------- | ---------------------------------- |
| Cloud Platform    | Microsoft Azure                    |
| Server OS         | Windows Server 2022                |
| Domain            | `corp.local`                       |
| Main Server Role  | Active Directory Domain Controller |
| Connection Method | Remote Desktop from MacBook        |

---

## What I Built

### 1. Deployed a Windows Server VM in Azure

I created a Windows Server 2022 virtual machine in Microsoft Azure to use as the main server for the Active Directory lab.

During deployment, I ran into Azure configuration issues, including:

* VM size unavailable in the original region
* Availability zone conflict

I solved these issues by:

* Changing the Azure region
* Selecting a compatible VM size
* Removing the availability zone restriction

---

### 2. Connected to the Server Using Remote Desktop

After the VM was created, I connected to the server from my MacBook using Remote Desktop.

This allowed me to manage the Windows Server environment remotely and begin configuring Active Directory.

---

### 3. Installed Active Directory Domain Services

I began installing the Active Directory Domain Services role on Windows Server 2022.

Active Directory Domain Services allows the server to manage users, computers, groups, and authentication inside a domain environment.

---

### 4. Promoted the Server to a Domain Controller

After installing AD DS, I promoted the Windows Server 2022 VM to a Domain Controller.

I created a new Active Directory forest:

```text
corp.local
```

This made the server responsible for managing authentication and directory services for the domain.

---

### 5. Opened Active Directory Users and Computers

I opened Active Directory Users and Computers, also known as ADUC.

ADUC is the main tool used to manage:

* Users
* Computers
* Groups
* Organizational Units
* Default Active Directory containers

I verified the default Active Directory containers:

* Builtin
* Computers
* Domain Controllers
* Users

---

## Organizational Units

### Purpose

Organizational Units, also known as OUs, are used to organize users, computers, and resources inside Active Directory.

OUs make it easier for administrators to manage departments and apply policies to specific groups of users or computers.

### OUs Created

I created the following Organizational Units:

* Finance
* HR
* IT
* Sales

### PowerShell Example

```powershell
New-ADOrganizationalUnit -Name "Finance" -Path "DC=corp,DC=local"
New-ADOrganizationalUnit -Name "HR" -Path "DC=corp,DC=local"
New-ADOrganizationalUnit -Name "IT" -Path "DC=corp,DC=local"
New-ADOrganizationalUnit -Name "Sales" -Path "DC=corp,DC=local"
```

---

## Security Groups

### Purpose

Security Groups are used to assign permissions to multiple users at once.

Instead of assigning permissions to users one by one, users can be added to a Security Group. Permissions can then be assigned to the group.

This makes access management easier, cleaner, and more scalable.

### Group Scope

```text
Global
```

### Group Type

```text
Security
```

### Security Groups Created

I created the following Security Groups:

* IT_Admins
* Finance_Users
* HR_Users
* Sales_Users

### PowerShell Example

```powershell
New-ADGroup -Name "IT_Admins" -GroupScope Global -GroupCategory Security -Path "OU=IT,DC=corp,DC=local"
New-ADGroup -Name "Finance_Users" -GroupScope Global -GroupCategory Security -Path "OU=Finance,DC=corp,DC=local"
New-ADGroup -Name "HR_Users" -GroupScope Global -GroupCategory Security -Path "OU=HR,DC=corp,DC=local"
New-ADGroup -Name "Sales_Users" -GroupScope Global -GroupCategory Security -Path "OU=Sales,DC=corp,DC=local"
```

### Verification

I verified that the Security Groups were created inside their corresponding Organizational Units.

---

## User Organization

I assigned users to their correct departmental Organizational Units.

Example:

```text
carol.jones → HR OU
```

This helped me understand how Active Directory can be organized by department to simplify administration and access management.

---

## Group Policy Objects

### Purpose

Group Policy Objects, also known as GPOs, are used to apply rules and settings to users and computers in Active Directory.

Examples of GPO settings include:

* Password policies
* Desktop wallpaper settings
* Software installation policies
* Security settings
* Login restrictions
* Removable storage restrictions

### Why GPOs Matter

Instead of configuring each computer individually, administrators can apply policies to an entire Organizational Unit at once.

This allows centralized management across a company environment.

---

## GPO Configuration Completed

I created a Group Policy Object named:

```text
SkoolGPO1
```

I linked the GPO to the IT Organizational Unit.

This showed how administrators can apply specific policies to a department by linking a GPO to an OU.

---

## Security Policy Configuration

I created and configured a security policy inside a Group Policy Object.

This helped me understand how administrators can enforce security settings across an entire Organizational Unit.

### Removable Storage Policy

I configured a Group Policy Object to deny access to removable storage devices.

Example use cases:

* Block USB drives
* Restrict software installation
* Enforce password policies
* Apply desktop settings

This is important because removable storage devices can create security risks in business environments.

---

## Password Management

### Purpose

Active Directory administrators can reset user passwords and require users to create a new password at next login.

### What I Practiced

* Resetting a user account password
* Forcing a password change at next logon
* Managing user accounts centrally through Active Directory

This is a common real-world help desk and system administration task.

---

## Problems I Ran Into

| Problem                                      | Solution                              |
| -------------------------------------------- | ------------------------------------- |
| VM size unavailable in original Azure region | Changed Azure region                  |
| Availability zone conflict                   | Removed availability zone restriction |
| VM configuration issue                       | Selected a compatible VM size         |

---

## What I Learned

From this lab, I learned how to:

* Deploy a Windows Server 2022 VM in Microsoft Azure
* Connect to a cloud server using Remote Desktop from my MacBook
* Install Active Directory Domain Services
* Promote a server to a Domain Controller
* Create a new Active Directory forest
* Open and use Active Directory Users and Computers
* Verify default Active Directory containers
* Create Organizational Units
* Use PowerShell to automate OU creation
* Create Security Groups
* Understand the difference between assigning access individually and assigning access through groups
* Link Group Policy Objects to Organizational Units
* Configure security policies using Group Policy
* Block removable storage devices through Group Policy
* Reset user passwords
* Force password changes at next logon

---

## Screenshots to Add

Add screenshots of the following items to document the lab:

1. Azure VM overview page
2. Successful Remote Desktop connection
3. AD DS installed in Server Manager
4. Domain Controller promotion confirmation
5. Active Directory Users and Computers showing `corp.local`
6. Default AD containers
7. Created OUs: Finance, HR, IT, Sales
8. Created Security Groups
9. Users assigned to their correct OUs
10. Group Policy Object named `SkoolGPO1`
11. GPO linked to the IT OU
12. Removable storage policy configured
13. Password reset or change-at-next-logon setting

---

## Real-World Skills Practiced

This lab helped me practice skills used in real IT environments, including:

* Identity and access management
* User account administration
* Group-based access control
* Active Directory organization
* Group Policy management
* Basic security policy enforcement
* Password reset support
* Cloud-based server deployment

---

## Next Steps

Future improvements for this lab:

* Add a second Windows client VM
* Join the client VM to the `corp.local` domain
* Test Group Policy from the client machine
* Practice account lockout and unlock scenarios
* Create more users using PowerShell automation
* Document the full lab with screenshots and a Loom walkthrough

---

## Lab Status

Completed core Active Directory setup and administration tasks.

Current focus:

```text
Creating and managing Security Groups in Active Directory
```

---

## Author

**Austin Decembre**
Cloud / IT Lab Portfolio
# AD-02
