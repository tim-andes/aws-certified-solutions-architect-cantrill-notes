## Demo - SSE-S3 - Object Encryption and Role Separation
Create an S3 bucket, and upload 3 images to the bucket using different encryption methods

1. Create S3 Bucket > name "catpics[random number]" > Create Bucket
2. Create Key: Nav to KMS > Create Key > Defaults > Alias "catpics" > Next > Don't set any Key Administrative Positions > Next > skip Key Usage Permissions > Finish
3. Upload SSE-S3 image: Back to S3 > catpics bucket > upload just sse-s3-dweez.jpg (must upload separate as we are configuring separate encryptions) > expand Properties accordian, Server-side encryption "Specify an en encryption key" > Encryption settings "Override bucket settings" > Encryption Key type "SSE-S3" > Upload
4. Upload SSE-KMS image w/ AWS managed default key: Upload see-kms-ginny.jpg > Properties > SSE - Specify an encrypt key > Override bucket settings > key type: SSE-KMS > Choose from your AWS KMS keys: choose the one ending "aws/s3", an AWS managed default key > Upload
5. Replace Step 4 Object, SSE-KMS image w/ KMS Generated Key: Upload see-kms-ginny.jpg > Properties > SSE - Specify an encrypt key > Override bucket settings > key type: SSE-KMS > Choose from your AWS KMS keys: alias "catpics" > Upload
6. Apply Deny policy on IAM, preventing KMS use > IAM Dashboard > Users > iamadmin > Permissions tab > Add Policy: Inline Policy > JSON tab > delete template > Paste in JSON provided in lesson > Review policy > name "denyKMS" > Create policy. Now you can open see-s3 image, but not the kms image. IAM > Remove DenyKMS
7. Set Default Bucket Encryption: catpics bucket > Properties tab > Default Encryption "edit" > key type: SSE-KMS > AWS KMS Key: Choose, "catpics"
8. Upload Default Merlin jpg with no encrypt settings: upload default-merlin.jpg without changing anything > Properties tab: Server-side encryption settings - see default stuff added from Step 7

EXAM: If you need to fully manage the keys used as part of S3 encryption process, you have to use SSE-KMS
