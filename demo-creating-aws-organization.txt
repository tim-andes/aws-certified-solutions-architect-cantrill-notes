## DEMO - AWS Organizations

Steps:
1. The GENERAL account will become the MANAGEMENT / MASTER account for the organisation
2. We will invite the PRODUCTION account as a MEMBER account and create the DEVELOPMENT account as a MEMBER account.
3. Finally - we will create an OrganizationAccountAccessRole in the production account, and use this role to switch between accounts.

1. Nav to AWS Organization > "Create an Organization"
2. In Incognito Window, log in to the Production Account admin, copy Account ID > back to General AWS Management Account window > "Add an AWS account" > Invite Existing Account > Paste in ID / add message > Send Invitation
3. In Production Admin account > nav to AWS Organizations > Invitations > Accept Invitation
4. Manually adding a Role to an invited account > In Prod account nav to IAM > Roles > Create Role > Type of Entity: AWS Account > get account ID of General AWS Org Account > select Another AWS Account > Paste Account ID > Add Permissions: AdministratorAccess > Next > name "OrganizationAccountAccessRole" > Create Role. In IAM > Roles >  OrganizationAccountAccessRole > Trust Relationships, you'll see the General Account ID referenced as a Trusted Entity
5. Role Switch: From General to Production Account. Copy Production ID > Main Dropdown "Switch Role" > click "Switch Role" > paste Prod ID > name of Role created "OrganizationAccountAccessRole" > Display Name "Prod" > select color Red > Create / Switch Role. You'll see Display name "Prod" on top right menu drop down. You can also SWITCH BACK

6. Create new Account within Org. AWS Orgz > Add Account > Create an AWS Account > name "OrganizationAccountAccessRole" > Create 
7. After new Account created, copy its account ID > dropdown Switch Role > switch to DEV role
