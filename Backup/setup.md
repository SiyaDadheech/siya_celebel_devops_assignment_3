# to create the backup in AWS use the backup plan 
step 1: Step 1: Create a Backup Vault
Go to AWS Console → AWS Backup.

In the left menu, click Backup vaults → Create backup vault:  


> Name: MyBackupVlt

> Click Create backup vault.



Step 2: Create a Backup Plan
In AWS Backup, go to Backup plans → Create backup plan.

Choose: Build a new plan.
Name: PlanBackupDaily

Backup rule name: DailyBackupRule

Backup frequency: Daily

 Select custom time → Start time: 03:00 AM UTC

Backup vault: Choose MyBackupVault

Click Create plan  


Step 3: Assign EC2 Instance to Backup Plan
After creating the backup plan, click Assign resources.

Resource assignment name: e.g., AssignEC2VM

IAM role: Choose default or create one.

Resource type: EC2

Resource ID: Select your instance ID

Click Assign resources  

# to steup an alert using SNS

Step 4: Create an Alarm for CPU > 50%
> Go to CloudWatch → Alarms → Create Alarm.

Click Select Metric:

choose EC2 → Per-Instance Metrics → CPUUtilization

Select your instance

Define conditions:

Threshold type: Static

Whenever CPUUtilization is... Greater than 50

Set period (e.g., 5 minutes), evaluation periods (e.g., 2).



Step 5: Set Email Notification (SNS)
Under Notification, choose Create new topic:

Topic name: CPUAlert

Email address: xyz@gmail.com

After alarm is created, go to your mail inbox and confirm the subscription.

Now user backup will trigger automatically.
