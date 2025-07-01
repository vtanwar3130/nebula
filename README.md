# nebula
DevSecOps Assignment


1. How do you rate yourself for writing scripts in Python (1–10)?
I would rate myself 8/10 in Python scripting.

I’m very comfortable with:

Writing modular and reusable code

Using Boto3 for AWS automation

Handling exception flows

Writing scripts for CI/CD, DevSecOps, and cloud automation

I’m always learning new idiomatic practices and improving testing and structuring for production readiness.

2. Have you used the Boto3 library before? What did you use it for?
Yes, I have extensively used the Boto3 library for automating AWS operations, especially around security, monitoring, and resource management.

Some key use cases:

GuardDuty: Enable detectors, list findings, suppress alerts.

IAM: Audit users, list roles and policies, identify unused credentials.

S3: Enforce encryption, remove public ACLs, automate backups.

EC2: Start/stop instances, enforce tagging policies.

CloudWatch: Create alarms for CPU, disk, and anomaly detection.

3. How do you validate if your API calls were successful in a script?
I use a combination of HTTP status code checks and exception handling.

Example:

python
Copy
Edit
response = ec2.describe_instances()
if response['ResponseMetadata']['HTTPStatusCode'] == 200:
    print("Call succeeded.")
else:
    print("Call failed.", response)
In production-grade scripts, I use try-except blocks to handle failures gracefully and to log AWS-specific error codes like AccessDenied, Throttling, etc.

4. How do you handle exceptions in Python? (Example using API calls)
I use try-except blocks, often catching ClientError from botocore.exceptions.

Example:

python
Copy
Edit
import boto3
from botocore.exceptions import ClientError

s3 = boto3.client('s3')

try:
    s3.create_bucket(Bucket='my-secure-bucket')
    print("Bucket created.")
except ClientError as e:
    print(f"AWS error: {e.response['Error']['Code']} - {e.response['Error']['Message']}")
except Exception as e:
    print("Unexpected error:", str(e))
finally:
    print("Execution complete.")
5. Have you automated any AWS native security services (e.g., GuardDuty, Macie)? If yes, please share details.
Yes, I have automated several AWS security services using Python + Boto3:

✅ GuardDuty Automation
Enabled GuardDuty detectors across all AWS accounts in an Org.

Listed and filtered high-severity findings (Severity > 7).

Auto-suppressed benign alerts using create_filter().

Triggered remediation via Lambda for EC2 instances flagged in findings.

✅ IAM Audit Scripts
Identified inactive IAM users and access keys (>90 days).

Scanned inline and managed policies for risky permissions.

Automatically disabled keys and notified admins via SNS.

✅ S3 Security Checker
Audited all buckets for:

Public access settings

Missing encryption

Missing versioning

Generated CSV reports and uploaded to a secure S3 bucket.

✅ (Optional) Macie (If you've done it)
If applicable:

Enabled Macie across regions

Configured classification jobs for sensitive data in S3

Automated alerting when PII was detected
