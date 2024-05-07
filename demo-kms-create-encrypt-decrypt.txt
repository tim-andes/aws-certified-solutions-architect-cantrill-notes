## DEMO - KMS - Encrypting the battleplans with KMS
Run through the practical steps of creating and configuring a KMS Key, an Alias and we use that Key and the CLI tools to encrypt and decrypt some data

1. Generate KMS Key: Login to Mgmt/General Admin account > KMS > Create a key > Key Type: Symmetric > Next > create alias "catrobot" > Next > Define key admin permissions: check "iamadmin" (so iamadmin user can administer this key) > Next > Define key usage permissions: select "iamadmin" > Next > Review > Finish
2. Enable Key Rotation: Access catrobot key > Key Rotation tab > Check auto-rotate KMS key yearly, Save
3. Use Key / Create Battle Plan: access CloudShell (first icon on right-side main AWS menu, looks like Terminal icon) > Create plaintext battleplan:  || echo "find all the doggos, distract them with the yumz" > battleplans.txt ||
4. Encrypt message - Output will be the Encrypted not_battleplans.enc. Enter below lines into Shell
aws kms encrypt \
    --key-id alias/catrobot \
    --plaintext fileb://battleplans.txt \
    --output text \
    --query CiphertextBlob \
    | base64 --decode > not_battleplans.enc 
5. Receiver needs to Decrypt the cihpertext. Enter below lines into Shell:
aws kms decrypt \
    --ciphertext-blob fileb://not_battleplans.enc \
    --output text \
    --query Plaintext | base64 --decode > decryptedplans.txt
6. Clean Up: Select key > Key Actions: Schedule for deletion (waiting period 7-30 days, input 7) > Confirm > Schedule deletion 
