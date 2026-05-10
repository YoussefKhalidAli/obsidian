CORS is a **browser security mechanism** that controls whether a web application can make requests to a **different origin**.

## 1. What is an Origin?
An **origin** is defined by:
- **Protocol (Scheme)** → HTTP / HTTPS
- **Host (Domain)** → example.com
- **Port** → 80, 443, etc.

### Example:
https://www.example.com
- Protocol: HTTPS
- Domain: www.example.com
- Port: 443 (default for HTTPS)

---

## 2. Same Origin vs Different Origin

### Same Origin (Allowed by default)
- Same protocol
- Same domain
- Same port
### Different Origin (Blocked by default)
- Different domain
    - example:
        - [www.example.com](http://www.example.com)
        - api.example.com
- Different protocol (HTTP vs HTTPS)
- Different port

---

## 3. Why CORS Exists

Browsers block cross-origin requests by default to prevent:
- Data theft
- Unauthorized API calls
- Malicious scripts accessing other sites

CORS allows servers to **explicitly permit** these requests.

---

## 4. How CORS Works
### Step 1: Request from Browser
- Browser sends request to another origin
- Includes:
    Origin: https://www.example.com

### Step 2: Preflight Request (OPTIONS)
Browser sends a **preflight request**:
- Method: `OPTIONS`
- Asks server:
    - Which methods are allowed (GET, POST, etc.)
    - Which origins are allowed

### Step 3: Server Response

Server responds with headers like:

Access-Control-Allow-Origin: https://www.example.com  
Access-Control-Allow-Methods: GET, POST

### Step 4: Actual Request

- If allowed → browser proceeds with request
- If not allowed → request is blocked

---

## 5. Key Header

### Access-Control-Allow-Origin
Controls which origins can access the resource:
- Allow specific origin:
	`Access-Control-Allow-Origin: https://www.example.com`
- Allow all:
	Access-Control-Allow-Origin: *`

---

## 6. CORS in Amazon S3

Used when:
- A web app hosted in one S3 bucket
- Requests resources from another S3 bucket

### Example Scenario
- Bucket 1 → hosts website (HTML)
- Bucket 2 → stores images/assets

Browser loads:
- HTML from Bucket 1
- Images from Bucket 2 (different origin)

### Problem
- Browser blocks request to Bucket 2
### Solution

Configure **CORS on Bucket 2**
Example CORS configuration:
[  
  {  
    "AllowedOrigins": ["*"],  
    "AllowedMethods": ["GET"],  
    "AllowedHeaders": ["*"]  
  }  
]

---

## 7. Important Notes
- CORS is enforced by **browsers only**
- Servers can still communicate without CORS
- Missing CORS config → browser blocks request

---

## 8. Key Takeaways
- CORS controls **cross-origin requests**
- Origin = protocol + domain + port
- Different origin → blocked by default
- Must allow via **Access-Control-Allow-Origin**
- In S3:
    - Required when accessing resources across buckets
    - Configured using **CORS policy**