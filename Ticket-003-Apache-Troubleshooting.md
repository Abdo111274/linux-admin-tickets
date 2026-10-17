# Ticket #003: Apache Web Server Troubleshooting

## Environment
- Operating System: Red Hat Enterprise Linux 9
- Service: Apache HTTP Server (httpd)
- Category: Service Management and Troubleshooting


## Problem Description

An employee reports that the company's internal website is not accessible.

The server uses Apache HTTP Server to host the website.

The Linux System Administrator must investigate the issue, identify the root cause, restore the service, and verify that the website is accessible.

## Tasks

1. Check the status of the Apache service.
2. Investigate service logs for errors.
3. Identify and fix the root cause.
4. Start Apache if it is stopped.
5. Enable Apache to start automatically at boot.
6. Test the website locally.
7. Verify that Apache is listening on the expected port.
8. Check firewall rules if remote access fails.

## Solution

### 1. Check Apache Service Status

    systemctl status httpd

### 2. Review Apache Logs

    journalctl -u httpd -n 50 --no-pager

### 3. Check Apache Configuration

    apachectl configtest

Expected output if the configuration is valid:

    Syntax OK

### 4. Start Apache and Enable It at Boot

    systemctl enable --now httpd

### 5. Test the Website Locally

    curl -I http://localhost

Expected response if the HTTP request succeeds:

    HTTP/1.1 200 OK

### 6. Check Listening Ports

    ss -tlnp | grep :80

### 7. Check Firewall Configuration

    firewall-cmd --list-services

If HTTP access is required and the firewall is blocking it:

    firewall-cmd --permanent --add-service=http
    firewall-cmd --reload

### 8. Verify the Website Again

    curl -I http://localhost
    systemctl is-active httpd
    systemctl is-enabled httpd

## Expected Results

- Apache is running.
- Apache starts automatically at boot.
- The Apache configuration is valid.
- The website responds successfully to local HTTP requests.
- Apache listens on the expected port.
- Firewall rules allow HTTP traffic when remote access is required.

## Troubleshooting Notes

If Apache fails to start, inspect the service logs before making changes.

If Apache is running but the website is inaccessible, investigate:

- Apache configuration errors
- Listening ports
- Firewall rules
- Network connectivity
- SELinux restrictions, when relevant

Do not assume that restarting the service fixes the root cause.

## Skills Practiced

- systemd Service Management
- Apache HTTP Server Administration
- Log Analysis
- HTTP Troubleshooting
- Firewall Configuration
- Network Diagnostics
- Service Verification

## Verification Evidence

Document the actual command outputs and test results after completing the lab.

Record the root cause, the corrective action, and the final verification results.

## Commit Message

Add Ticket 003 - Apache Troubleshooting