<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Windows Server 2025
- Windows 10
- Active Directory Domain Services (AD DS)
- DNS
- Remote Desktop Protocol (RDP)
- Windows Event Viewer
- PowerShell
- Azure Virtual Network

<h2>Operating Systems Used </h2>

- Windows Server 2025
- Windows 10 (21H2)

  <h2>Project Objectives</h2>

- Deploy a Windows Server 2022 Domain Controller in Microsoft Azure
- Configure networking, DNS, and virtual machine connectivity
- Install and configure Active Directory Domain Services (AD DS)
- Create and manage an Active Directory domain environment
- Join a Windows 10 client machine to the domain
- Create and manage administrative and standard user accounts
- Configure Organizational Units (OUs) for resource organization
- Troubleshoot user authentication and account lockout issues
- Enable and disable user accounts as part of identity management processes
- Monitor system and security logs using Event Viewer
- Validate domain authentication, DNS resolution, and client connectivity
- Gain hands-on experience with enterprise identity and access management concepts

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Azure Resource Group and Virtual Network
- Deploy Windows Server and Windows 10 Virtual Machines
- Configure the Domain Controller and install Active Directory Domain Services
- Join the Client Computer to the Domain and verify connectivity

<h2>Deployment and Configuration Steps</h2>

<p>
Step 1: Create Azure Resource Group and Virtual Network
</p>
<p>
<img width="1364" height="286" alt="1-resource group" src="https://github.com/user-attachments/assets/4b9a2b2f-f8f5-4afa-a7fc-2e3259cf0561" />
</p>
<p>
<img width="1195" height="372" alt="2- virtual network" src="https://github.com/user-attachments/assets/b2414c3e-b8ac-4e7f-94b4-cc3ebef25276" />
</p>

<p>
  
- What was done:
Created a Resource Group and Virtual Network in Azure to host all resources required for the Active Directory environment.
  
- Why it matters:
The Virtual Network provides secure communication between virtual machines, while the Resource Group helps organize and manage cloud resources efficiently.
</p>
<br />

<p>
Step 2: Create the Domain Controller VM (DC-1)
</p>
<p>
<img width="1178" height="499" alt="3- dc1" src="https://github.com/user-attachments/assets/cbf200bb-1f3f-4f62-8e2b-ab17647d6791" />
</p>

<p>
  
- What was done:
Deployed a Windows Server 2022 virtual machine and configured a static private IP address to serve as the Domain Controller.

- Why it matters:
A Domain Controller provides centralized authentication, authorization, and directory services. A static IP address ensures clients can consistently locate domain and DNS services.
</p>
<br />

<p>
Step 3: Create the Client VM (Client-1)
</p>
<p>
<img width="1199" height="458" alt="4 - client 1" src="https://github.com/user-attachments/assets/7db93827-3316-4fb6-9ee3-d899416b5a87" />
</p>
<p>
  
- What was done:
Deployed a Windows 10 virtual machine within the same Virtual Network as the Domain Controller.

- Why it matters:
This machine simulates a workstation in a corporate environment and will later be joined to the Active Directory domain for centralized management.
</p>
<br />

<p>
Step 4: Set DC-1 NIC Private address to be static
</p>
<p>
<img width="573" height="668" alt="5 - dc1 Nic static" src="https://github.com/user-attachments/assets/03a20566-17b5-4e2b-9587-9caea8618c0d" />
</p>

<p>
  
- What was done:
The Network Interface Card (NIC) of the Domain Controller (DC-1) was configured with a static private IP address within Azure. This ensures that the server always uses the same internal network address.

- Why it matters:
Domain Controllers provide critical services such as Active Directory and DNS. If the server's IP address changes, client computers may be unable to locate the Domain Controller, causing authentication, DNS resolution, and domain-related services to fail. Assigning a static IP address ensures reliable communication and consistent access to network services throughout the environment.
</p>
<br />

<p>
Step 5: Disable DC-1  windows Firewall
</p>
<p>
<img width="912" height="731" alt="6 - firewall off" src="https://github.com/user-attachments/assets/67308905-8bb1-4fdc-8f5e-af42294242d5" />
</p>

<p>
  
- What was done:
Logged into the Domain Controller (DC-1) and temporarily disabled the Windows Defender Firewall on all network profiles (Domain, Private, and Public) to test network communication between virtual machines.

- Why it matters:
Disabling the firewall during initial setup helps determine whether connectivity issues are being caused by firewall rules or by network configuration problems. This allows administrators to verify that Client-1 can successfully communicate with DC-1 before implementing more restrictive security settings. In a production environment, the firewall would typically remain enabled with properly configured rules rather than being permanently disabled.
</p>
<br />

<p>
Step 6: Configure DNS Settings
</p>
<p>
<img width="737" height="622" alt="7 - client 1 to dc 1 dns" src="https://github.com/user-attachments/assets/317e5729-e551-4e39-9646-0acab99cc6de" />
</p>

<p>
  
- What was done:
Configured the client machine to use the Domain Controller's private IP address as its primary DNS server.
  
- Why it matters:
Active Directory relies heavily on DNS to locate domain resources and services. Without proper DNS configuration, domain joins and authentication will fail.
</p>
<br />

<p>
Step 7: Restart Client-1
</p>
<p>
<img width="956" height="326" alt="8 - client1 restart" src="https://github.com/user-attachments/assets/dab8ca97-b0a3-4522-8ab9-8b17cba7c0c2" />
</p>

<p>
  
- What was done:
Restarted the Client-1 virtual machine through the Azure Portal after completing network and Domain Controller configuration changes.
  
- Why it matters:
Restarting the client ensures that any recent network configuration changes, such as DNS settings or connectivity updates, are fully applied. This helps guarantee that the client machine can properly communicate with the Domain Controller and accurately recognize Active Directory services before proceeding with domain-related tasks.
</p>
<br />

<p>
Step 8: Verify Network Connectivity
</p>
<p>
<img width="630" height="705" alt="9 - client 1 connectivity " src="https://github.com/user-attachments/assets/25bbc140-40f8-49fd-99b7-0d33121e5210" />
</p>

<p>
  
- What was done:
Used Remote Desktop and network testing tools to confirm communication between the client and server machines.

- Why it matters:
Verifying connectivity ensures that domain services, DNS resolution, and authentication requests can successfully travel across the network.
</p>
<br />

<p>
Step 9: Install Active Directory
</p>
<p>
<img width="779" height="561" alt="10 - AD installed" src="https://github.com/user-attachments/assets/6b73463b-d8c3-4ee6-a92a-531c6f75f306" />
</p>

<p>
  
- What was done:
Installed the Active Directory Domain Services (AD DS) server role on the Windows Server virtual machine.
  
- Why it matters:
AD DS provides the framework for centralized identity management, enabling administrators to manage users, computers, groups, and security policies.
</p>
<br />

<p>
Step 10: Promote the Server to a Domain Controller
</p>
<p>
<img width="776" height="799" alt="11 - Server to DC" src="https://github.com/user-attachments/assets/c3d3267c-4188-422c-9177-7f00bd19d43f" />
</p>

<p>
  
- What was done:
Promoted the server to a Domain Controller and created a new Active Directory forest and domain.
  
- Why it matters:
This step establishes the foundation of the organization's identity infrastructure and allows devices and users to authenticate against a centralized directory
</p>
<br />

<p>
Step 11: Create Organizational Units (OUs) AND Create a domain Admin user (jane) within the domain (mydomain.com)
</p>
<p>
<img width="759" height="535" alt="12 - jane admin" src="https://github.com/user-attachments/assets/1189fece-b860-4b50-bd3c-6fda3205970b" />
</p>

<p>
  
- What was done:
Created Organizational Units within Active Directory to logically organize users, computers, and administrative resources. Created a new user account within Active Directory and assigned it to the Domain Admins security group, granting the account administrative privileges across the domain.

- Why it matters:
OUs simplify management and allow administrators to apply permissions and Group Policies to specific groups of users or devices. Domain Administrator accounts are used to manage Active Directory resources such as users, computers, groups, and organizational units. Creating a dedicated administrative account follows best practices by separating administrative tasks from the default built-in administrator account and provides secure, centralized management of the domain environment.
</p>
<br />

<p>
Step 12: Join Client-1 to the Domain
</p>
<p>
<img width="745" height="522" alt="13 - client 1 join domain" src="https://github.com/user-attachments/assets/db07d21c-d6cd-4c53-9414-cd7a143134c6" />
</p>

<p>
  
- What was done:
Added the Windows 10 client computer to the Active Directory domain and restarted the system.
  
- Why it matters:
Joining the domain enables centralized management of the workstation, including authentication, security policies, and administrative controls.
</p>
<br />

<p>
Step 13: Set up remote desktop for non-administrative users on Client-1
</p>
<p>
<img width="459" height="668" alt="14 - rdp access" src="https://github.com/user-attachments/assets/6c6d8199-1ad7-4e98-b980-628bc34ad1df" />
</p>

<p>
  
- What was done:
Configured the client machine to allow Remote Desktop access for authorized domain users.

- Why it matters:
Remote administration is a common requirement in enterprise environments and allows IT staff to support systems efficiently.
</p>
<br />

<p>
Step 14: Generate 1000 Users with PowerShell and attempt to log into Client-1 with one of the users
</p>
<p>
<img width="789" height="851" alt="15 - 1000 users" src="https://github.com/user-attachments/assets/1fabc082-213d-4476-974e-478d84fa6efc" />
</p>
<p>
<img width="804" height="645" alt="16 - baru decu" src="https://github.com/user-attachments/assets/a6981f8e-3771-45d1-885c-a60697bae560" />
</p>

<p>
  
- What was done:
Used a PowerShell script to automatically create multiple Active Directory user accounts.
  
- Why it matters:
Automation reduces administrative effort, minimizes errors, and demonstrates practical scripting skills used by system administrators.
</p>
<br />

<p>
Step 15: Dealing with accounts lockouts

- Set account lockout policy in Active directory 
<p>
<img width="926" height="735" alt="17 - set account lock out policy     " src="https://github.com/user-attachments/assets/a2a4997e-cb23-42ed-b3fa-5cd68df95db2" />
</p>

- Lock user account out (baru.decu)
<p>
<img width="580" height="527" alt="18 - log in failure" src="https://github.com/user-attachments/assets/0b887307-b170-4632-a77a-7cd111e73123" />
</p>

- Unlock user account (baru.decu)

<p>
<img width="637" height="660" alt="19 - unlock account baru decu" src="https://github.com/user-attachments/assets/4c59bab0-d6ad-413d-9da2-5974b295cee2" />
</p>
  
<p>
  
- What was done:
Simulated an account lockout by entering incorrect login credentials multiple times, then used Active Directory administrative tools to identify the locked account, unlock it, and restore user access.
  
- Why it matters:
Account lockouts are a common Help Desk and System Administration issue. Understanding how to identify, troubleshoot, and resolve locked accounts helps maintain user productivity while enforcing security policies that protect against unauthorized access attempts.
</p>
<br />

<p>
Step 16: Enabling and Disabling User Accounts
</p>
<p>
<img width="626" height="621" alt="20 - disable account" src="https://github.com/user-attachments/assets/9c5e9b30-f4bf-4e51-88f2-4a91ca9ac20a" />
</p>
<p>
<img width="632" height="537" alt="21 - acct disabled" src="https://github.com/user-attachments/assets/3c45ff1c-7957-42fd-9a05-b306aeb9684d" />
</p>

<p>
  
- What was done:
Used Active Directory Users and Computers (ADUC) to disable and re-enable user accounts within the domain. This involved modifying account status settings to control whether users could log in and access network resources.
  
- Why it matters:
Disabling accounts is a common security and administrative practice used when employees leave an organization, take extended leave, or when suspicious account activity is detected. Re-enabling accounts restores access when appropriate while maintaining centralized control over user authentication and permissions.
</p>
<br />

<p>
Step 17:Observing Logs
</p>
<p>
<img width="770" height="673" alt="22 - security logs" src="https://github.com/user-attachments/assets/5d420ccd-7178-4889-9018-0c6a8628a2e1" />
</p>

<p>
  
- What was done:
Reviewed system and security logs using Windows Event Viewer to monitor authentication events, account activity, and system-generated messages within the Active Directory environment.
  
- Why it matters:
Logs provide valuable information about user logins, account lockouts, system errors, and security events. Monitoring logs helps administrators troubleshoot issues, investigate security incidents, and verify that Active Directory services are operating correctly.
</p>
<br />


<h2>Final Result</h2>

<p>
- Successfully deployed an on-premises Active Directory environment within Microsoft Azure by creating a Windows Server 2022 Domain Controller and a Windows 10 client workstation. Active Directory Domain Services (AD DS) and DNS were configured to provide centralized authentication, user management, and name resolution services across the environment.
</p>

<p>
- The client computer was successfully joined to the domain, allowing users to authenticate using domain credentials. Administrative tasks such as creating a Domain Administrator account, managing user accounts, enabling and disabling accounts, troubleshooting account lockouts, and reviewing security and system logs were completed to simulate real-world IT support and system administration responsibilities.
</p>

<p>
- The completed environment demonstrates foundational skills in cloud infrastructure deployment, Windows Server administration, Active Directory management, DNS configuration, user lifecycle management, authentication troubleshooting, and enterprise identity and access management.
</p>


<h2>Skills Demonstrated</h2>

- Microsoft Azure Virtual Machine Deployment
- Azure Virtual Networking
- Windows Server 2025 Administration
- Active Directory Domain Services (AD DS)
- Domain Controller Installation and Configuration
- Active Directory Forest and Domain Creation
- DNS Configuration and Troubleshooting
- Active Directory Users and Computers (ADUC)
- Organizational Unit (OU) Management
- Domain User Account Administration
- Domain Administrator Account Creation
- User Lifecycle Management
- Account Enablement and Disablement
- Account Lockout Troubleshooting
- Windows Event Viewer Log Analysis
- Authentication and Authorization Management
- Identity and Access Management (IAM) Fundamentals
- Remote Desktop Administration
- Network Connectivity Testing
- Windows Security Administration
- Troubleshooting and Root Cause Analysis
- PowerShell Fundamentals
- IT Infrastructure Documentation
- Enterprise Environment Administration
