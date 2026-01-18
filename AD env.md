192.168.144.206 
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
![[Screenshot 2026-01-17 at 9.39.40 PM.png]]

Proof.txt 
![[Screenshot 2026-01-17 at 9.41.20 PM.png]]


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


![[Screenshot 2026-01-17 at 11.14.55 PM.png]]![[Screenshot 2026-01-17 at 11.21.20 PM.png]]
![[Screenshot 2026-01-17 at 11.31.01 PM.png]]

172.16.144.202 

![[Screenshot 2026-01-17 at 11.30.41 PM.png]]
Download scripts/tasks.vbs 

![[Screenshot 2026-01-17 at 11.33.15 PM.png]]
![[Screenshot 2026-01-17 at 11.34.09 PM.png]]
Bloodhound enumeration 
ls![[Screenshot 2026-01-17 at 11.35.30 PM.png]]

Got users from smb 
![[Screenshot 2026-01-17 at 11.39.59 PM.png]]
username dictionary attack to find matching user to discovered password. 
![[Screenshot 2026-01-17 at 11.42.28 PM.png]]

Shell as c.rogers 
![[Screenshot 2026-01-17 at 11.43.55 PM.png]]


![[Screenshot 2026-01-17 at 11.45.18 PM.png]]

DC = 172.16.144.200 

rogers user privleges ![[Screenshot 2026-01-17 at 11.49.37 PM.png]]

Rogers bloodhound json outputs show GenericAll 
Add himself to Domain Admin group in oscp.exam domain 
![[Screenshot 2026-01-17 at 11.55.19 PM.png]]
Login to 200 (DC) 
![[Screenshot 2026-01-17 at 11.56.08 PM.png]]
Proof.txt 
![[Screenshot 2026-01-17 at 11.56.56 PM.png]]