# Ticket #001: User Management and Permissions

## Environment
- OS: Red Hat Enterprise Linux 9
- Category: Linux Administration
- Priority: Medium

## Problem
A new IT employee named ahmed needs access to
the /company/IT directory to create files.

## Tasks
1. Create the IT group.
2. Create the ahmed user.
3. Add ahmed to the IT group.
4. Create /company/IT.
5. Configure ownership and permissions.
6. Enable SGID.
7. Test file creation.

## Commands Used

```bash
groupadd IT
useradd -m ahmed
usermod -aG IT ahmed

mkdir -p /company/IT

chown root:IT /company/IT
chmod 2770 /company/IT

id ahmed
ls -ld /company/IT