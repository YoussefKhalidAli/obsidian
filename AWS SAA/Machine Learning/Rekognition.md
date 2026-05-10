## What is Amazon Rekognition?

Amazon Rekognition is a **machine learning service** used to analyze:

- Images
- Videos

It can detect and identify:

- Objects
- People
- Text
- Scenes
- Activities

---

## Core Capabilities

### 1. Object & Scene Detection
- Identifies objects in images/videos
- Example:
  - Person
  - Bicycle
  - Dog
  - Mountain

---

### 2. Facial Analysis

Rekognition can analyze faces to detect:

- Gender
- Age range
- Emotions (happy, sad, etc.)
- Facial attributes (eyes open, smile, etc.)

---

### 3. Face Search & Verification

- Compare a face against a database
- Used for:
  - Authentication systems
  - Security applications

---

### 4. Celebrity Recognition

- Matches faces against a database of known celebrities

---

### 5. Text Detection (OCR)

- Extracts text from images/videos

Example:
- License plates
- Signs
- Numbers in races

---

### 6. Activity Detection (Pathing)

- Tracks movement in videos
- Example:
  - Sports analytics
  - Player movement tracking

---

## 7. Content Moderation (IMPORTANT)

### Purpose

Detects inappropriate or unsafe content in:

- Images
- Videos

### Examples of flagged content:

- Violence
- Explicit content
- Hate symbols
- Offensive material

---

### How It Works

1. Image/video is analyzed
2. Rekognition assigns a **confidence score**
3. You define a **Minimum Confidence Threshold**
4. If threshold is met → content is flagged

---

### Key Concept: Confidence Threshold

- Represents how confident Rekognition is in detection
- Lower threshold:
  - More detections (higher recall)
- Higher threshold:
  - More precise detections

---

### Use Cases

- Social media platforms
- Content filtering systems
- E-commerce platforms
- Media moderation

---

## 8. Human Review (A2I)

### Amazon Augmented AI (A2I)

- Adds **manual human review**
- Used after automated detection

Flow:
1. Rekognition flags content
2. A2I sends for human review
3. Final decision is made
