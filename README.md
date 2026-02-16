# lambda-ebs-volume-backup
Serverless AWS Lambda solution to automate EBS volume backups using snapshots and EventBridge scheduling across regions.

## Project Introduction:

This project demonstrates how to automate **Amazon EBS volume backups** using **AWS Lambda**. The Lambda function creates snapshots of EBS volumes and helps maintain data backups without manual intervention.

The solution uses **AWS Lambda**, **IAM Roles**, and **Amazon EventBridge** to create scheduled and event-based backups across multiple AWS regions.

This project provides hands-on experience with serverless automation in AWS.

---

## About Project:

The main goal of this project is to create a **serverless backup solution** that automatically takes snapshots of EBS volumes.

The workflow includes:

* Launching EC2 instances in two regions
* Creating AMIs and copying them across regions
* Creating additional EBS volumes
* Writing and deploying a Lambda function
* Assigning IAM permissions
* Configuring EventBridge for automation

This project demonstrates how to build a scalable and automated AWS backup system.

---

## Technologies Used:

* **AWS Lambda** – Serverless compute service to run backup code
* **Amazon EC2** – Virtual servers used for testing volumes
* **Amazon EBS (Elastic Block Store)** – Storage volumes to be backed up
* **Amazon AMI (Amazon Machine Image)** – Used for cross-region instance launch
* **IAM (Identity and Access Management)** – Role and permission management
* **Amazon EventBridge** – Used to schedule automated backups
* **Amazon Linux** – Operating system used for EC2 instances

---

## Step 1: Launch EC2 Instance (Primary Region):

1. Go to AWS Console → EC2
2. Launch Instance

   * AMI → Amazon Linux
   * Region → us-east-1
3. Deploy a simple static website (optional testing purpose)

---

## Step 2: Create and Copy AMI:

1. Create an AMI from the EC2 instance
2. Copy the AMI to another region (ap-south-1)
3. Launch a new EC2 instance in ap-south-1 using the copied AMI

---

## Step 3: Create Additional EBS Volumes:

1. In both regions:

   * Create a new EBS volume
   * Keep the state as **Available**

These volumes will be used for snapshot backup testing.

---

## Step 4: Create Lambda Function:

1. Go to AWS Console → Lambda
2. Click **Create Function**
3. Choose:

   * Author from scratch
   * Function name → `volume_backup`
   * Runtime → Python
4. Create the function

---

## Step 5: Add Backup Code:

Paste the EBS snapshot backup code inside the Lambda function.

Create a test event and run the function.

---

## Step 6: Troubleshooting:

### Issue 1: Timeout Error

* Error occurred during test execution
* Solution:

  * Go to Configuration → General Configuration
  * Edit Timeout → Set to **1 minute 30 seconds**
  * Save and test again

### Issue 2: Permission Denied

* Lambda did not have required EC2 permissions

---

## Step 7: Create IAM Role for Lambda:

1. Go to IAM → Roles
2. Create a new role for Lambda
3. Attach policy:

   * `AmazonEC2FullAccess`
4. Name the role:

   * `LambdaEc2FullAccess`

---

## Step 8: Attach Role to Lambda:

1. Go to Lambda → Configuration
2. Edit Execution Role
3. Select Existing Role
4. Choose `LambdaEc2FullAccess`
5. Save

Test the function again → ✅ Successful

---

## Step 9: Verify Snapshots:

1. Go to EC2 → Snapshots
2. Check snapshots in:

   * us-east-1
   * ap-south-1

Snapshots should be successfully created.

---

## Step 10: Automate Using EventBridge:

### Create Scheduled Rule

1. Go to Amazon EventBridge
2. Create Rule
3. Choose Schedule Pattern
4. Attach the Lambda function as Target

### Create Pattern-Based Rule

1. Create another rule
2. Choose Event Pattern
3. Select EC2-related events
4. Attach Lambda as Target

Now the backup process runs automatically.
