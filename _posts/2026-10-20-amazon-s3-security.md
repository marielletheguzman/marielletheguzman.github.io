---
layout: post
title: "Amazon S3 Security"
date: 2026-10-20 11:00:00 +0800
categories: [aws-s3-security]
cover: /images/amazon-s3.png
---

> **Today’s focus:** S3  
> **Study time:** 30 minutes

## What I thought about the topic before learning? 💭

🤔 I thought S3 was basically just a place to store static files. I didn’t realize it had so many security features.

## What I studied 📖
I studied about the following:
- S3 Encryption 
- CORS
- MFA Delete


## What I learned 🧠
S3 automatically encrypts new objects using SSE-S3 by default. Older objects aren’t automatically re-encrypted

**There are four server-side options and one client-side option:**
1. **SSE-S3** - This is S3’s default encryption. AWS manages the keys, so it’s a simple choice if you don’t want to manage them yourself. 😉
2. **SSE-KMS** - S3 still encrypts the file, but the key is managed through AWS Key Management Service (KMS). I can use a customer-managed key when I want more control over who can use it. 👍
3. **DSSE-KMS** - This applies two independent layers of encryption, which can help meet security or compliance requirements. It also adds some processing and cost. 🔐🔒
4. **SSE-C** - This option lets you provide and manage your own encryption key. S3 uses it to encrypt the file, so keep the key safe you’ll need it again to access the file. If you lose it, you may lose access to the file 📂

**S3 MFA Delete 🗑️
*Before this lesson, I hadn’t heard of S3 MFA Delete. I learned that it adds an extra check before someone can permanently delete a specific object version. It can also protect changes to the bucket’s versioning settings.*

>> It’s off by default, but that doesn’t mean everyone can delete files normal S3 permissions still decide who can

[S3 MFA Delete Activity](https://marielletheguzman.github.io/activity/s3-mfa-activity-delete/)▶️


## What confused me about CORS 😕
**The part that confused me was: if a website needs something from another website, why not just let every website use it?**❓
*Why CORS matters: Browsers try to stop one website from secretly reading information from another website. CORS lets a site choose which websites can use its response.* ❕
>> For public content, allowing every origin can be fine. For private data, allow only the websites that need it, and use permissions and sign-in checks to control access. 🔐

## Quick recap 🔃

## Next study session ⏭️
