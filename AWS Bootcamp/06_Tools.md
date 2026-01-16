# 🛠️ Tools (Detailed Setup)

## 📌 Pacu
Open-source AWS exploitation framework.
```bash
# Install
python3 -m pip install -U pacu
#start cli 
pacu 
# Inside Pacu
set_keys
help
run iam__enum_users
run iam__enum_roles
run iam__privesc_scan
run iam__enum_permissions 
run iam__enum_action_query --query iam:* 
```

# 📌 Prowler 
Compliance Testing Tool 
```
#setup profile 
aws configure --profile antonio
aws sts get-caller-identity --profile antonio

# list compliance checks 
prowler aws --profile name --list-compliances --no-banner 
# run cis aws 1.4 checks 
prowler aws --profile solaris1 --compliance cis_1.4_aws --region us-west-2 --no-banner
```



## 📌 Trufflehog
Scan repos for secrets.
```bash
pip install trufflehog
trufflehog --regex --entropy=False myrepo
trufflehog git https://github.com/myrepo.git
```

## 📌 git-secrets
Prevent secrets in commits.
```bash
git clone https://github.com/awslabs/git-secrets.git
cd git-secrets
make install
# Init for repo
git secrets --install
git secrets --register-aws
git secrets --scan-history
```

## 📌 GoAWSConsoleSpray
Password spraying AWS IAM console logins.
```bash
# Example
GoAWSConsoleSpray -a <account_id> -u users.txt -p passwords.txt
```

## 📌 ffuf
Fast web fuzzer. Useful for finding hidden files and directories.

```bash
# Install
git clone https://github.com/ffuf/ffuf
cd ffuf
go build
# Example
ffuf -w wordlist.txt -u http://target/FUZZ
```

## 📌 s3-account-search 
Obtain account id number from s3 bucket 
```
git clone https://github.com/RhinoSecurityLabs/s3-account-search.git
cd s3-account-search
python3 s3-account-search.py -b <bucket-name>
s3-account-search <role arn> <bucket-name> 
```
## 📌 aws-enumerator
Automates permission enumeration.

```bash
go install -v github.com/shabarkin/aws-enumerator@latest
~/go/bin/aws-enumerator cred #Setup 
~/go/bin/aws-enumerator enum -services all
~/go/bin/aws-enumerator dump -services secretsmanager
```

## 📌 CloudFox 

```
cloudfox aws all-checks #giant dump
cloudfox aws access-keys #map IAM users to key 
cloudfox aws secrets
cloudfox aws lambda 
cloudfox aws env-vars 
```
## 📌 AWSEye
AWSEye is an open-source AWS account reconnaissance tool.
https://awseye.com/ 

- Enumerates IAM users, roles, groups, policies, S3 buckets, CloudFormation, Lambda, and more.
- Useful for mapping permissions and finding attack paths.

**Install:**
```bash
git clone https://github.com/sa7mon/AWSEye.git
cd AWSEye
pip install -r requirements.txt
```

**Usage Examples:**
```bash
# Enumerate using a profile
python3 awseye.py --profile <profile>

# Enumerate with explicit keys
python3 awseye.py --access-key <ACCESS_KEY> --secret-key <SECRET_KEY> --region us-east-1
```


s3Scanner 
$ s3scanner -bucket-file names.txt -enumerate 


[https://github.com/DataDog/undocumented-aws-api-hunter/](https://github.com/DataDog/undocumented-aws-api-hunter/) 

[https://frichetten.com/blog/undocumented-amplify-api-leak-account-id/](https://frichetten.com/blog/undocumented-amplify-api-leak-account-id/) 