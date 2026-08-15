# Group Policy Configuration — Password Policy & Logon Message

**Project:** Active Directory Lab Security Hardening  
**Date:** 2026  
**Objective:** Implement password complexity requirements and display security notice on logon screen

---

## Overview

Configured Group Policy at the domain level to enforce:
1. Strong password requirements (minimum 12 characters, complexity)
2. Password rotation policy (every 90 days)
3. Login warning message for security awareness

**Policy Applied to:** `Default Domain Policy` in `empresafake.local` domain

---

## Configuration Details

### Password Policy Settings

| Setting | Value | Purpose |
|---|---|---|
| Maximum password age | 90 days | Forces users to change passwords regularly |
| Minimum password length | 12 characters | Prevents weak passwords |
| Password must meet complexity requirements | Enabled | Requires mix of uppercase, lowercase, numbers, symbols |
| Enforce password history | 5 | Users cannot reuse last 5 passwords |

**Location in Group Policy:**
```
Computer Configuration 
→ Policies 
→ Windows Settings 
→ Security Settings 
→ Account Policies 
→ Password Policy
```

**Impact:**
- New user accounts must have 12+ character passwords with complexity
- Existing passwords expire every 90 days
- Users are prompted to change password before expiration
- System prevents reusing recent passwords

### Logon Message Configuration

**Message displayed on login screen:**
```
AUTHORIZED ACCESS ONLY

This computer is the property of TechFake Corp. Unauthorized access is prohibited.
All activities are monitored and logged. By accessing this system, you consent to monitoring.
```

**Location in Group Policy:**
```
Computer Configuration 
→ Policies 
→ Windows Settings 
→ Security Settings 
→ Local Policies 
→ Security Options
→ Interactive logon: Message text for users attempting to log on
```

**Purpose:**
- Legal disclaimer before access
- Sets expectations for monitoring and authorized use
- Protects organization from unauthorized access claims

---

## Implementation Steps

1. **Opened Group Policy Management** (Server Manager → Tools → Group Policy Management)
2. **Located Default Domain Policy** (Forest → Domains → empresafake.local)
3. **Edited policy** and configured:
   - Password Policy settings (minimum length, complexity, age)
   - Security Options (logon message text)
4. **Applied changes** via `gpupdate /force` command
5. **Verified** settings took effect on domain controller

---

## Real-World Scenarios

### Scenario 1: New User Needs to Set Password
- User account created, set temporary password
- User attempts to log in → forced to change password on first login
- New password must be 12+ characters with uppercase, lowercase, numbers, symbols
- If password fails complexity check, system rejects it with explanation

### Scenario 2: Password Expiration
- User's password is 90 days old
- Windows displays warning: "Your password will expire in X days"
- User is prompted to change password during login
- New password must follow same complexity rules

### Scenario 3: User Forgets Password
- Help desk resets password to temporary value
- System forces password change on next login
- User must create new 12-character complex password
- **(Related to Ticket #001 in our support tickets)**

---

## Security Benefits

✅ **Prevents brute-force attacks:** Complex, long passwords are harder to crack  
✅ **Regular rotation:** Limits damage window if password is compromised  
✅ **Legal protection:** Logon message establishes consent for monitoring  
✅ **Compliance:** Meets NIST/CIS security framework recommendations  
✅ **User awareness:** Message reminds users of security expectations  

---

## Troubleshooting

| Issue | Cause | Solution |
|---|---|---|
| Password change fails | New password doesn't meet complexity requirements | Ensure: 12+ chars, uppercase, lowercase, number, symbol |
| Policy not applying | Group Policy hasn't updated yet | Run `gpupdate /force` on affected computer |
| Users bypass message | Message not displaying | Check if policy applied to correct OU/users |
| Password expiration not working | Policy set to "Not Configured" | Re-edit policy, ensure "Define this policy setting" is checked |

---

## Commands Used

```powershell
# Force immediate policy update on domain controller
gpupdate /force

# View current password policy settings
Get-ADDefaultDomainPasswordPolicy

# Check when user password was last changed
Get-ADUser -Identity username -Properties PasswordLastSet | Select-Object Name, PasswordLastSet
```

---

## Files & Screenshots

- `gpo-password-policy.png` — Password Policy configuration screen
- `gpo-logon-message.png` — Logon message configuration

---

## Next Steps / Future Improvements

- Monitor password change compliance (reporting)
- Configure account lockout policy to work with password policy
- Add IP restriction policies (restrict logon to specific locations)
- Implement passwordless authentication (Windows Hello, smart cards)

---

**This configuration demonstrates:**
- Active Directory Group Policy administration
- Security policy implementation
- Domain-level configuration management
- Real-world security hardening practices

Perfect portfolio material for help desk / sysadmin interviews.
