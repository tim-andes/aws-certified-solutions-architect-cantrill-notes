## DEMO - Implementing an Organizational Trail (CloudTrail)
This CloudTrail will be configured for all regions and set to log global services events.
We will set the trail to log to an S3 bucket and then enhance it to inject data into CloudWatch Logs.

NOTE: You can create individual trails in accounts, but it's always more efficient to use an Organizational Trail.
NOTE: By default when you create a Trail, it creates a Trail for all AWS Regions in your account

EXAM: s3 bucket names MUST be GLOBALLY UNIQUE

1. iamadmin login > CloudTrail > Trails > Create trail > Trail name "Animals4lifeOrg" > check "Enable for all accounts in my org" > uncheck Enable under "Log file SSE-KSM encryption (use this in production, not in this practice) > Enable CloudWatch Logs > CW Logs Role name "CloudTrailRoleForCloudWatchLogs_Animals4Life" > Next > select Event types to log: check Management Events > Next > Review / Create trail
- After creating, can take some time for data to start appearing
2. Open the s3 link on the new Trail > move down through CloudTrail/ > View json.gz (can decompress with Chat GPT) to verify Trail is working
3. In new tab, nav to CloudWatch > Log Groups > Log Streams all in us-east-1
- Account ID is contained within Log Stream file name. 
- In Cloud Trail Event History, this will log Events for 90 days even if you have no Trail created. Trails allow you to customize what happens to the data

- In this demo, we created a Trail 1) to store data in s3 2) to put it into CloudWatch Logs 

NOTE: s3 charges based on storage. If CloudTrail is enabled, the logs will accumulate possibly past Free Tier
- To Avoid logging events and incurring charges: Go to Trails, "Stop Logging"
