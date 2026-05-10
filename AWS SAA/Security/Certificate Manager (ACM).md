AWS Certificate Manager (ACM) is a service used to **provision, manage, and deploy TLS certificates** in AWS.  
  
---  
  
## 1. What is a TLS Certificate?  
  
- Provides **encryption in transit (in-flight encryption)**  
- Enables **HTTPS** (secure communication between client and server)  
  
**Explanation:**  
When you see `https://`, it means data is encrypted using a TLS certificate.  
  
---  
  
## 2. Key Features of ACM  
  
- Provision **public and private TLS certificates**  
- **Free** public certificates (when issued by ACM)  
- **Automatic renewal** for ACM-issued certificates  
- Integrated with many AWS services  
  
---  
  
## 3. Supported Integrations  
  
ACM certificates can be used with:  
  
- Elastic Load Balancers (ALB, NLB, CLB)  
- CloudFront distributions  
- API Gateway  
  
**Important:**  
- Cannot directly use ACM certificates on **EC2 instances**  
- Public ACM certificates **cannot be exported**  
  
---  
  
## 4. Public Certificate Request Process  
  
### Step 1: Specify Domain Names  
- Fully Qualified Domain Name (FQDN): `app.example.com`  
- Wildcard domain: `*.example.com`  
  
---  
  
### Step 2: Choose Validation Method  
  
#### 1. DNS Validation (Recommended)  
- Add a **CNAME record** to your DNS  
- Can be automated (especially with Route 53)  
- Required for automatic renewal  
  
#### 2. Email Validation  
- AWS sends verification emails to domain contacts  
- Manual process  
  
---  
  
### Step 3: Wait for Validation  
- Certificate is issued after verification (can take minutes to hours)  
  
---  
  
### Step 4: Automatic Renewal  
- ACM renews certificates **automatically ~60 days before expiration**  
  
---  
  
## 5. Imported Certificates  
  
- You can import certificates created outside ACM  
  
**Limitations:**  
- No automatic renewal  
- Must manually replace before expiration  
  
---  
  
## 6. Monitoring Certificate Expiration  
  
### Option 1: EventBridge  
  
- ACM sends **daily expiration events**  
- Starts ~45 days before expiration (configurable)  
- Can trigger:  
- Lambda  
- SNS  
- SQS  
  
---  
  
### Option 2: AWS Config  
  
- Managed rule: `acm-certificate-expiration-check`  
- Detects expiring certificates  
- Sends non-compliance events to EventBridge  
  
---  
  
## 7. ACM with Load Balancers (ALB)  
  
- Attach TLS certificate to ALB  
- Enable HTTPS listener  
  
### Common Setup:  
- Redirect HTTP → HTTPS  
  
**Flow:**  
1. User accesses HTTP  
2. ALB redirects to HTTPS  
3. HTTPS uses ACM certificate  
4. Traffic forwarded to backend (e.g., EC2 via Auto Scaling)  
  
---  
  
## 8. ACM with API Gateway  
  
API Gateway supports 3 endpoint types:  
  
### 1. Edge-Optimized Endpoint  
- Uses CloudFront (global users)  
- Certificate must be in **us-east-1**  
  
**Explanation:**  
CloudFront only uses certificates from `us-east-1`.  
  
---  
  
### 2. Regional Endpoint  
- Clients in same region  
- Certificate must be in **same region as API**  
  
---  
  
### 3. Private Endpoint  
- Only accessible inside VPC  
- Uses resource policies  
- ACM not typically relevant here for public access  
  
---  
  
## 9. Custom Domain Setup (API Gateway)  
  
Steps:  
  
1. Create **Custom Domain Name** in API Gateway  
2. Attach ACM certificate  
3. Create DNS record (CNAME or Alias in Route 53)  
  
---  
  
## 10. Key Points  
  
- ACM manages TLS certificates for AWS services  
- Public certificates are **free and auto-renewed**  
- Use **DNS validation** for automation  
- Cannot use ACM directly on EC2  
- CloudFront certificates must be in **us-east-1**  
- Imported certs require **manual renewal**