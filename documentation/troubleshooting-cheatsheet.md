# Help Desk Troubleshooting Cheat Sheet

**Quick reference for common IT support issues. Organized by symptom → diagnosis → solution.**

---

## ACCOUNT ACCESS ISSUES

### Problem: User Can't Log In

**Symptoms:**
- "Invalid credentials" error
- "Account is locked out"
- "Logon failure: unknown user name or bad password"

**Diagnosis Steps:**
1. Confirm username is correct (check with user or employee directory)
2. Check if account is locked (Active Directory Users and Computers)
3. Verify password meets complexity requirements
4. Check if account is disabled

**Solutions:**

| Issue | Solution | Time |
|---|---|---|
| Forgot password | Reset password via ADUC → right-click user → Reset Password. Enable "User must change password at next logon." | 3 min |
| Account locked | ADUC → user properties → Account tab → uncheck "Account is locked out" | 2 min |
| Wrong username | Guide user to correct username format (usually firstname.lastname) | 5 min |
| Password doesn't meet requirements | Explain requirements (12+ chars, mixed case, numbers, symbols). Reset with temp password. | 5 min |

---

### Problem: User Locked Out After Multiple Failed Attempts

**Symptoms:**
- Account suddenly locked despite knowing password
- Message: "This user account has been locked out"

**Diagnosis:**
- Check Group Policy: Computer Config → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy
- Typical threshold: 3-5 invalid attempts

**Solution:**
1. Unlock via ADUC → user properties → Account tab → uncheck "Account is locked out"
2. Advise user on password practices to prevent future lockouts
3. Consider if user needs password reset (if forgotten their real password)

**Time:** 4 minutes

---

## FILE & FOLDER ACCESS ISSUES

### Problem: "Access Denied" Error When Opening Files/Folders

**Symptoms:**
- "You do not have permission to access this folder"
- "Access denied" when trying to open network drive or shared folder
- Can see folder but can't open it

**Diagnosis Steps:**
1. Right-click folder → Properties → Security tab
2. Check if user has Read permission (look for username in permissions list)
3. Look for explicit "Deny" permissions that override "Allow"
4. Use Effective Access feature to simulate user's actual access level:
   - Properties → Security → Advanced → Effective Access tab → "Select a user" → choose username → "View effective access"
   - Shows what user can/cannot do with visual checkmarks

**Solutions:**

| Scenario | Action | Time |
|---|---|---|
| User not in permission list | Edit → Add user → grant Read permission → Apply | 5 min |
| Explicit Deny is set | Edit → remove Deny OR change to Allow | 5 min |
| Permission inherited from parent folder | Check parent folder permissions, may need to propagate changes | 10 min |

**Pro tip:** Always use Effective Access to verify before/after — it's the ground truth of what a user can do.

**Time:** 6 minutes average

---

## ACCOUNT LOCKOUT POLICY (GROUP POLICY)

### What It Does
Automatically locks accounts after N failed login attempts to prevent brute-force attacks.

**Where to find:**
Group Policy Management → Domain → Default Domain Policy → Edit → Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy

**Three settings:**
- **Account lockout threshold:** how many wrong attempts before lock (typically 3)
- **Account lockout duration:** how long account stays locked in minutes (typically 15-30, or "until admin unlocks")
- **Reset account lockout counter after:** how long before failed attempt counter resets (typically 15 minutes)

**Example scenario:**
- Threshold: 3 attempts
- Duration: 15 minutes
- Reset: 15 minutes

User tries wrong password 3 times → account locks for 15 minutes → can try again after 15 min

---

## SERVICE/APPLICATION ISSUES

### Problem: Application Won't Start / "Service Not Running"

**Symptoms:**
- Application crashes on launch
- "Service unavailable" error
- Application was working yesterday, now doesn't start

**Diagnosis:**
1. Check if service is running (Services.msc)
2. Check Event Viewer for errors (Event Viewer → Windows Logs → Application)
3. Verify application folder permissions
4. Check if application was recently updated (may have broken compatibility)

**Solutions:**

| Cause | Fix | Time |
|---|---|---|
| Service not running | Services.msc → find service → right-click → Start | 2 min |
| Service disabled | Services.msc → properties → Startup type: Automatic → Start | 3 min |
| Permissions issue | Check folder/file permissions, grant Read+Execute | 5 min |
| Corrupt installation | Uninstall → restart → reinstall application | 15 min |

---

## PRINTER ISSUES

### Problem: Can't Print / Printer Not Found

**Symptoms:**
- "Printer not found" error
- Print job stuck in queue
- Printer shows offline in device settings

**Quick Fixes:**
1. **Printer offline:**
   - Check if printer is powered on and connected to network
   - Restart printer (power cycle: off 30 sec → on)
   - Ping printer IP to confirm network connectivity

2. **Print queue stuck:**
   - Settings → Devices → Printers & Scanners → select printer → "Manage" → "Pause" → wait 10 sec → "Resume"
   - Or via command line: `net stop spooler` → `net start spooler`

3. **Printer not showing up:**
   - Add printer manually: Settings → Devices → Printers & Scanners → "Add a printer"
   - Select shared printer from network

**Time:** 5-10 minutes

---

## NETWORK CONNECTIVITY

### Problem: No Internet / Can't Connect to Network

**Symptoms:**
- WiFi disconnected
- "No internet" in system tray
- Can't access internal network resources
- Ping fails

**Diagnosis:**
1. Check if other devices have internet (confirms it's not ISP issue)
2. Restart network adapter (Settings → Network → Status → "Change adapter options" → right-click ethernet/WiFi → Disable/Enable)
3. Check IP configuration: `ipconfig /all` in Command Prompt
4. Ping default gateway: `ping 192.168.1.1` (or your gateway IP)

**Solutions:**

| Issue | Solution | Time |
|---|---|---|
| WiFi disconnected | Reconnect to network, check password | 2 min |
| No IP address (shows 169.x.x.x) | Release & renew: `ipconfig /release` → `ipconfig /renew` | 3 min |
| Can't reach gateway | Check network cable, restart router/modem | 5 min |
| Firewall blocking | Temporarily disable Windows Firewall, test, re-enable | 5 min |

---

## GENERAL TROUBLESHOOTING WORKFLOW (STAR FORMAT)

Use this structure in interviews when explaining a problem you solved:

**S — Situation:** What was the problem? ("User reported can't access RH folder")  
**T — Task:** What were you assigned to do? ("Restore access to the folder")  
**A — Action:** What specific steps did you take? ("Checked permissions via Properties > Security > Advanced, found explicit Deny, removed it")  
**R — Result:** What was the outcome? ("User regained access, confirmed working")

---

## QUICK COMMANDS

```
# Check services
Get-Service | Where-Object {$_.Status -eq "Running"} | Select-Object Name, Status

# Reset password (PowerShell as Admin)
Set-ADAccountPassword -Identity username -NewPassword (ConvertTo-SecureString -AsPlainText "TempPassword123!" -Force)

# Unlock account (PowerShell as Admin)
Unlock-ADAccount -Identity username

# Check IP configuration
ipconfig /all

# Restart a service
net stop servicename
net start servicename

# View group memberships
whoami /groups
```

---

## When in Doubt

- **Ask the user more questions:** How did the problem start? What were you doing? What error message did you see?
- **Replicate the issue:** Try it yourself first before declaring it broken
- **Check Event Viewer:** Applications and Services → look for errors with timestamps
- **Consult documentation:** Company wiki, internal runbooks, vendor documentation
- **Escalate:** If you can't resolve in 15-20 minutes, escalate to N2/senior support — don't waste time

---

**Last updated:** 2026  
**Confidence level:** Tested in real lab scenarios
