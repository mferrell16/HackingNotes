
```
nmap -p- -sC -sV -Pn IP 
-iL input -oN nmaps 
```
![[Screenshot 2026-01-16 at 3.49.31 PM.png]]
Credential checks 
![[Screenshot 2026-01-16 at 3.03.29 PM.png]]
```
nxc smb IP -u username -p password 
nxc rdp 
nxc winrm 
nxc ldap 
```

List users 
```
nxc command --users 
--pass-pol 
```

Check shares
```
smbmap -u '' -p '' -H <IP>
enum4linux -a IP 
```


Bloodhound 
- clone the repo to my host (`git clone https://github.com/dirkjanm/BloodHound.py.git`);
- `cd BloodHound.py` to go into that directory;
- checkout the CE branch with `git checkout bloodhound-ce`;
- install the repo as a standalone Python application using [pipx](https://github.com/pypa/pipx) by running `pipx install .`:
```
bloodhound-python 
```
