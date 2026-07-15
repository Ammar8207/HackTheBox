# HTB - Vaccine (Tier 2)
**Difficulty:** Easy
**OS:** Linux

## Tools Used
- nmap
- ftp
- zip2john
- john
- Browser
- sqlmap
- ssh
- vi

## Steps
1. Connected Kali VM to HTB network via OpenVPN
2. Ran `nmap -sV` on target IP — found ports 21 (FTP), 22 (SSH), and 80 (HTTP) open
3. Logged into FTP anonymously and downloaded `backup.zip`
4. Cracked the ZIP password using `zip2john` and `john`
5. Extracted the backup and found `index.php`
6. Recovered the web login info from the source file
7. Logged into the website as `admin`
8. Used `sqlmap` on the `search` parameter in `dashboard.php`
9. Got access as `postgres`
10. Checked `sudo -l` and found `vi` could be run as root
11. Used `vi` shell escape to become root
12. Read `/root/root.txt`

## What I Learned
- Anonymous FTP access can expose sensitive backup files
- Cracked backups and weak hashes can lead to valid credentials
- SQL injection after login can still be dangerous
- Misconfigured `sudo` permissions on `vi` can lead to full root access
