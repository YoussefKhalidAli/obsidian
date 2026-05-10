Amazon API Gateway is a **fully managed service** used to create, publish, and manage **APIs (REST, HTTP, WebSocket)**.

**Explanation:** It acts as a **front door** for applications, allowing clients to securely invoke backend services like Lambda.

---

## 1. Core Concept

Client → API Gateway → Backend (Lambda / HTTP / AWS Service)

**Explanation:** API Gateway handles the request, applies rules (auth, throttling, etc.), then forwards it to the backend.

---

## 2. Why Use API Gateway?

- Expose APIs without managing servers
- Built-in security (auth, IAM, Cognito)
- Request throttling & rate limiting
- API versioning & stages (dev/test/prod)
- Request/response validation
- Caching support

**Explanation:** Much more powerful than just exposing an HTTP endpoint.

---

## 3. Common Integrations

### 3.1 Lambda Integration (Most Important)

- API Gateway → AWS Lambda

**Use Case:**

- Fully serverless applications

---

### 3.2 HTTP Integration

- Connect to:
    - On-prem APIs
    - ALB endpoints

**Use Case:**

- Add API Gateway features (auth, throttling) on top of existing services

---

### 3.3 AWS Service Integration

- Directly integrate with services like:
    - Amazon SQS
    - Amazon Kinesis Data Streams
    - Step Functions

**Use Case:**

- Expose AWS services securely without giving credentials

---

## 4. Endpoint Types

### 4.1 Edge-Optimized (Default)

- Uses Amazon CloudFront
- Best for **global users**

---

### 4.2 Regional

- For users in the same region
- Can combine with your own CloudFront

---

### 4.3 Private

- Only accessible داخل VPC
- Uses VPC Endpoints

**Use Case:**

- Internal APIs

---

## 5. Security Options

### 5.1 IAM Authentication

- For internal AWS users

---

### 5.2 Cognito Authentication

- For mobile/web users
- Uses Amazon Cognito

---

### 5.3 Lambda Authorizer

- Custom authentication logic
- Uses AWS Lambda

---

### 5.4 HTTPS & Custom Domain

- Uses AWS Certificate Manager

---

## 6. Key Features

### 6.1 API Keys & Usage Plans

- Control access per client
- Enforce quotas

---

### 6.2 Throttling

- Prevent abuse
- Protect backend

---

### 6.3 Caching

- Cache responses
- Improve performance

---

### 6.4 Request Transformation

- Modify requests/responses
- Validate input

---

### 6.5 API Versioning & Stages

- dev / test / prod
- Safe deployments

---

## 7. Real-Time APIs

- Supports **WebSocket APIs**

**Use Case:**

- Chat apps
- Live updates

---

## 8. Example Architecture

Client → API Gateway → Lambda → DynamoDB

- API Gateway handles:
    - Auth
    - Validation
    - Routing
- Lambda handles:
    - Business logic
- DynamoDB stores:
    - Data

---

## 9. Key Takeaways

- API Gateway = **entry point for serverless apps**
- Works best with:
    - Lambda
    - DynamoDB

---

## Key Points

- **Expose Lambda → API Gateway**
- **Need auth + throttling → API Gateway**
- **Global API → Edge-Optimized**
- **Internal API → Private API Gateway**
- **Custom auth → Lambda Authorizer**
- **Mobile users → Cognito**
- **Direct AWS service access → API Gateway integration**
- **Need full serverless API → API Gateway + Lambda + DynamoDB**

---