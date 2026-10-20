# Ticket-005: SELinux Troubleshooting

## Ticket Information
- Ticket ID: 005
- Category: Linux Security
- Status: In Progress

## Problem Description
The Apache web server is running, but it cannot access the website content as expected.

Standard Linux file permissions appear to be correct. SELinux may be preventing Apache from accessing the files because of an incorrect security context.

## Step 1: Check SELinux Status

Commands:
    getenforce
    sestatus

Expected Knowledge:
- Enforcing: Blocks access that violates SELinux policies and logs denials.
- Permissive: Logs policy violations without blocking access.
- Disabled: SELinux policies are not enforced.

## Step 2: Inspect SELinux Contexts

Commands:
    ls -Z /var/www/html/index.html
    ls -Zd /var/www/html

Purpose:
Inspect the SELinux security contexts of the website file and directory.

Expected SELinux context type for standard Apache web content:
    httpd_sys_content_t

## Step 3: Check Apache Status and Logs

Commands:
    systemctl status httpd
    journalctl -u httpd

Purpose:
Confirm that Apache is running and investigate service errors.

## Step 4: Investigate SELinux Denials

Command:
    ausearch -m AVC -ts recent

Purpose:
Search audit logs for recent SELinux access denials.

Additional command (if available):
    sealert -a /var/log/audit/audit.log

Note:
The sealert command may require the setroubleshoot-server package.

## Step 5: Check the Default SELinux Context

Command:
    matchpathcon /var/www/html/index.html

Purpose:
Compare the expected default context with the actual context.

## Step 6: Restore Default Contexts If Incorrect

Command:
    restorecon -Rv /var/www/html

Purpose:
Restore default SELinux contexts for website files and directories.

Verify the result:
    ls -Z /var/www/html/index.html

Important:
Run restorecon only after investigating the issue and determining that the contexts need correction.

## Step 7: Test Apache

Command:
    curl -I http://localhost

Purpose:
Check the HTTP response from the local Apache server.

If the problem persists, review the Apache logs and SELinux audit messages again.

## Root Cause
An incorrect SELinux context may prevent Apache from accessing website content.

The actual root cause must be confirmed by inspecting the contexts and audit logs.

## Resolution
Investigated SELinux status, inspected file contexts, checked for AVC denials, and documented the appropriate troubleshooting steps.

The ticket should be marked Resolved only after the problem has been reproduced, corrected, and verified.

## Skills Demonstrated
- SELinux administration
- Linux security troubleshooting
- Apache troubleshooting
- Audit log analysis
- SELinux file contexts
- restorecon
- Linux command-line administration

## Safety Notes
- Never disable SELinux just to bypass a problem.
- Do not change security contexts without identifying the cause.
- Verify commands and results in a test environment.
- Do not claim the issue is resolved until the website works as expected.