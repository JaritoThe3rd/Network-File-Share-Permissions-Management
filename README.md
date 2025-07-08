# Azure AD Lab: File Share Permissions

## Instructions

1. **Power On VMs**
    - Turn on the DC-1 and Client-1 VMs in the Azure Portal if they are off.

2. **Create Sample File Shares with Permissions**
    - Log into DC-1 as your domain admin account (`mydomain.com\jane_admin`).
    - Log into Client-1 as a normal user (`mydomain\<someuser>`).
    - On DC-1, open the C:\ drive and create the following folders:
        - `read-access`
        - `write-access`
        - `no-access`
        - `accounting`
    - Share each folder and set the following permissions:
        - **read-access**: Group = `Domain Users`, Permission = `Read`
        - **write-access**: Group = `Domain Users`, Permission = `Read/Write`
        - **no-access**: Group = `Domain Admins`, Permission = `Read/Write`
        - *(Skip sharing "accounting" for now)*

3. **Test File Share Access as a Normal User**
    - On Client-1, log in as `<someuser>`.
    - Press `Win + R` and enter `\\dc-1` to open the shared folders.
    - Attempt to access each shared folder:
        - Which folders can you access?
        - Which folders can you create or edit files in?
        - Does access match the permissions you set?


https://github.com/user-attachments/assets/ba5d3591-b2b4-4eb2-861a-85c8d88d5859


4. **Create ACCOUNTANTS Security Group, Assign Permissions, and Test**
    - On DC-1, in Active Directory, create a security group named `ACCOUNTANTS`.
    - Set permissions on the `accounting` folder:
        - Group = `ACCOUNTANTS`, Permission = `Read/Write`
    - On Client-1, as `<someuser>`, try to access the `accounting` folder in `\\dc-1` (should fail).
    - Log out from Client-1 as `<someuser>`.
    - On DC-1, add `<someuser>` to the `ACCOUNTANTS` security group.
    - Sign back into Client-1 as `<someuser>`, try to access the `accounting` share in `\\dc-1` again (should now work).

5. **Cleanup**
    - Delete the VMs if you are done, or keep using them for practice.

---
