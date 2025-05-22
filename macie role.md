# 1. Create a New AWS Account for Admin/Security Use
- You’ll want a dedicated account separate from your management account. Here’s how to create one:

- Steps to create a new AWS account:
- Go to the AWS Organizations Console.

- From the Management Account (the root account), click Accounts in the left-hand menu.

- Click Add account and choose Create an account.

- Enter details for the new account:

- Account name: e.g., Macie-Security-Admin

- Email address: Use a unique email for the account

- IAM role: You can optionally define an IAM role to be used for access to this account later.

- This account will be a new member of your organization.

# 2. Set Permissions for the New Account
- After creating the new account, you'll need to assign it appropriate permissions for AWS Macie administration.

- Create an IAM Policy for Macie Administration:
- Go to the IAM Console in your newly created account (Macie-Security-Admin).

- Go to Policies and click Create Policy.

- Under JSON, paste the following example policy that gives access to manage Macie:

```bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "macie2:*",
                "organizations:Describe*",
                "organizations:List*",
                "s3:ListBucket",
                "s3:GetObject"
            ],
            "Resource": "*"
        }
    ]
}
```

- This policy allows full Macie management actions across the organization.

- You can modify this policy if you want more restrictive access.

- Review and create the policy (e.g., MacieAdminPolicy).

- Attach the Policy to an IAM Role/User:
- In the same account, go to Roles and click Create role.

- Choose AWS service and select IAM as the trusted entity.

- Attach the MacieAdminPolicy you just created.

- Give this role a name, e.g., Macie-Admin-Role, and click Create role.

# 3. Assign the New Account as a Delegated Administrator
- Now that the new account has the appropriate IAM permissions, let’s make it the Delegated Administrator for AWS Macie:

- Go to the Macie Console from the Management Account (the root account).

- In the Macie Settings section, choose Accounts.

- Click Manage delegated administrators.

- Enter the 12-digit Account ID of your newly created account (Macie-Security-Admin).

- You can find the Account ID in the IAM Console or using the aws sts get-caller-identity CLI command.

- Click Enable trusted access.

- AWS will now assign the two service-linked roles for Macie to the new delegated admin account, which will allow it to manage Macie settings for the entire organization.

# 4. Review & Test
- Login to the new account (Macie-Security-Admin).

- Go to the Macie Console to ensure that the account now has the ability to manage Macie across all accounts in the organization.

- You can now use this account to:

- Enable Macie for individual accounts

- Manage Macie findings

- Set up data classification jobs
