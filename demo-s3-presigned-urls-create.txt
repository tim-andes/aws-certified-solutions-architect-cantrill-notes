## DEMO S3 Creating and using PreSigned URLs
 Create a bucket, upload an object and generate a presignedURL allowing access for any unauthenticated identities.
 
 1. Create bucket > name "animals4lifemedia[randomnumber]" > Create bucket 
 2. Upload object > all5.jpv to new bucket
 3. Generate PreSigned ULR > Cloud Shell (terminal icon top right of AWS) > shell command "aws s3 presign s3://animals4lifemedia745675/all5.jpg --expires-in 180"
 - 180 is in seconds, 3 mins
 4. Clean up: Empty/delete bucket
 
 NOTE: Interesting Aspects...
 1. Try "aws s3 presign s3://animals4lifemedia745675/all5.jpg --expires-in 604,800"
 2. Nav to IAM > Users > iamadmin > Permissions: Add inline policy, copy JSON from lesson > save
 3. In CloudShell, try "aws s3 ls", you'll see Access Denied. This Explicit Deny overrules S3 permissions. Refresh PreSigned URL and see that access is now denied as the current permissions of iamadmin are restricted from S3
 4. iamadmin currently restricted from S3, but can still generated a PreSigned URL for it, even with no access. 
 - You can also generate a PreSigned URL on a non-existent object
 - If you generate a PreSigned URL with an assumed Role, the URL will stop working with the temporary creds for the Role stop working
 - Can now create PreSigned URL from AWS Dashbord s3 > bucket > object > Object Actions dropdown "Share with a presigned URL"
