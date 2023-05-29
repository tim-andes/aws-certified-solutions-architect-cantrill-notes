## DEMO S3 Versioning
This lesson looks at a 'Animal of the week' website, and how to use versioning to recover when objects are changed and deleted accidentally or intentionally.

1. Create new S3 Bucket: Login to Mgmt/General Admin account > S3 > Buckets > Create Bucket > name [unique] "acbucket23425" > uncheck Block Public Access > Enable Bucket Versioning > Create Bucket
2. Enable Static Hosting: New bucket > Properties tab > Enable Static Website Hosting (bottom of page) > Index doc "index.html" > error doc "error.html" > Save changes
- REMEMBER: Just enabling Static Website Hosting is insufficient, you also need to add a Bucket Policy
3. Add Policy: Access new bucket > Permissions tab > edit Bucket Policy > copy text from bucket_policy.json (from demo .zip) > paste in json, edit Resource to look like " "Resource": "arn:aws:s3:::acbucket23425/*" ", except with your copied Bucket ARN instead
4. Upload files: acbucket > Upload > file "index.html" and folder "img" > click Upload
5. Versions: acbucket > Objects tab > toggle Show Versions > access winkie.jpg > Upload > Add Files > version 2/winkie.jpg > Upload > Access winkie.job object and see multiple versions if "Show versions" toggle is enabled
6. Delete Marker: Untoggle Show Versions within winkie.jpg Object > select winkie.jog > Delete > toggle on Show Versions > see Delete Marker > select Delete Marker and Delete
7. Delete Latest Version to Perma-Delete: acbucket Objects > toggle on Show Versions > select Latest Version of winkie.jpg > Delete
- NOTE: Whenever working with specific Versions of an object, this permanently deletes and makes next most recent version the new Latest / Current Version
8. Clean Up: Empty acbucket > Delete acbucket

REMEMBER: Versioning Enabled can incur significantly higher costs than Versioing turned off.
