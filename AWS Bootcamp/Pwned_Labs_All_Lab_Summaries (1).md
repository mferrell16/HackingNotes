# ✅ Pwned Labs - One Page Lab Summaries

Below is a concise, high-level bullet point summary for each lab covered so far.

---

## 🔑 Lab 1: Intro to IAM Enumeration
- Logged in as IAM user.
- Verified identity with `sts get-caller-identity`.
- Listed groups, attached user policies.

## 🔑 Lab 2: S3 Enumeration Basics
- Found public bucket via website source.
- Listed & downloaded S3 objects.
- Extracted hardcoded AWS keys.

## 🔑 Lab 3: Identify AWS Account ID
- Found bucket name.
- Used `s3-account-search` to find AWS Account ID.
- Prepared for brute force IAM principal enum.

## 🔑 Lab 4: Loot Public EBS Snapshots
- Listed public snapshots.
- Created a volume from snapshot.
- Attached and mounted volume on EC2.

## 🔑 Lab 5: Unauthenticated IAM Enumeration
- Brute forced IAM user and role names.
- Assumed `Administrator` role using `sts:AssumeRole`.
- Gained privileged access.

## 🔑 Lab 6: Hunt for Secrets in Git Repos
- Cloned vulnerable repo.
- Used `git-secrets` and `trufflehog` to find secrets.
- Downloaded files with PII.

## 🔑 Session 1: Multiple Hands-On Labs
- Retrieved EC2 IAM creds from metadata.
- Identified account ID & snapshot.
- Brute forced IAM login with GoAWSConsoleSpray.

## 🔑 Lab 8: Assume Privileged Role with External ID
- Fuzzed files with ffuf, found config.json with creds.
- Verified identity & enumerated with aws-enumerator.
- Used `sts:AssumeRole` with External ID to access Secrets Manager.

## 🔑 Lab 10: IAM Policy Rollback
- Found creds in passwords.xlsx.
- Verified user had `SetDefaultPolicyVersion` permission.
- Rolled back policy to regain S3 list/get permissions.
- Downloaded a password-protected zip, cracked with JohnTheRipper.

## 🔑 Lab 11: Abuse OpenID Connect and GitLab
- Phished GitLab user and bypassed MFA.
- Exploited broad OIDC trust to assume AWS role.
- Looted S3 for backups and EC2 key.
- Pivoted to EC2, grabbed IMDSv2 keys.
- Accessed Secrets Manager with final keys.

---

Each lab illustrates a practical attack flow you can reference for future ops.

## 🔑 Session 2 Lab 1: Revealing IAM Permissions
- Found exposed .env file with AWS keys.
- Configured AWS CLI with found creds.
- Used `aws-enumerator` to brute-force permissions.
- Discovered Lambda permissions & API key in env vars.
- Downloaded Lambda function source code; found new AWS creds inside.

## 🔑 Session 2 Lab 2: Leverage OIDC for AWS Access
- Logged into a test machine using found creds.
- Used `github-oidc-checker` to find vulnerable OIDC trust for GitHub.
- Created private GitHub repo with workflow to assume the vulnerable role.
- Ran GitHub Actions workflow → minted OIDC token → assumed the AWS role.
- Listed bucket contents and exfiltrated `flag.txt`.
