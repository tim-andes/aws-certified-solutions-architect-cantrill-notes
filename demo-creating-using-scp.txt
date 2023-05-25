## DEMO - Using Service Control Policies (SCP)
Update the structure within the organization, add hierarchy (Root, Dev OU, Prod OU) - and apply an SCP to the PRODUCTION account to test their capabilities
- Follows the same DENY-ALLOW-DENY IDP pattern

1. Create OU: Be in Admin account > AWS Organizations > check Root container box, "Actions: Create New" > Org Unit Name "PROD" > Create OU.
2. Create OU: Repeat above for DEV
3. Move relevant accounts to new OUs: check Production account, dropdown "Move" > Select respective OU (PROD/DEV) > Move AWS Account
4. Add SCP to Production Account: Switch Role: PROD > nav to s3 > Create Bucket > name (must be globally unique) "catpics3453451" > region: us-e-1 > upload attached photo (proving we have admin access)
5. Restrict with SCP. Switch Back > AWS Orgz > Policies > click SCP, enable SCP > Create Policy > copy .json text content from lesson file denys3.json > replace JSON with copied text > name "Allow All Except S3" > create policy
6. AWS Orgz > AWS Accounts > click PROD OU > tab "Policies" > Attach Allow All Except S3 Policy
7. Detach FullAWSAccess. AWS Orgz > Account PROD > tab "Policies" > select "attached directly" FullAWSAccess > Detach > Detach Policy
8. We reverted everything back to normal (re-attached Full Access policy to PROD OU, emptied s3 bucket, deleted s3 bucket
