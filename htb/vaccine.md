# HTB - Vaccine (Tier 2)
**Difficulty:** Very Easy  
**OS:** Linux

## Tools Used
- nmap
- ftp
- fcrackzip
- john (John the Ripper)
- sqlmap
- ssh
- vi

## Steps
1. Ran `nmap -sV <IP>` — found FTP (21), SSH (22), and HTTP (80) open
2. Logged into FTP anonymously and downloaded `backup.zip`
3. Cracked the ZIP password and extracted the files
4. Cracked the MD5 hash to recover the admin password
5. Logged into the web dashboard
6. Used `sqlmap --os-shell` to gain a shell as `postgres`
7. Read the user flag
8. Retrieved the `postgres` password from a configuration file
9. Logged in via SSH
10. Checked `sudo -l` and abused `vi` to get a root shell
11. Read the root flag

## What I Learned
- Anonymous FTP can expose sensitive backups
- Weak ZIP passwords and MD5 hashes can be cracked offline
- SQL injection can lead to remote code execution
- Configuration files may contain plaintext credentials
- Always check `sudo -l` for privilege escalation paths
- `vi` can be abused for privilege escalation when allowed via `sudo`
