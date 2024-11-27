![image](https://github.com/user-attachments/assets/00ac12fe-8953-4254-9c4b-bc97ab6a643b)

## Overview
This project involved setting up and configuring Active Directory Domain Services (ADDS) in a Windows Server environment hosted in Microsoft Azure. This lab extends Part 1 and demonstrates the creation of domain accounts, joining client machines to the domain, and enabling Remote Desktop access for users.

---

## Environments and Technologies Used
- **Microsoft Azure**
  - Virtual Machines (DC-1 and Client-1)
  - Compute Resources
- **Windows Server**
  - Active Directory Domain Services (ADDS)
  - DNS Configuration
- **Remote Desktop**

---

## Operating Systems Used
- **Windows Server 2019**
- **Windows 10 (21H2)**

---

## List of Prerequisites
1. Azure subscription with Virtual Machines (VMs) for DC-1 and Client-1.
2. Client-1 DNS settings pointed to the DC-1 private IP address.
3. Active Directory Domain Services (ADDS) installed on DC-1.
4. PowerShell scripting capabilities.

---

## Project Steps

### **Part 1: Active Directory Setup**

1. **Log in to DC-1:**
   - Install the **Active Directory Domain Services** (ADDS) role.
     ![image](https://github.com/user-attachments/assets/8b618a29-8a06-4d67-8f37-3cd15b4eeb74)

   - Promote the server as a Domain Controller (DC).     
   - Set up a new forest named `mydomain.com` (replaceable with any domain name).
     ![image](https://github.com/user-attachments/assets/3089a71d-0c11-4c18-a227-07221014c6a9)
     
   - Restart and log back in as `mydomain.com\labuser`.
     ![image](https://github.com/user-attachments/assets/a4f768b4-3c14-4533-80fe-184a0221b97d)
     ![image](https://github.com/user-attachments/assets/a47a2ce6-0ac5-42cb-a874-c56644409fb4)


     
2. **Create a Domain Admin User:**
   - Open **Active Directory Users and Computers (ADUC)**.
   - Create Organizational Units (OUs):
     - `_EMPLOYEES`
     - `_ADMINS`
   - Add an employee named `Jane Doe` with username `jane_admin`.
   - Assign `jane_admin` to the **Domain Admins Security Group**.
     ![image](https://github.com/user-attachments/assets/508b3662-5cb5-4b10-9425-53552ced5480)

   - Log out and log back in as `mydomain.com\jane_admin`.
     ![image](https://github.com/user-attachments/assets/a8e3b4fc-282b-44a8-a0a5-339e2b85f23d)


3. **Join Client-1 to the Domain:**
   - Set Client-1's DNS settings to the DC’s private IP address.
   - Restart Client-1 and join it to the domain `mydomain.com`.
     ![image](https://github.com/user-attachments/assets/822c3e09-a33b-447e-8603-c92c6f2b3e59)

   - Verify in ADUC that Client-1 appears under **Computers**.
     ![image](https://github.com/user-attachments/assets/2adee9d4-0875-4231-8c47-6bbe945959a8)

   - Move Client-1 to a new OU named `_CLIENTS`.
     ![image](https://github.com/user-attachments/assets/7beca858-b992-42d7-8daf-d88ee4c234d6)


4. **Finish the Lab:**
   - Shut down the VMs in Azure to save costs.

---

### **Part 2: Remote Desktop and Bulk User Creation**

1. **Enable Remote Desktop Access for Non-Admin Users:**
   - Log in to **Client-1** as `mydomain.com\jane_admin`.
   - Open System Properties > Remote Desktop.
   - Allow `Domain Users` to access Remote Desktop.
     ![image](https://github.com/user-attachments/assets/3a9fd961-75d2-4e78-b602-fd922f0f1867)


2. **Create Multiple Users Using PowerShell:**
   - Log in to **DC-1** as `jane_admin`.
   - Open PowerShell ISE as an administrator.
   - Create and run a script to bulk-create users.
     - Users are added to the `_EMPLOYEES` OU.
   - Verify in ADUC that the accounts were successfully created.
     ![image](https://github.com/user-attachments/assets/1833591e-4fbc-4170-9eed-18d19517c31b)


3. **Test User Accounts:**
   - Attempt to log in to **Client-1** using one of the newly created accounts.
     ![image](https://github.com/user-attachments/assets/12c8aec7-5bfd-4c45-ae76-144daada5e38)


4. **Wrap-Up:**
   - Ensure the VMs remain in Azure for future labs.
   - Shut down the VMs in Azure to save costs.

---

## Key Learning Outcomes
- Successfully configured Active Directory Domain Services on DC-1.
- Joined a client machine to the domain and managed it via ADUC.
- Enabled Remote Desktop access for non-administrative users.
- Automated user account creation using PowerShell.

---

## Conclusion
This project demonstrated a comprehensive understanding of Active Directory setup and configuration, as well as efficient user management techniques using tools like ADUC and PowerShell. It highlights the ability to manage resources in a Windows Server environment and integrate systems within a domain structure.
