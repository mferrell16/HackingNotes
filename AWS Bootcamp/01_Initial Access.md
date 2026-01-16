# Initial Access (Detailed)

## ✅ Common Triggers
- Found AWS keys in zip/script (.env, git)
- Got temp credentials from EC2 metadata
- Discovered leaked keys in GitHub

## 🔑 Steps
1. Verify identity:
    ```bash
    aws sts get-caller-identity (loud)
    aws sns publish --message "whoami" --phone-number "1234567890" --region us-east-1 (can identify canaries)
    ```
2. If using new keys:
    ```bash
    aws configure
    aws configure --profile <name>
    # Set Access Key ID, Secret Key, default region
    ```
3. Check region for buckets:
    ```bash
    curl -I https://s3.amazonaws.com/<bucket>
    ```

## 🛠️ Tools used here:
- AWS CLI
- curl
- Pacu: `set_keys` command

## 🗂️ Example:
- Lab 1: IAM user credentials
- Session 1: Retrieved creds from EC2 metadata.
