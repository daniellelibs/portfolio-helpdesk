# Ticket #002 — Account Lockout

**User:** Maria Silva
**Category:** Account Access
**Priority:** Medium
**Status:** Closed

## Reported Issue
"My account got locked and I can't log in, it says 'This user account has been locked out.'"

## Diagnosis
Checked the user account in Active Directory Users and Computers. Found the **"Account is locked out"** flag enabled after multiple failed login attempts, consistent with the domain's configured Account Lockout Policy (3 invalid attempts threshold, set via Group Policy).

## Resolution
Unlocked the account via **Properties > Account tab > unchecked "Account is locked out."** Advised the user on password best practices to help avoid future lockouts.

## Resolution Time
4 minutes

## Tools Used
Active Directory Users and Computers (ADUC), Group Policy Management
