## DEMO Creating a Static Website with S3
 1. Create S3 Bucket > bucket name "[custom-globally-unique]" > uncheck "Block All Public Access" and acknowledge > Create Bucket
 2. Enable Static Website Hosting > access new bucket > Properties tab > scroll to bottom, Edit Static Website Hosting, Enable > Hosting Type: Static > Index Document "index.html" > Error Document "error.html" > In properties, scroll down and copy new static URL
 3. Upload some Objects to the bucket > Objects tab, "Upload" > Upload index.html, error.html, and "img" folder
 4. Paste copied URL into browser
 - You'll get a 403 Forbidden error (Access Denied) - Remember, S3 buckets are private by Default. We need to add permissions for anonymous/public users to visit site (no method to provide creds to S3)
 5. Give Permissions to un-authenticated uses to acess bucket > Access S3 bucket > Permissions tab > Bucket Policy > Edit > Grab JSON from .zip > Paste in, but replace the "Resource" value BEFORE the "/*" (mine now looks like "Resource":["arn:aws:s3:::top10catsever876.com/*"]) > Save
 6. You can now visit your website
 Extra: If you Registered a domain in R53, you can customize your URL. R53 > Hosted Zones > access your domain > Create Record > select Simple Routing > Record Name Eg. "top10".animals4life.io > choose Endpoint "Alias to S3 website endpoint" > Region: us-east-1 > S3 endpoint, select your bucket > click "Define simple record" > Create Records. Now Cantrill can go to top10.animals4life.io. Remember: Domain name and bucket name must match exactly to do this
 7. Clean Up: Empty bucket, delete bucket
 
 
Requirements for S3 bucket to operate as a website:
- Disable Block Public Access Settings
- Enable Static Web Hosting
- Set index/error documents
- Upload web files
- Add a bucket policy
