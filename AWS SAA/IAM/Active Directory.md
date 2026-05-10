Let’s break it down in a clean mental model.

---

## What is Active Directory (AD)?

On-premises Microsoft AD is a **central identity database** used in Windows environments.

It stores:

- Users (John, Alice…)
- Computers
- Groups
- Printers
- Permissions

And it works via a **Domain Controller**, where all logins are validated centrally.

So instead of each machine checking users locally, they all ask the domain controller:

> “Is this user allowed?”

---

## AWS Directory Services (AD in AWS)

AWS gives you 3 main ways to use AD in the cloud:

---

## AWS Managed Microsoft AD

AWS Managed Microsoft AD

### What it is:

A **fully managed Active Directory inside AWS**

### Key idea:

- AWS runs the domain controllers for you
- You can create users inside AWS AD
- Supports MFA
- Can connect (trust) with on-prem AD

### Best for:

✔ Enterprises wanting real AD in AWS  
✔ Hybrid setups (AWS + on-prem)

---

## AD Connector

AD Connector (AWS Directory Service)

### What it is:

A **proxy, not a real directory**

### Key idea:

- It does NOT store users
- It forwards login requests to your on-prem AD
- Think of it like a “login tunnel”

### Best for:

✔ You already have AD on-prem  
✔ You don’t want anything stored in AWS  
✔ Just want AWS to “use” your existing AD

⚠️ Important:

- No user management in AWS
- Just authentication forwarding

---

## Simple AD

Simple AD (AWS Directory Service)

### What it is:

A **basic AD-compatible directory inside AWS (not full Microsoft AD)**

### Key idea:

- Cheap and simple
- No advanced AD features
- No trust with on-prem AD

### Best for:

✔ Small setups  
✔ No existing AD  
✔ Basic Windows login needs

---

## How IAM Identity Center fits in

AWS IAM Identity Center

This is your **SSO layer (Single Sign-On)**.

It lets users:

- Log in once
- Access multiple AWS accounts
- Access cloud apps (SAML)
- Access EC2 Windows instances

---

## Identity flow (simple view)

User logs in → IAM Identity Center → gets access to:

- AWS accounts (via roles)
- Business apps (Salesforce, etc.)
- Windows EC2

But users come from:

- Built-in Identity Store OR
- Active Directory (via Directory Services)

---

## Permission Sets

Instead of IAM policies directly, Identity Center uses:

**Permission Sets**

Think of them as:

> “IAM policies + role templates for SSO users”

Example:

- Devs → Admin access in Dev accounts
- Devs → Read-only in Prod

Then AWS automatically:

- Creates IAM roles per account
- Lets users “assume role” after login

---

## Big comparison

|Option|Stores users?|On-prem integration|Type|
|---|---|---|---|
|Managed Microsoft AD|✅ Yes|✅ Yes (trust)|Full AD in AWS|
|AD Connector|❌ No|✅ Yes (proxy)|Bridge only|
|Simple AD|✅ Yes|❌ No|Basic AD|

---

## One-line memory trick

- **Managed AD** → “Real AD in AWS”
- **AD Connector** → “Just forwards to on-prem AD”
- **Simple AD** → “Lightweight standalone AD”