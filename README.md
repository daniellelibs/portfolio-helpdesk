# Help Desk Portfolio — Active Directory & IT Support Lab

Hands-on IT support lab demonstrating practical help desk skills: Active Directory administration, troubleshooting, security practices, and support ticket management.

---

## About This Portfolio

**Candidate:** Libiane Danielle  
**Target Role:** Help Desk / Technical Support (entry-level)  
**Certifications:** Google Cybersecurity Professional Certificate  
**Status:** Actively applying for help desk positions

This repository contains real lab work demonstrating the skills used in day-to-day IT support roles. Everything is self-built and documented — no templates, all practical experience.

---

## Repository Structure

```
portfolio-helpdesk/
├── README.md (you are here)
├── tickets/                          # Real support tickets
│   ├── ticket-001-password-reset.md
│   ├── ticket-002-account-lockout.md
│   └── ticket-003-folder-permissions.md
├── screenshots/                      # Lab environment evidence
│   └── (9 screenshots from Active Directory configuration)
├── documentation/                    # Guides & references
│   ├── security-guide.md
│   ├── troubleshooting-cheatsheet.md
│   └── gpo-password-policy.md
├── platforms/                        # Multi-platform ticketing demo
│   └── freshdesk-tickets.png (proof of Freshdesk ticketing)
└── scripts/                          # Automation & tools
    ├── system-info.ps1
    └── system-info-output.png
```

---

## What's Inside

### Tickets (Real troubleshooting scenarios)
Three complete support tickets documenting actual help desk workflows:

1. **Ticket #001 — Password Reset** (3 min resolution)
   - User forgot password, couldn't access workstation
   - Demonstrated: ADUC password reset, "must change on next logon" flag

2. **Ticket #002 — Account Lockout** (4 min resolution)
   - Account locked after failed login attempts
   - Demonstrated: account unlock, understanding Account Lockout Policy, user guidance

3. **Ticket #003 — Folder Permissions** (6 min resolution)
   - Access denied error on network folder
   - Demonstrated: NTFS permissions, Effective Access feature, Deny override

### Screenshots (9 images)
Evidence of lab work:
- Active Directory Users and Computers (OU structure, users, groups)
- Group Policy Management configurations
- Server Manager and system settings

### Documentation (Professional guides)

**Security Guide for End Users**
- Password best practices (12+ chars, complexity, rotation)
- Phishing recognition and reporting
- Multi-Factor Authentication (MFA)
- Social engineering defense
- Incident response procedures
- Leverages Google Cybersecurity certification

**Troubleshooting Cheat Sheet**
- Quick reference for 15+ common help desk issues
- Organized by symptom → diagnosis → solution
- STAR format for interview answers
- Practical commands (PowerShell, Windows utilities)

**Group Policy Configuration**
- Password Policy (complexity, length, age, history)
- Logon message (legal disclaimer / security notice)
- Real-world scenarios and troubleshooting
- Screenshots of working configuration

### Platforms (Multi-platform ticketing)
Screenshot showing the same 3 tickets created in **Freshdesk**, proving ability to use real ticketing platforms that enterprises use.

### Scripts (Automation & tools)
**system-info.ps1** — PowerShell script that collects:
- Computer name & OS version
- RAM installed
- Disk space available per drive

Demonstrates automation skills — help desk often needs quick system diagnostics.

---

## Lab Environment

**Infrastructure:**
- Windows Server 2022 (Domain Controller, Active Directory)
- VirtualBox virtualization
- Domain: `empresafake.local`
- Organizational Units: Funcionarios (test users)

**Technologies:**
- Active Directory Users and Computers (ADUC)
- Group Policy Management
- NTFS permissions & security
- PowerShell scripting
- Freshdesk ticketing platform

---

## Skills Demonstrated

| Skill | Evidence | Time to Complete |
|---|---|---|
| Active Directory management | 3 tickets, screenshots, OU/user creation | 1 hour |
| Password resets & account unlock | Tickets #001, #002 | 5 min each |
| NTFS permissions troubleshooting | Ticket #003, Effective Access | 6 min |
| Group Policy configuration | GPO documentation, screenshots | 30 min |
| Ticketing system proficiency | Freshdesk setup, 3 tickets | 40 min |
| Security awareness | Security guide for end users | 50 min |
| Troubleshooting methodology | Cheat sheet with 15+ scenarios | 45 min |
| PowerShell automation | system-info.ps1 script | 10 min |

---

## How This Helps Me Stand Out

✓ Real lab, not just theory — Actually built Active Directory, configured policies, resolved tickets  
✓ Multi-platform experience — Know Freshdesk, not just one ticketing system  
✓ Security-minded — Google Cybersecurity cert + documented security practices  
✓ Automation-aware — Can write simple scripts to save time  
✓ Professional documentation — Every ticket and guide written as if for real clients  
✓ Interview-ready — STAR format examples, common scenarios, real troubleshooting logic  

---

## Next Steps (In Progress)

- [ ] Practice on ServiceNow & Jira Service Management (additional platforms)
- [ ] CompTIA Security+ certification (in progress)
- [ ] More complex AD scenarios (group policies, delegation, multi-domain)
- [ ] Additional scripting (disk space alerts, service monitoring)

---

## Contact & Links

- GitHub: You're here
- Email: Available upon request

---

**Built:** August 2026  
**Last Updated:** August 2026  
**Status:** Active job search, continuously improving  

This portfolio represents 8+ hours of hands-on lab work. Everything shown here I've actually done — not copy-pasted from tutorials.


