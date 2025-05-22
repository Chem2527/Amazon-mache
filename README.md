# Amazon-mache


## Pre-requisites:
- You need an AWS Organization with a Management (root) account and Member  accounts.

- Ensure that you have sufficient permissions to enable services on both root and member accounts.

### Steps to Enable Amazon Macie
- Step 1: Enable Amazon Macie in the Root Account (Management Account)
- Log in to the AWS Console with your root account (the AWS Organization's management account).

- Navigate to Amazon Macie:

- In the AWS Management Console, type "Macie" in the search bar and select Amazon Macie from the dropdown.

- Enable Macie:

- If this is your first time setting up Amazon Macie, click on "Enable"

- Note: Macie uses an IAM role to access your data. Ensure that the role is set up during this process.

- Configure the Settings:

 - After enabling Macie, choose the "Settings" tab from the Macie dashboard.

 - In the "discovery" section, you can choose to enable or disable sensitive data discovery

- Create a Discovery Job:

- Macie requires a discovery job to scan your S3 buckets for sensitive data. You can set it up now, or configure it later as needed.

- You’ll need to specify which S3 buckets to scan and the frequency of scans.

### Step 2: Enable Macie Across the AWS Organization
- To enable Macie in multiple accounts under your AWS Organization, you need to enable Amazon Macie Organization-wide using AWS Organizations.

- Go to AWS Organizations:

- Open the AWS Organizations service in the root account console.

- Enable Macie for the Organization:

 - In the AWS Organizations dashboard, go to “Services” and search for "Macie".

 - Select Macie and enable it for the entire organization.

 - Choose to enable it for all accounts (including Member), or select specific accounts.

- Configure Permissions:

 - AWS Organizations will create a delegated administrator in your organization to manage Macie settings for all accounts.

 - Once this is enabled, Macie will be active in the Member account as well.

### Step 3: Enable Macie in the Dev Account (if needed)
- Log in to the AWS Console with your Member account credentials.

- Navigate to Amazon Macie:

- In the search bar, type "Macie" and select it.

- Check the Status:

 - If you've enabled Macie through AWS Organizations, you should see Macie enabled in your Member account.

 - You may be prompted to configure settings like data classification and jobs.

- Create Discovery Jobs (Optional):

 - Set up discovery jobs in the Member account, specifying which S3 buckets to scan for sensitive data.

### Step 4: Verify Macie is Working
- Once Amazon Macie is enabled, you can verify that it's working by checking the following:

- Sensitive Data Discovery:

 - Macie will scan your S3 buckets for PII (Personal Identifiable Information) and other sensitive data.

 - In the Macie dashboard, you should see findings like PII discovered.

- Reports & Notifications:

 - Macie can generate findings based on the data it scans. You can set up notifications to alert you to these findings.

 - These findings can be sent to SNS topics or CloudWatch.

### Step 5: Automate Macie for Continuous Monitoring
To make the process automated:

- Configure Continuous Data Scanning:

 - Enable continuous data scanning on your S3 buckets to ensure Macie keeps monitoring data in real-time.

- Set Up CloudWatch Alarms:

 - Create CloudWatch alarms to trigger alerts when Macie detects sensitive data (such as PII).
