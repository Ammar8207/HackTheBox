# HTB - Fawn (Tier 0)
**Difficulty:** Very Easy
**OS:** Linux

## Tools Used
- nmap
- ftp

## Steps
1. Connected Kali VM to HTB network via OpenVPN
2. Ran nmap -sV on target IP — found port 21 (FTP) open
3. Connected using `ftp <IP>`
4. Logged in with username `anonymous`, blank password
5. Ran `ls` to list files, found flag.txt
6. Downloaded using `get flag.txt`, exited with `bye`
7. Read flag with `cat flag.txt`

## What I Learned
- FTP anonymous login is a common misconfiguration
- FTP transfers data unencrypted
