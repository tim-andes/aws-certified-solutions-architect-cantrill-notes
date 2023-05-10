# DEMO Creating Access Keys and Setting Up AWS CLI v2 Tools

Once logged in with Admin user:
IAM Dropdown > Security Credentials > scroll down to "Create Access Key", click > Command Line Interface (CLI) > check box at bottom > Next > Set Decription Tag > "Create Access Key"

Once Access Key is created, you can use Actions dropdown to Deactivate, Activate, and Delete. If you ever lose access to a key, you need to deactivate & delete it, then create a new one.

## Download AWS CLI v2 
AWS CLI v2 (Windows) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html

AWS CLI v2 (macOS) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html

AWS CLI v2 (Linux) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html

## Configure CLI
Configure a set of credentials which CLI will use to communicate with AWS. We will use the General IAMADMIN user for this one.

COMMAND: 'aws configure': configures default profile for CLI
COMMAND: 'aws configure --profile iamadmin-general' / 'aws configure --profile iamadmin-production': named profile for CLI

Upon entering the above Command:
- AWS Access Key ID
- AWS Secret Key
- Default Region Name: us-east-1
- Default output format (press Enter with blank field for default)

Test that this is successful with COMMAND 'aws s3 ls --profile [CLI profile name]'. This will error first as we need to specify named profile:
'aws s3 ls --profile iamadmin-general', which will currently return a blank string as there are no s3 buckets.

## Configure for Production
COMMAND: 'aws configure --profile iamadmin-production'
COMMAND to test: 'aws s3 ls --profile iamadmin-production'

SECURITY REMINDER: Never share your SECRET KEY. If leaked, delete and create new set of keys and re-configure in CLI

TIP: If after you Configure CLI with credentials, you can delete the credential files (CSVs)
