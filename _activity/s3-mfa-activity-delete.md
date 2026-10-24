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


##For security purpose, you don't want anyone can delete your bucket so you must enable the MFA authenticator.

1. Open S3 bucket's property, then double check that MFA is disable.
![S3 bucket MFA Delete setting](https://github.com/user-attachments/assets/d2cba54a-a54f-40fa-9063-aa68e4a23a31)
  As of now, this can't be enable in UI so we need to change it in CLI.

![S3 bucket MFA](https://github.com/user-attachments/assets/fc00eee7-30b9-4a50-960c-4176d16d10df)


3. Open your root account then go to **My Security Credentials** then **Create Access Key**
![My Security Credentials](https://github.com/user-attachments/assets/6a10fa0d-f3fd-4f31-9964-2602ea07714b)

  Take note of your key, this will be needed later.

4. Open CLI and then type **aws configure --profile root-mfa-delete-demo**
   ![aws configure](https://github.com/user-attachments/assets/21f8a4f5-164e-493f-b586-67c2c2a24ed9)

  AWS configure also known as **named profile** saves the name setup for the AWS CLI, it includes the default region, credentials, and output format. We can add settings there that can re-used.

```bash
aws s3api put-bucket-versioning --bucket s3-demo-mfa-delete-maye --versioning-configuration Status=Enabled,MFADelete=Enabled --mfa "arn:aws:iam::419676625334:mfa/Authapp 651027" --profile root-delete-mfa-maye-test
```
--bucket names the bucket.
Status=Enabled,MFADelete=Enabled turns on versioning and MFA Delete.
--mfa supplies the MFA device ARN and its current code.
--profile tells the CLI which saved credentials to use. The profile name is just a local label; the credentials it points to must be for the root account to enable MFA Delete.

Also ensure to add --mfa "arn:aws:iam::419676625334:mfa/Authapp **651027**" - the PIN Code from Auth app to avoid error with invalid arguments
   ![arn:aws:iam](https://github.com/user-attachments/assets/54c0483c-39d8-4475-9f83-57b4f1854c9f)


To check if it was enabled:
```bash
aws s3api get-bucket-versioning --bucket s3-demo-mfa-delete-maye --profile root-delete-mfa-maye-test
```
   ![enabled](https://github.com/user-attachments/assets/32bb2ea7-a6e2-43b0-bd66-ed5d9ce17e91)


5. Now go back to S3 bucket > Properties
   ![S3 bucket](https://github.com/user-attachments/assets/7b52e45a-c522-49cc-863b-34b412ee9870)

  We can now see that MFA is enabled

6. To check if it is working. Let's go to:
   ![working](https://github.com/user-attachments/assets/b030877e-5a8b-4738-9305-16e8372a6d91)
   
  We will get an error in deleting this is because the MFA delete is enabled
   ![enabled](https://github.com/user-attachments/assets/a15b504f-d415-4daa-9564-078678a05ebd)


---
_With the use of S3 MFA, we can make our S3 secured and avoid unecessary deletion._


