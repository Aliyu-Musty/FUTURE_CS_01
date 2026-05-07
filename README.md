## DVWA Security Assessment

I did this for a vulnerability assessment project. I tested DVWA on Kali Linux.

# Quick Summary

What I tested:** Damn Vulnerable Web Application (DVWA) - Low security level
Date: May 3-5, 2026
Environment: My Kali Linux lab machine

# Tools I Used

- Nmap - ran port scans, found open ports 80 and 3306
- OWASP ZAP - passive scan only (didn't want to break anything)
- Firefox DevTools - checked headers and cookies manually

# What I Found

| Risk     | Issue                    | Where                    |
| -------- | ------------------------ | ------------------------ |
| Critical | Command Injection        | `/vulnerabilities/exec/` |
| Medium   | Missing security headers | Every page               |
| Medium   | Cookie without HttpOnly  | `PHPSESSID`              |
| Low      | Server version visible   | HTTP responses           |

## The Worst One

Command Injection was the biggest problem. I typed `127.0.0.1; ls` into the ping box and it showed me the directory listing. That means an attacker could run ANY command on the server. Not good.

# How to Fix (Short Version)

*Do this now:*
- Stop using exec() and shell_exec() - validate inputs instead
- Add HttpOnly flag to the session cookie

*Do this soon:
- Add X-Frame-Options and CSP headers
- Hide Apache version number

# Files in This Repo

- `DVWA_Assessment_Report.pdf` - full report with screenshots
- `screenshots/` - proof of concept images
- `nmap/` - raw scan output
- `zap/` - ZAP alert list

# Notes

I learned that DVWA on "Low" security is really as bad as people say. Almost everything was broken. The good news is that most of these fixes are easy - just configuration changes.

*Made for my vulnerability assessment project.*
