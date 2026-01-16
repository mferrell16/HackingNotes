# Commands Cheat Sheet (Practical)

## Identity
aws sts get-caller-identity

## IAM
aws iam get-user
aws iam list-groups-for-user
aws iam list-attached-user-policies
aws iam list-user-policies
aws iam get-policy-version

## S3
aws s3 ls s3://<bucket> --no-sign-request
aws s3 cp s3://<bucket>/file .

## EBS
aws ec2 describe-snapshots --owner-ids <account_id>
aws ec2 describe-snapshot-attribute --snapshot-id <id> --attribute createVolumePermission
aws ec2 create-volume --snapshot-id snap-xxxx --availability-zone us-east-1a

## Pacu
set_keys
run iam__enum_users
run iam__enum_roles
run iam__privesc_scan

## Trufflehog
trufflehog --regex --entropy=False repo

## git-secrets
git secrets --scan-history

## GoAWSConsoleSpray
GoAWSConsoleSpray -a <account_id> -u users.txt -p passwords.txt
