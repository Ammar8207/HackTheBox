# HTB - Oopsie (Tier 2)

**Difficulty:** Easy  
**OS:** Linux

## Tools Used
- nmap
- gobuster
- Firefox Developer Tools
- PHP reverse shell
- netcat
- Linux enumeration

## Steps
1. Connected Kali VM to the HTB VPN
2. Ran `nmap` and discovered:
   - Port **22** (SSH)
   - Port **80** (HTTP)
3. Enumerated directories with Gobuster and found `/cdn-cgi/login`
4. Logged in using the **Guest** account
5. Inspected and modified authentication cookies to gain admin access
6. Enumerated user accounts and identified the administrator's Access ID
7. Accessed the upload functionality
8. Uploaded a PHP reverse shell
9. Started a Netcat listener and triggered the uploaded shell to gain access as `www-data`
10. Upgraded the shell using Python PTY
11. Located `db.php` and extracted database credentials
12. Switched to the `robert` user with the discovered password
13. Enumerated SUID binaries and found `/usr/bin/bugtracker`
14. Exploited the vulnerable SUID binary to obtain root privileges
15. Retrieved both the user and root flags

## What I Learned
- Broken Access Control can allow privilege escalation by manipulating client-side data.
- Hidden web directories are often discovered through enumeration.
- Unrestricted file uploads can lead to remote code execution.
- Configuration files may expose sensitive credentials.
- Password reuse enables lateral movement between accounts.
- SUID binaries should be carefully audited because insecure command execution can lead to privilege escalation.
- PATH hijacking occurs when privileged programs execute commands without absolute paths.
