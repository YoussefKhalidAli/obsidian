Amazon Comprehend Medical is a **specialized NLP service** designed to **analyze and extract information from medical text**.

---

## Core Idea

- Extension of **Amazon Comprehend**, but focused on **healthcare data**
- Processes **unstructured clinical text** → converts it into **structured insights**

---

## What It Analyzes

- Doctor notes
- Discharge summaries
- Test results
- Medical case notes

---

## Key Features

### 1. Medical Entity Extraction

- Identifies:
    - Medications
    - Dosage
    - Medical conditions
    - Procedures
    - Symptoms

---

### 2. PHI Detection (Protected Health Information)

- Detects sensitive patient data such as:
    - Names
    - Ages
    - Medical record details
- Uses:
    - **DetectPHI API**

---

### 3. Structured Output

- Converts raw clinical text into:
    - Organized entities
    - Relationships between data (e.g., medication + dosage + frequency)

---

## Integration Flow

### Common Architectures

1. **Batch Processing**
    - Store documents in S3
    - Call Comprehend Medical API
2. **Real-Time Processing**
    - Stream data via Kinesis Data Firehose
    - Analyze instantly
3. **Voice → Text → Medical Analysis**
    - Audio → Transcribe
    - Text → Comprehend Medical

---

## What It Does

- Input: Unstructured medical text
- Output:
    - Extracted entities
    - PHI detection
    - Structured healthcare insights

---

## Use Cases

- Clinical data analysis
- Electronic health records (EHR) processing
- Medical research
- Compliance (detect sensitive health data)

---

## Key Points

- Comprehend Medical = **NLP for healthcare**
- Extracts **medical insights from text**
- Detects **PHI (sensitive data)**
- Fully **managed and serverless**

---

## Summary Table

|Feature|Description|
|---|---|
|Type|Medical NLP|
|Input|Clinical text|
|Output|Structured medical data|
|Special Feature|PHI detection|
|Use Case|Healthcare analytics|

---

## Key Points

- Medical text + NLP → **Comprehend Medical**
- PHI detection → **Comprehend Medical**