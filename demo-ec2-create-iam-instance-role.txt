## DEMO - Using EC2 Instance Roles
Create an EC2 Instance Role, apply it to an EC2 instance and learn how to interact with the credentials this generates within the EC2 instance metadata.

Steps:
1. 1 click deploy
2. EC2 > instance connect > EC2 Instance Connect > test command `aws s3 ls` > need creds
3. Create IAM Role > IAM > Roles > Create Role > Trust Entity, AWS service: select `EC2` > Next, Add Permissions, search `s3`, select AmazonS3ReadOnlyAccess > Next, Role name "A4LInstanceRole" > Create Role
4. Attach Role to Instance: EC2 > Right-click instance, Security: Modify IAM Role > Choose Role A4LInstanceRole
5. You can now `aws s3 ls` command in EC2 Connect because you have applied the IAM Role that has the S3ReadOnly permission to the EC2 instance
6. Clean up > IAM: Delete A4LInstanceRole > EC2: Security: Modify IAM, select NO IAM Role > CFN: Delete Demo stack
