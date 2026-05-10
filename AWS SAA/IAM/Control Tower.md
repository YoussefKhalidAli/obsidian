## What is AWS Control Tower?

AWS Control Tower
It is a **multi-account governance layer** built on top of:
AWS Organizations

### In simple terms:
Instead of manually building a secure multi-account structure, Control Tower:
- Creates accounts for you
- Applies security rules automatically
- Monitors compliance
- Gives you a dashboard

So it’s basically:

> “AWS Organizations + automation + security best practices pre-packaged”

---

## Why people use it

Control Tower helps you:

- Set up a multi-account AWS environment quickly
- Enforce company-wide security rules
- Monitor compliance centrally
- Avoid misconfigured accounts

Think:

> “Enterprise AWS landing zone in a box”

---

## Core concept: Guardrails

Guardrails = rules applied across all accounts in your organization.

There are 2 types:

---

## Preventive Guardrails

### What they do:
They **block bad actions before they happen**

### How they work:
They use:
AWS Organizations Service Control Policies (SCPs)

### Example:
- Only allow regions: `us-east-1`, `eu-west-2`
- Block everything else
So users literally CANNOT do disallowed actions

---

## Detective Guardrails

### What they do:
They **detect violations after they happen**

### How they work:
They use:
AWS Config

### Example:
- Find untagged resources
- Detect non-compliant configurations

Then they can:
- Send alerts via  
    Amazon SNS
- Trigger automation via  
    AWS Lambda

---

## Full flow (important mental model)

### Control Tower does:

1. Creates AWS accounts via Organizations
2. Applies SCP-based guardrails (preventive)
3. Deploys AWS Config rules (detective)
4. Monitors everything in a dashboard
5. Optionally auto-remediates issues

---

## Preventive vs Detective (exam favorite)

|Type|Purpose|Service used|Result|
|---|---|---|---|
|Preventive|Stop actions|SCP|Block|
|Detective|Detect issues|AWS Config|Alert / Fix|

---

## Easy way to remember

- **Control Tower = “AWS multi-account governance starter kit”**
- **Preventive = SCP = block**
- **Detective = Config = detect + alert**

---

## One-line trick

If you see:

- “multi-account setup + governance + best practices” → **Control Tower**
- “block regions / restrict actions across accounts” → **SCP (preventive guardrail)**
- “find non-compliant resources” → **AWS Config (detective guardrail)**