## DEMO Cross-Region Replication of an S3 Static Website
Create 2 S3 buckets - one in N. Virginia, the other in N. California and configure Cross-Region Replication (CRR) between the two.

1. iamadmin account, N.VA region selected
2. Nav to S3 > Create Source Bucket > Create Bucket > name of source "sourcebucketta[random number]" > region us-east-1 > Create Bucket
3. Enable Static Website on Source > Properties Tab > Static website hosting: edit: Enable > type: static website > index doc "index.html"/error doc "index.html" > Save changes
4. Edit Source bucket Permissions for Public Access > Permissions tab > uncheck Block All Public Access > confirm > Save changes
5. To made Source Bucket public, add policy > Permissions tab > Bucket Policy "edit" > from lesson docs, paste JSON, replace Resource arn before the "/*" > Save
6. Create Destination Bucket & Set Permissions/Policy > Create Bucket > name of dest "destinationbucketta[random number]" > AWS Region: us-west-1 > uncheck Block All Public Access > Properties tab, Enable Static website hosting > Hosting type: static > index/error docs "index.html" > Save changes > Permissions tab, edit Bucket policy, paste JSON, update ARN, Save 
7. Enable Cross-Region Replication (CRR): Source Bucket Management tab > Create replication rule > Enable Versioning > Replication rule name "staticwebsiteDR" > Status "Enabled" > Choose Rule Scope: "Apply to All objects in the bucket" > Destination: Browse S3, find destination bucket, enable versioning > IAM Role: dropdown "create new role" > Create replication rule > Replicate Existing Obejcts? No (as we have no pre-existing objects)
8. Clean Up: Empty/Delete Destination Bucket > Empty/Delete Source Bucket > IAM: locate role staring with "s3crr_role[...]"
