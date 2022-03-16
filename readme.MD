## Output format -
- json
- yaml
- text
- table
## Path of .aws in windows -
C:\Users\arghy\.aws
### C:\Users\arghy\.aws\config
```
[default]
region = ap-south-1
output = json
```
### C:\Users\arghy\.aws\config\credentials
```
[default]
aws_access_key_id = xxxx
aws_secret_access_key = xxxx+xxxx
```
## Add another config and credentials 
```
[default]
aws_access_key_id = xxxx
aws_secret_access_key = xxxx+xxxx

[arghya]
aws_access_key_id = xxxx
aws_secret_access_key = xxxx+xxxx
```
in config, we have a add **profile** before name. And name of config and credentials should be same.
```
[profile arghya]
region = ap-south-1
output = yaml
```
## When we use default config and credentials -
```
aws s3 ls
```
## When we use another config and credentials -
```
aws s3 ls --profile arghya
```
## Command structure of AWS CLI -
- aws = aws
- command = cloudformation ( We can compare command with resource name)
- subcommand = create-change-set
- [options and parameters] = --stack-name my-stack --change-set-name my-change-set
```
aws <command> <subcommand> [options and parameters]
aws cloudformation create-change-set --stack-name my-stack --change-set-name my-change-set
```
## To see all command / resources -
```
aws help
```
## To see all sub-command -
```
aws command/resource_name help
aws ec2 help
```
## To see all options and parameters -
```
aws command/resource_name help subcommand help
aws ec2 create-key-pair help
```
## To see each and everything - 
https://docs.aws.amazon.com/cli/latest/index.html

# Create EC2 Instance using CLI -
## Step 1 - creating key pair
### Creating Key_pair -
```
aws ec2 create-key-pair --key-name key_name --query 'KeyMaterial' --output text > key_name.pem
```
### To see key_pair -
```
aws ec2 describe-key-pairs --key-name key_name
```
### To delete key_pair -
```
aws ec2 delete-key-pair --key-name key_name
```
### To see all key_pair -
```
aws ec2 describe-key-pairs
```
## Step 1 - creating security group
### creating security group-
```
aws ec2 create-security-group --group-name my-sg --description "My security group" --vpc-id vpc-084b6ab5c7f8733f7
```
### see this security group -
```
aws ec2 describe-security-groups --group-ids sg-903004f8
```
### see all security groups -
```
aws ec2 describe-security-groups
```
### inbound port to security group -
```
aws ec2 authorize-security-group-ingress --group-id sg-903004f8 --protocol tcp --port 22 --cidr x.x.x.x
```
### delete security group -
```
aws ec2 delete-security-group --group-id sg-903004f8
```
## Step 3 - create instance 
### creating instance - 
```
aws ec2 run-instances --image-id ami-04893cdb768d0f9ee --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-0c24df9da61de93d3 --subnet-id subnet-0a60d15b8aa468535
```
### create tag -
```
aws ec2 create-tags --resources i-5203422c --tags Key=Name,Value=MyInstance
```
### delete ec2 instance -
```
aws ec2 terminate-instances --instance-ids i-5203422c
```
