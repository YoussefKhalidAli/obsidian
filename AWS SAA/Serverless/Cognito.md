Amazon Cognito is a **serverless authentication and identity service** used to manage **users for web and mobile applications**.
**Explanation:** It provides **sign-in, authentication, and access control** for users _outside AWS_.

---

## 1. Core Concept

- Manages **application users (external users)**
- Provides:
    - Authentication (who you are)
    - Authorization (what you can access)

**Explanation:** Unlike IAM (for internal AWS users), Cognito is for **end users**.

---

## 2. Main Components (VERY IMPORTANT)

### 2.1 Cognito User Pools (CUP)
- User directory (database of users)
- Handles **authentication**

**Features:**
- Sign up / Sign in
- Email & password login
- MFA (Multi-Factor Authentication)
- Password reset
- Email/phone verification
- Social login (Google, Facebook, etc.)
**Explanation:** Acts like a **user database + auth system**.

---

### 2.2 Cognito Identity Pools (Federated Identities)
- Provides **temporary AWS credentials**
- Handles **authorization to AWS resources**
**Explanation:** Allows users to **access AWS services directly**.

---

## 3. User Pools Flow

User → Cognito User Pool → Token → Backend

Example:

User → Login → Token →  
→ Amazon API Gateway → AWS Lambda

**Explanation:**

- User authenticates
- Gets JWT token
- API Gateway validates token
- Backend receives user identity

---

## 4. Integration with ALB

User → Cognito →  
→ ALB (auth check) → Backend

**Explanation:**

- ALB handles authentication
- Backend receives verified user

---

## 5. Identity Pools Flow

User → Login (User Pool / Google / SAML) →  
→ Identity Pool → Temporary AWS Credentials → AWS Services

Example:

- Access Amazon S3
- Access Amazon DynamoDB

---

## 6. IAM Roles in Identity Pools

- Assign IAM roles to users
- Fine-grained permissions

**Example:**

- User can only access their own data

---

## 7. Row-Level Security (Important)

- Use IAM policies with conditions

**Example:**

- DynamoDB access restricted to:
    - User’s own items

**Explanation:** Enables **fine-grained access control per user**.

---

## 8. When to Use What

### Use User Pools when:

- You need **authentication**
- Login system (signup/signin)

---

### Use Identity Pools when:

- You need **AWS access**
- Users access S3, DynamoDB directly

---

### Use BOTH when:

- Authenticate users
- Then give them AWS permissions

---

## 9. Key Features

- Serverless user management
- Secure authentication (JWT tokens)
- Social login support
- MFA support
- Scalable to millions of users

---

## 10. Key Takeaways

- Cognito = **identity for external users**
- Two parts:
    - User Pools → authentication
    - Identity Pools → AWS access

---

## Key Points

- **Users outside AWS → Cognito**
- **Login system → User Pools**
- **Access AWS resources → Identity Pools**
- **API Gateway auth → User Pools**
- **ALB auth → User Pools**
- **Temporary AWS credentials → Identity Pools**
- **Fine-grained DynamoDB access → Identity Pools + IAM**
- **Mobile/web users → Cognito (NOT IAM)**