
| Scenario | What to do |
|----------------|----------------|
| Found keys in code | Use `aws configure`, `sts get-caller-identity` |
| Found .env | Same as above |
| EC2 metadata | curl with IMDSv2 token |
| Public bucket | `aws s3 ls --no-sign-request` |
| EBS snapshot | `describe-snapshots` + `create-volume` |
| Brute force IAM principal | Pacu or GoAWSConsoleSpray |

Help

```
aws iam simulate-principal-policy \
  --policy-source-arn arn:aws:iam::<account-id>:user/<UserName> \
  --action-names <Action1> <Action2> \
  --resource-arns <ResourceARN>
```

can i assume role 
```
aws iam simulate-principal-policy \
  --policy-source-arn arn:aws:iam::123456789012:user/myuser \
  --action-names sts:AssumeRole \
  --resource-arns arn:aws:iam::123456789012:role/AdminRole

```

### **Avoid Detection with IAM Wildcards in Policies**

**Goal:** Evade CSPM tools (e.g., Prowler) that look for dangerous IAM actions
**Technique:**
- Instead of directly using dangerous actions like `iam:PassRole`, use **wildcard obfuscation**:

`"Action": [   "iam:P*Ro??",          // Bypasses strict string match   "lambda:CreateFunction" ]`

**Effect:**
- Maintains functional access to sensitive actions
- **Thwarts regex/static detection** used by many tools

### **CloudTrail Logging Evasion via Oversized IAM Policies**

**Goal:** Hide malicious IAM policies from CloudTrail logs
**Technique:**
- CloudTrail will **omit** the `policyDocument` field if its size exceeds ~102,401 characters.
- You can **bloat** the policy with whitespace (e.g., long descriptions, comments, or empty statements) to reach this threshold.

Command to check
```
cat too-large-iam-policy.json | wc -m
```