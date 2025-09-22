Active Directory (AD), is a directory service developed by Microsoft. It provides essential network services, including authentication, authorization, and resource management in Windows.

AD is like the IT environment's brain, managing who gets access to what files, tools, systems, and settings. It keeps everything organized and ensures that employees see only what they need to do their jobs.

## Active Directory Features

**Authentication**:

- AD provides a means for employees to log into the network using a user account provisioned by the organization. It allows security features such as locking an account so it cannot be used or automatically locking after a set number of unsuccessful login attempts.

**Authorization**:

- After authentication, AD controls access based on the user account's permissions and group memberships. This determines what resources a user can access and what actions they can perform.

**Centralized Management:**

- AD enables centralized management of user accounts, computers, printers, and security policies, allowing administrators to manage resources efficiently across the domain.

**Group Policy:**

- Group Policies allow administrators to define and manage settings for users and computers across the network, such as security settings, software installation, and desktop configurations.

-----
## Objects and Organizational Units

An object in Active Directory is a digital representation of a resource, such as a user, computer, group, printer, or any other resource that can be managed within the network.

#### **Types of Objects in Active Directory**

Some of the key objects within AD include:

- **User Objects:** Represent individual users within the organization. User objects store information such as usernames, passwords, personal details, and group memberships. These objects also hold a Security Identifier (SID), a unique value assigned to each user account for security purposes. The SID remains the same for the user account even if the user is renamed, but if the account is deleted and recreated, a new SID will be assigned.  
     
- **Computer Objects:** Represent computers that are part of the domain. These objects are used to manage policies, permissions, and security settings for computers in the network. Like user objects, computer objects also have a unique SID assigned when the computer joins the domain. This SID is used to identify the computer within the domain for security purposes and remains constant, even if the computer is renamed.  
     
- **Group Objects:** Represent collections of user or computer objects. Groups simplify management by allowing administrators to assign permissions and rights to a collection of users instead of managing each user individually. There are two types of groups:
    - Security Groups: Used to assign permissions and rights to resources.
    - Distribution Groups: Used for email distribution lists and do not have security permissions.  
         
- **Organizational Units (OUs):** Containers used to organize and manage objects within a domain. OUs can hold user accounts, groups, computers, and other OUs. They allow for delegated administration and the application of Group Policies.
    - For example, in the NotARealCompany domain, we could have an OU for the Finance team, that includes their user accounts and computers.  
         
- **Printer Objects:** Represent network printers. They store information about printer configurations and permissions for users to access the printers.  
     
- **Shared Folder Objects:** Represent shared resources such as file shares. These objects manage access and permissions for shared folders.

----
## Searching AD Objects

#### Using PowerShell

**AD User Search:**
```
Get-ADUser -Identity "NameHere" -Properties *
```

- lastLogonTimestamp - tells us when the account was last logged into
- LockedOut - tells us the account isn't currently locked
- MemberOf - tells us the groups this user is a part of
- modifyTimeStamp/Modified - tells us when this account was last modifie.

```plaintext
Get-ADUser -Identity "NameHere" -Properties LastLogonDate,LockedOut,Modified,PasswordExpired,PasswordLastSet
```

#### Using LDAP

LDAP is a protocol used to access and manage directory information services over a network, and is the primary means by which users and applications interact with the directory service.

Many vendors offer software that allows us to interact with LDAP using a graphical user-interface (GUI). One example of a free tool is Softerra LDAP Browser. In the below screenshot, we have opened the Users directory and have selected Admin Ferris:

![[Pasted image 20250210125525.png]]

-----

## Domain Controller

A Domain Controller is a server that hosts the Active Directory Domain Services (AD DS) role. It is responsible for controlling the domain, and has the following key functions:

- Validate user credentials during logon requests. When a user attempts to log in to a domain-joined machine, the DC verifies their username and password against the stored credentials in Active Directory.

- After authentication, the DC determines what resources a user can access based on their permissions and group memberships, enforcing security policies across the domain.

- DCs provide access to the Active Directory database, which contains information about all objects in the domain (users, computers, groups, etc.). They allow users and applications to query this directory for information. This can be accessed locally, as shown below, or remotely via LDAP (covered in the Accessing Objects lesson!)

- Apply Group Policies that dictate security settings, software installations, and other configurations for users and computers in the domain.

- In environments with multiple DCs, changes made on one DC (such as user account creation or modification) are replicated to other DCs to ensure consistency and redundancy across the domain.
![[Pasted image 20250210125642.png]]
#### **Types of Domain Controllers**

**Primary Domain Controller (PDC)**

- The PDC is the main DC that is responsible for managing password changes and certain other operations. In a multi-DC environment, one DC is designated as the PDC Emulator, which is important for backward compatibility with older Windows systems.

**Backup Domain Controller (BDC)**

- In older versions of Windows NT, BDCs provided redundancy by holding read-only copies of the user accounts database. Modern Windows environments use multi-master replication, so all DCs can read and write data.

**Read-Only Domain Controller (RODC)**

- An RODC holds a read-only copy of the AD database, which is useful for branch offices or locations where physical security cannot be guaranteed. RODCs can authenticate users but cannot make changes to the directory.

-----

## AD Structure Examples

**Single Domain Example**
![[Pasted image 20250210130008.png]]

**Multi-Domain Example (Tree/Forest)**
![[Pasted image 20250210125929.png]]

**Multi-Root Domain Example (Forest)**
![[Pasted image 20250210125912.png]]

-----

## Security Groups

Security groups allow IT teams to group users or other AD objects (such as computers) and then assign permissions to these groups, rather than to individuals.

![[Pasted image 20250210130140.png]]

------

## Groups Policy

In a large network environment, managing hundreds or thousands of computers and user accounts manually can quickly become challenging. Issues like unauthorized software installations, inconsistent password policies, and security vulnerabilities (e.g., open USB access) create serious problems. **Group Policy** is the answer to these problems.

Group Policy settings can be stored either locally on a computer or in Active Directory. When used with AD, these settings are grouped into a Group Policy Object (GPO). GPO is a collection of rules that define security settings, permissions, and configurations applied to users and computers in the network.

#### Types of GPOs

There are three types of GPOs: local, non-local, and starter.

**Local GPOs**

- These apply to a single computer only, regardless of whether it's part of a network or domain.
- Useful for standalone PCs or testing.
- Example: You set a local password policy on your personal computer.

**Non-Local GPOs**

- These are stored in Active Directory and apply across multiple computers and users in a domain environment.
- Admins use these GPOs to enforce rules for entire departments or groups, ensuring everyone follows the same policies.
- Example: A non-local GPO disables USB ports for all employees in the "Workstations" group within a company network.

**Starter GPOs**

- These are templates that contain a basic set of recommended settings to help admins create new GPOs faster.
- They don’t apply directly but serve as a starting point for creating customized policies.
- Example: An admin uses a starter GPO with pre-configured security settings to quickly set up a new policy for remote workers.

#### GPO Processing Order

The order in which Group Policies are processed determines which settings are ultimately applied to a computer or user. Following is the order in which GPOs are applied.

**Local Policy Processed First**

- The system applies local policies configured on the individual computer first.

**Active Directory Policies Processed in Hierarchy**

- Site-level policies are applied next.
- Domain-level policies follow.
- Organizational Unit (OU) policies are applied, starting from the outermost (closest to the root) and working inward to the specific nested OU.

**Nested Organizational Units (OUs)**

- Policies in nested OUs apply in the order from higher-level OU to lower-level OU.

**Conflict Resolution**

- If there are conflicting settings, the last applied policy (the one closest to the object, e.g., a lower-level OU) will take effect.
- For example:
    - The domain-level GPO allows USB storage devices and the OU-level GPO (applied to the “Workstations” OU) blocks USB storage devices.
    - GPOs applied at the OU level are processed last, the USB restriction from the OU-level GPO will override the domain-level GPO. As a result, users in the OU will not be able to use USB devices, even though the domain-level policy allows it.
- A Catch - When a GPO is enforced (discussed in the next section), it overrides any conflicting policies, regardless of where it falls in the LSDOU hierarchy (Local, Site, Domain, Organizational Unit). This means that even if a lower-level policy, such as one applied at the OU level, tries to change a setting, the enforced GPO will take precedence.

----

## Authentication and Security

**Kerberos Authentication**

Kerberos is a secure authentication system used in many organizations to ensure that users can access services like email, file servers, and databases without repeatedly entering their passwords. It operates using a system of encrypted tickets to prove a user's identity. Kerberos ensures that passwords aren't constantly sent across the network, meaning users can access multiple services after logging in once.

![[Pasted image 20250210130812.png]]

**NTLM (NT LAN Manager)**

NTLM (NT LAN Manager) is an older Windows authentication protocol that uses a challenge-response method to verify a user's identity without sending their password over the network. When a user tries to access a resource, the server sends a random challenge. The user's computer encrypts this challenge with a hashed version of their password and sends the response back to the server. The user is granted access if the response matches what the server expects.

![[Pasted image 20250210130832.png]]

**LDAP (Lightweight Directory Access Protocol)**

LDAP (Lightweight Directory Access Protocol) Authentication verifies user identities and controls access to resources by communicating with a centralized directory service, like Active Directory. During authentication, the user’s credentials are sent to the LDAP server in a bind request, and the server checks the credentials. The user can authenticate and request further resource access if the credentials are valid. Access is either granted or denied based on the server results.

![[Pasted image 20250210130850.png]]
## **Best Practices For AD Security**

**Regular Auditing and Monitoring**

Regular auditing and monitoring in Active Directory should be conducted, consistently checking who is accessing, modifying, or trying to log into the system. You can quickly spot unusual behavior by observing Windows Event logs, such as unauthorized attempts to access sensitive information, make changes to AD objects, or authentication failures.

**Least Privilege Principle**

The Least Privilege Principle means giving users the minimum access level to do their job. For example, if an employee only needs access to a specific set of files or set permissions, there’s no reason to give them administrative rights to the entire network. By limiting access, even if an account is compromised, the potential damage is minimized.

**Segregation of Duties**

Segregation of Duties is about dividing responsibilities so that no single person has control over all aspects of critical processes. For instance, one person may be responsible for creating user accounts, while another approves changes to security settings. This division prevents misuse of power and reduces the risk of insider threats.

**Patch Management**

Patch Management involves regularly updating AD servers and related software to fix security vulnerabilities. Keeping your systems patched ensures that any known weaknesses are resolved before attackers can exploit them. Software vendors release updates to address bugs and improve security, so staying current with these patches is essential to protecting your AD environment.