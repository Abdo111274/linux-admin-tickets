# Ticket #002: Troubleshooting HR Directory Permissions

## Environment
- Operating System: Red Hat Enterprise Linux 9
- Category: Linux Permissions and Troubleshooting


## Problem Description

An HR employee named mohamed cannot create files inside the /company/HR directory.

Initial directory permissions:

    drwx------. root root /company/HR

The directory is owned by root and is not accessible to other users.

## Tasks

1. Check whether the HR group exists.
2. Check whether the mohamed user exists.
3. Create missing accounts if necessary.
4. Add mohamed to the HR group.
5. Configure directory ownership.
6. Set permissions and enable SGID.
7. Verify that mohamed can create files.

## Solution

### 1. Check Whether the HR Group Exists

    getent group HR

If the group does not exist:

    groupadd HR

### 2. Check Whether the User Exists

    id mohamed

If the user does not exist:

    useradd -m mohamed

### 3. Add the User to the HR Group

    usermod -aG HR mohamed

### 4. Configure Directory Ownership

    chown root:HR /company/HR

### 5. Configure Permissions

    chmod 2770 /company/HR

### 6. Verify the Configuration

    id mohamed
    ls -ld /company/HR

Expected permissions:

    drwxrws---. root HR /company/HR

### 7. Test File Creation

    su - mohamed
    touch /company/HR/test01.txt
    ls -l /company/HR

## Expected Results

- The HR group exists.
- The mohamed user belongs to the HR group.
- The directory owner is root.
- The directory group is HR.
- The owner has read, write, and execute permissions.
- Group members have read, write, and execute permissions.
- Other users have no permissions.
- SGID is enabled.
- The user can create files inside the directory.

## Skills Practiced

- Linux User and Group Management
- File Ownership
- Linux Permissions
- SGID
- Troubleshooting
- Command-Line Administration
- Verification and Testing