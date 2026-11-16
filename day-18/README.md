# AWS Cloud Cost Optimization - Identifying Stale Resources

## Identifying Stale EBS Snapshots

In this example, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

### Description:

The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.

## Cloud Cost Optimization: Auto-Delete Unused EBS Snapshots with AWS Lambda

### Step 1: Launch an EC2 instance
![EC2 instance running](images/01-ec2-instance-running.png)

### EBS volume created and attached with the instance
![EBS volume attached](images/02-ebs-volume-attached.png)

### Step 2: Create and deploy the Lambda function (Python)
![Lambda function deployed](images/03-lambda-function-deployed.png)

### Step 3: Create a test event
![Lambda test event](images/04-lambda-test-event.png)

### Step 4: Create an IAM policy and attach it to the Lambda role
Permissions: `ec2:DescribeSnapshots`, `ec2:DeleteSnapshot`, `ec2:DescribeInstances`, `ec2:DescribeVolumes`

![IAM policy attached](images/05-iam-policy-attached.png)

### Test 1: Instance running, so the snapshot is retained
![Test 1 snapshot retained](images/06-test1-snapshot-retained.png)

### Test 2: Terminate the EC2 instance (its volume is deleted)
![EC2 instance terminated](images/07-ec2-instance-terminated.png)

### Orphaned snapshot still exists after the volume is gone
![Orphaned snapshot exists](images/08-orphaned-snapshot-exists.png)

### Lambda run: orphaned snapshot deleted
![Lambda deleted snapshot](images/09-test2-lambda-deleted-snapshot.png)

### Snapshots page after the run: no snapshots left
![No snapshots remaining](images/10-snapshots-empty.png)

### Test 3: Snapshot created from a standalone volume (no instance attached)
![Standalone volume snapshot](images/11-standalone-volume-snapshot.png)

