Amazon Forecast is a **fully managed machine learning service** that is used for **time-series forecasting** (predicting future values based on historical data).

---

## What it does

- Uses ML to predict **future trends**
- Example predictions:
    - Sales
    - Demand
    - Revenue
    - Resource usage

---

## Key Idea

Instead of manually analyzing historical data, Amazon Forecast:

- Automatically builds a forecasting model
- Improves accuracy using ML
- Reduces forecasting time from months → hours

---

## Common Use Cases

- Product demand planning (e.g., raincoat sales)
- Financial forecasting (revenue, costs)
- Workforce/resource planning
- Inventory management
- Traffic or usage prediction

---

## How Amazon Forecast Works

### 1. Input Data

You provide:

- Historical time-series data (core requirement)
- Optional additional features:
    - Prices
    - Discounts
    - Promotions
    - Website traffic
    - Location data

---

### 2. Data Storage

- Data is stored in **Amazon S3**

---

### 3. Model Training

- Forecast automatically:
    - Cleans data
    - Trains ML models
    - Builds forecasting engine

---

### 4. Prediction

- Output is a **future forecast**
- Example:
    - “Next year sales = $500,000”

---

## Key Characteristics

- Fully managed (no ML setup needed)
- Built specifically for **time-series forecasting**
- Uses historical patterns + extra features for accuracy
- More accurate than traditional statistical methods

---

## Key Point

If you see:

> forecasting, predicting future sales, demand planning

Think:

Amazon Forecast

---

## Summary Table

| Feature  | Description                    |
| -------- | ------------------------------ |
| Type     | Time-series forecasting        |
| Input    | Historical + optional features |
| Output   | Future predictions             |
| Use Case | Sales, demand, planning        |
| Setup    | Fully managed ML service       |