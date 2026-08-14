# Ticket #003 — Folder Access Denied

**User:** Maria Silva
**Category:** File/Folder Access
**Priority:** Medium
**Status:** Closed

## Reported Issue
"I'm getting 'Access Denied' when trying to open the RH shared folder on the network drive."

## Diagnosis
Checked NTFS folder permissions via Properties > Security > Advanced tab. Used **Effective Access** to simulate the user's access level: found an explicit **"Deny - Read"** permission set on Maria Silva's account for the RH folder. This prevented the user from reading or accessing any contents within the folder, regardless of other inherited permissions.

## Resolution
Removed the explicit Deny permission on Maria Silva's account via Security > Edit > selected user > unchecked "Deny - Read" > Apply. Granted standard Read access to the folder, restoring normal file access.

Advised the user to test access and confirmed the folder contents were now visible and accessible.

## Resolution Time
6 minutes

## Tools Used
Active Directory Users and Computers (ADUC), NTFS folder permissions, Effective Access feature
