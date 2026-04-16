# Active Directory Home Lab with osTicket Help Desk


## Overview

A fully functional IT Support home lab built from scratch using VirtualBox. This lab simulates a real enterprise IT environment with Active Directory, Group Policy, DHCP, DNS, a domain-joined Windows 11 client, and a working osTicket help desk ticketing system.


---

## Lab Architecture

```
┌─────────────────────────────────────────────────────┐
│                  Internal Network (intnet)           │
│                   192.168.10.0/24                    │
│                                                      │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────┐  │
│  │    DC01      │  │  CLIENT01    │  │OSTICKET01 │  │
│  │Windows Server│  │  Windows 11  │  │  Ubuntu   │  │
│  │    2022      │  │              │  │  Server   │  │
│  │192.168.10.10 │  │192.168.10.100│  │192.168.10 │  │
│  │              │  │              │  │    .20    │  │
│  │ AD DS | DNS  │  │Domain Joined │  │ osTicket  │  │
│  │ DHCP | GPO   │  │Lab\jsmith    │  │   LAMP    │  │
│  └──────────────┘  └──────────────┘  └───────────┘  │
└─────────────────────────────────────────────────────┘
```

---

## Technologies Used

| Technology | Version | Role |
|------------|---------|------|
| Oracle VirtualBox | 7.1.16 | Hypervisor |
| Windows Server 2022 | Evaluation | Domain Controller |
| Windows 11 | 25H2 | Client Machine |
| Ubuntu Server | 24.04 LTS | osTicket Host |
| Active Directory Domain Services | - | Identity & Access Management |
| DNS Server | - | Name Resolution |
| DHCP Server | - | IP Address Management |
| Group Policy | - | Policy Management |
| osTicket | v1.18.2 | Help Desk Ticketing |
| Apache2 | - | Web Server |
| MySQL | - | Database |
| PHP | - | Backend Language |

---

## Lab Features

### Active Directory
- Domain: `lab.local`
- 3 Organizational Units: IT, HR, Finance
- 7 domain users across all OUs
- Static IP Domain Controller: `192.168.10.10`

### DNS & DHCP
- DC01 configured as authoritative DNS server
- DHCP scope: `192.168.10.100 – 192.168.10.200`
- Default gateway: `192.168.10.1`

### Group Policy Objects
- **Password Policy** (domain-wide): 12 character minimum, complexity enabled, 90-day expiry
- **Desktop Lockdown** (IT OU): 15-minute screen lock, password-protected screensaver

### osTicket Help Desk
- Deployed on Ubuntu Server with LAMP stack
- Accessible at `http://192.168.10.20/osticket/upload`
- 10 realistic support tickets created and documented

---

## Phase Breakdown

### Phase 1 — Hypervisor Setup
- Installed Oracle VirtualBox 7.1.16 on Windows 11 24H2
- Installed Extension Pack for USB and additional features
- Downloaded 3 ISOs: Windows Server 2022, Windows 11, Ubuntu Server

### Phase 2 — VM Creation
- Created DC01 (60GB, 4GB RAM, 2 CPU)
- Created CLIENT01 (50GB, 4GB RAM, 2 CPU) with EFI/TPM enabled
- Created OSTICKET01 (25GB, 2GB RAM, 2 CPU)
- All VMs placed on `intnet` internal network

### Phase 3 — Domain Controller Configuration
- Installed Windows Server 2022 on DC01
- Renamed computer to DC01, set static IP `192.168.10.10`
- Installed and configured AD DS, DNS, DHCP roles
- Promoted server to Domain Controller for `lab.local`
- Created OUs: IT, HR, Finance
- Created 7 domain users (jsmith, sjones, mbrown, ewilson, dtaylor, ldavis, jmiller)
- Created and linked GPOs: Password Policy, Desktop Lockdown

### Phase 4 — Client Domain Join
- Installed Windows 11 on CLIENT01
- Configured DNS to point to DC01 (`192.168.10.10`)
- Joined CLIENT01 to `lab.local` domain
- Verified GPO application with `gpresult /r`
- Logged in as domain user `LAB\jsmith`

### Phase 5 — osTicket Deployment
- Installed Ubuntu Server on OSTICKET01
- Configured static IP `192.168.10.20`
- Installed LAMP stack (Apache2, MySQL, PHP + extensions)
- Created MySQL database and user for osTicket
- Deployed osTicket v1.18.2
- Configured help desk portal accessible from CLIENT01

### Phase 6 — Support Tickets (In Progress)
10 realistic support tickets simulating real IT support scenarios — see ticket list below.

---

## Support Tickets

| # | User | Issue | Category |
|---|------|-------|----------|
| 01 | John Smith | Account locked out - cannot login | Account Management |
| 02 | Emma Wilson | New hire setup - need AD account and access | Onboarding |
| 03 | David Taylor | Cannot access shared folder | Permissions |
| 04 | Lisa Davis | Password reset request | Account Management |
| 05 | Mike Brown | New laptop needs to be joined to domain | Hardware Setup |
| 06 | James Miller | Need access to Finance shared resources | Permissions |
| 07 | Sarah Jones | Network printer not appearing | Hardware |
| 08 | John Smith | Desktop wallpaper keeps changing automatically | GPO Troubleshooting |
| 09 | Mike Brown | Employee offboarding - account needs to be disabled | Offboarding |
| 10 | John Smith | Software deployment needed for IT department | GPO Deployment |

---

## Key Skills Demonstrated

- Active Directory administration (users, OUs, groups)
- Group Policy creation and troubleshooting
- DNS and DHCP server configuration
- Windows domain environment setup
- Linux server administration (Ubuntu)
- LAMP stack deployment
- Help desk ticketing system administration
- IT support ticket lifecycle management
- PowerShell for AD administration
- Network troubleshooting in a virtualized environment

---

## Certifications

- Microsoft Azure AZ-900 (in progress)
- CompTIA A+ (targeting)

---

## Author

**Mohammad Zayed**  
IT Support Engineer | Dubai, UAE  
[LinkedIn](#) | [GitHub](#)

---

*This lab was built entirely from scratch as a portfolio project to demonstrate real-world IT Support Engineer skills.*
