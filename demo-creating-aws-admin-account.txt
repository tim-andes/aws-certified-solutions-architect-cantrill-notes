# DEMO: Creating the GENERAL AWS Account: https://learn.cantrill.io/courses/1820301/lectures/41301459

1. Create General AWS account (*MANAGEMENT). This account's root user will be what we log in with (root user = account specific).
2. Add root user MFA for security.
3. Create a Budget to protect against unintended costs.
4. Create an IAM user, IAMADMIN. Give permissions. Then we'll use this ID for the course.

## 1. Create General AWS account
- https://aws.amazon.com/resources/create-account/ - Root user email address (see TIP below), AWS account name
- Choose free tier AWS account after providing all account setup info (unique email, CC, verification).
- Complete the prompted steps. Account will now be created.

## 2. Add root user MFA for security
IAM Dropdown > Security Credentials > Assign MFA Device > follow steps
- Recommend using Google Authenticator app
Once, steps are complete, Log Out and test MFA login.

TIP: using one email for multiple accounts with Gmail. AWS accounts should be viewed as disposable, create as many as you need. Create a new account for each course. 
# TIP Example: email is catguy@gmail.com. You can use + sign in email address to create 'unique' email addresses. Ex: catguy+AWSAccount1@gmail.com, catguy+AWSAccount2@gmail.com, etc etc. This is called a Dynamic Alias.

## 3. Create a Budget to protect against unintended costs
AWS Free Tier: https://aws.amazon.com/free/
- Details allocations of free resources

Create Cost Budgets: click "Budgets" > select Use a Template > select an appropriate option based on monthly spend budget (select Zero spend budget) > Budget Name "Monthly Zero Budget", enter Email Recipients for alerts ([EMAIL]+trainingawsgeneral@gmail.com) > click "Create Budget"
-- Budgets allow you to monitor spend and configure alerts when hitting spend targets

## 4. Create an IAM user, IAMADMIN and give permissions
Search "IAM" > IAM Dashboard > Create user "iamadmin"
- Create an IAM user (2nd radial option, 1st option to be covered later), check "Provide user access to the AWS Management Console - optional"
- Select second radial option, Create IAM User: Custom PW
- Give admin permissions "Attach policies directly" > check "AdministratorAccess"
- Create user
- Test login by visiting alias URL
- Confirm login with profile dropdown that will show account name
- Secure admin account with OTP > Security Credentials > Assign MFA
- Log out and test OTP

# TIP: To set alias (make it globablly unique) 
Within IAM Dashboard, find right-side AWS Account info, find "Account Alias", click "Create".
- Must be a globablly unique ID. I am using "ta-cantrill-training-aws-general"
-- Now URL is https://ta-cantrill-training-aws-general.signin.aws.amazon.com/console
