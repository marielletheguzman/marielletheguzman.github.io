---
layout: post
title: "S3 MFA Delete Activity"
date: 2026-10-20 11:00:00 +0800
categories: [s3-mfa-activity-delete]
---

> **Today’s activity:** S3 MFA
> **Activity time:** 5-10 minutes

---

**We have created a sample S3 bucket for this activity**
*By default, MFA delete is disabled*

###For security purpose, you don't want anyone can delete your bucket so you must enable the MFA authenticator.

1. Open S3 bucket's property, then double check that MFA is disable.
![Bucket overview](/images/s3-demo-mfa-delete-maye-1.png.png)
  As of now, this can't be enable in UI so we need to change it in CLI.
![Edit Bucket Versioning](/images/s3-demo-mfa-delete-maye-2.png)

2. Open your root account then go to **My Security Credentials** then **Create Access Key**
![Create Access Key](/images/s3-demo-mfa-delete-maye-3.png)
  Take note of your key, this will be needed later.

4. Open CLI and then type **aws configure --profile root-mfa-delete-demo**
![Configure Profile](/images/s3-demo-mfa-delete-maye-4.png)
  AWS configure also known as **named profile** saves the name setup for the AWS CLI, it includes the default region, credentials, and output format. We can add settings there that can re-used.

```bash
aws s3api put-bucket-versioning --bucket s3-demo-mfa-delete-maye --versioning-configuration Status=Enabled,MFADelete=Enabled --mfa "arn:aws:iam::419676625334:mfa/Authapp 651027" --profile root-delete-mfa-maye-test
```
--bucket names the bucket.
Status=Enabled,MFADelete=Enabled turns on versioning and MFA Delete.
--mfa supplies the MFA device ARN and its current code.
--profile tells the CLI which saved credentials to use. The profile name is just a local label; the credentials it points to must be for the root account to enable MFA Delete.

Also ensure to add --mfa "arn:aws:iam::419676625334:mfa/Authapp **651027**" - the PIN Code from Auth app to avoid error with invalid arguments
![CLI command](/images/s3-demo-mfa-delete-maye-5.png)

To check if it was enabled:
```bash
aws s3api get-bucket-versioning --bucket s3-demo-mfa-delete-maye --profile root-delete-mfa-maye-test
```
![CLI command](/images/s3-demo-mfa-delete-maye-6.png)

5. Now go back to S3 bucket > Properties
![Enabled MFA](/images/s3-demo-mfa-delete-maye-7.png)
  We can now see that MFA is enabled

6. To check if it is working. Let's go to: 
<img width="1911" height="534" alt="image" src="https://github.com/user-attachments/assets/b030877e-5a8b-4738-9305-16e8372a6d91" />
  We will get an error in deleting this is because the MFA delete is enabled
<img width="1903" height="333" alt="image" src="https://github.com/user-attachments/assets/a15b504f-d415-4daa-9564-078678a05ebd" />

---
_With the use of S3 MFA, we can make our S3 secured and avoid unecessary deletion._


