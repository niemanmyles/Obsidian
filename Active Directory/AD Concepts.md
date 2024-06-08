## Catchall Vocab
- Object: Literally anything in AD. These are users, GPOs, Computers, Groups, Printers, etc.
- Attributes: Like metadata for objects, this can be queried through LDAP.
- Schema: Basically the blueprint of an enterprise environment. This

defines what kinds of objects can exist in the AD database and their associated attributes.

- Domain: A domain is a logical group consisting of computers, users, Ous, etc. These can operate independently of one another or be connected via trusts.
- Forest: A forest is a collection of domains, and is the topmost container.
- Tree: A group of domains that are connected by a single parent root domain
- Container: Container objects hold other objects
- Leaf: Leaf objects do not contain other objects and are found at the end of the subtree hierarchy.
- - GUID (Global Unique Identifier): A unique 128-bit value assigned when a domain user or group is created. Every single object in AD has one. It is stored in the ObjectGUID attribute. These never change for a given object as long as it exists.

- Security Principals: Anything that the operating system can authenticate. This includes users, computers, accounts, or even threads/processes running under a certain context. Basically, this is who the OS thinks you are. In AD, security principles are domain objects that can manage access to other resources within a domain.

- SID (Security Identifier):  Used as a unique identifier for a security principal or security group. Every account, group, or process has a unique SID. In an AD environment, this is issued by a domain controller and stored in a secure database.

- DN (Distinguished name): Describes the full path to an object in AD (such as cn=bjones, ou=IT, ou=Employees, dc=inlanefreight, dc=local). In this example, the user bjones works in the IT department of the company Inlanefreight, and his account is created in an Organizational Unit (OU) that holds accounts for company employees. The Common Name (CN) bjones is just one way the user object could be searched for or accessed within the domain. This must be unique in the domain

- RDN (Relative Distinguished Name): A single component of the DN. Basically put, two of the same names can't exist on the same path.
- SPN (Service Principal Name): This uniquely identifies a service instance and is used by kerberos auth to associate an instance of a service with a logon account

GPO: Group policy object: Virtual collections of policy settings. Each GPO has a unique GUID.

ACL (Access control list): An ordered collection of ACEs that apply to an object

ACE( Access control entry): Each ACE identifies a trustee and lists the access rights that are explicitly allowed, denied, or audited for a give trustee

DACL (Discretionary ACL): DACLs define wich security principles are granted or denied access to object

System Access Control Lists (SACL) Allows for administrators to log access attempts that are made to secured objects. ACEs specify the types of access attempts that cause the system to generate a record in the security event log.

- sAMAccountName: user's logon name, must be shorter than 20 characters
- userPrincipalName: the full concatenation of [username]@[domain]


## FSMO Roles
These were created by microsoft to solve the issues that arise when a master DC goes down. Microsoft separated the roles that a DC can have into several roles. These are known as the Flexible Single Master Operation (FSMO) Roles.

These roles are:

- Schema Master (One per forest)

- Manages rw copy of AD schema

- Domain Naming Master (One per forest)

- Domain names

- Relative ID (RID) Master (One per domain)

- Assigns RID blocks, ensures no SID duplication

- Primary Domain Controller (PDC) Emulator (One per domain)

- Authoritative in a domain to respond to auth requests, password changes, and manage GPOs (also maintains time)

- Infrastructure Master (One per domain)

- Translates GUIDS, SIDs, and DNs between domains

 All five roles are assigned to the first DC in the forest root domain in a new AD forest. Each time a new domain is added to a forest, only the RID Master, PDC Emulator, and Infrastructure Master roles are assigned to the new domain. FSMO roles are typically set when domain controllers are created, but sysadmins can transfer these roles if needed



## Global Catalog
Global Catalog: A domain controller that stores copies of ALL objects in an AD forest. This stores a full copy of all objects in the current domain and a partial copy of objects that belong to other domains in the forest. A GC allows users and applications to find info about objects in ANY domain in the forest.

GC performs two functions:

- Authentication
- Object Search

Read-Only Domain Controller (RODC):

Read only domain cntrollers have a read-only AD database. No AD account passwords are cached on an RODC except the computer account and KRBTGT.

Replication: This is when AD ojects are updated and transferred from one DC to another. When a DC is added, a service called the Knowledge Consistency Checker (KCC) creates connection objects in the domain in order to manage the replication.

NTDS.dit: Literally the AD database lol

Usually lives at C:\Windows\NTDS on the ADDC