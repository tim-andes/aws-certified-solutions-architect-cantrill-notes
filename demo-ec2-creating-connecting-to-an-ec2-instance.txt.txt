### DEMO: Create an EC2 Instance
https://learn.cantrill.io/courses/1820301/lectures/41301621

1. Create SSH Key Pair: Navigate to EC2 Console (search bar) > left sidebar > Network & Security > Key Pairs) > click "Create Key Pair"
- Note: For creating key pair, Private key file format choises are .pem and .ppk. For MacOS/Linux, always use .pem, if using modern Windows you can choose .pem. Older Windows or Putty terminal app, choose .ppk
2. Configure: Left sidebar "Instances" > click "Launch Instances" > select O/S (Amazon Linux) > select keypair login (A4L) > Network Settings: select Create Security Group > name/description "MyFirstInstanceSG" > leave Inbound security groups rules as defaults > Launch EC2 Instance

## DEMO: Connect to Terminal of an EC2 Instance
1. In EC2 Dashboard, Right Click your EC2 instance, select "Connect" > SSH Client
2. Open your local Terminal / Command Prompt and change directories to wherever your SSH private file key is (likely Downloads, it's a .pem file created previously)
3. Copy the command at the bottom of the SSH Client tab "ssh -i "A4L.pem" ec2-user@ec2-54-89-175-122.compute-1.amazonaws.com", verify fingerprint with "yes"
- Note: If using MacOS/Linux and "Permission Denied": paste in terminal "chmod 400 A4L.pem"
- More key file permissions help: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html#connection-prereqs-private-key
