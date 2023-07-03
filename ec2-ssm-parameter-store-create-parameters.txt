## DEMO - Parameter Store
Create some Parameters in the Parameter Store and interact with them via the command line - using individual parameter operations and accessing via paths.

Steps:
1. Nav to Systems Manager in AWS Console > Parameter Store > Create parameter
2. Parameter 1 details: Name "/my-cat-app/dbstring" > value "db.allthecats.com:3306" > description "Connection string for cat app" > create
- the fwd slashes create hierarchy in Parameter Store 
3. Parameter 2: Name "/my-cat-app/dbuser" > value: "bosscat" > create 
4. Param 3 (secure): Name "/my-cat-app/dbpassword" > Type: SecureString > value: amazingsecretpassword1337 (encrypted)
5. Param 4: Name "/my-dog-app/dbstring" > value: "db.ifwereallymusthavedogs.com:3306"
6. Param 5: Name "/rate-my-lizard/dbstring" > value "db.thisisprettyrandom.com:3306"
7. CloudShell (top menu) > try these commands:
aws ssm get-parameters --names /rate-my-lizard/dbstring 
aws ssm get-parameters --names /my-dog-app/dbstring 
aws ssm get-parameters --names /my-cat-app/dbstring 
aws ssm get-parameters-by-path --path /my-cat-app/ 
aws ssm get-parameters-by-path --path /my-cat-app/ --with-decryption
8. Clean up: Select all params > Delete
