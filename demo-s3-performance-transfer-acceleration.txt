## DEMO S3 Performance
Enable Accelerated Transfer on an S3 bucket and review the AWS provided tool to complete Direct uploads vs Accelerated Transfer

Creat s3 bucket (no perids in name, DNS naming compatible) > name "testac3464576" > Create Bucket > new Bucket Properties tab > edit Transfer Acceleration, Enable > Save changes
- NOTE: When Transfer Acceleration is Enabled, an Accelerated endpoint address is provided. You need to use this endpoint to get the benefit of Accel. Transfers.
- To compare upload speeds: http://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html
