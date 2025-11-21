# AWS Serverless Distance Calculator

---

## Overview

A serverless app on AWS.
It consists of a frontend hosted on **AWS Amplify**, that calls an **API Gateway endpoint** to trigger an **AWS Lambda function** then computes the geographical distance between two points.
Each request and result is logged to **DynamoDB**, using IAM-controlled access policies.

---

## Architecture Diagram

``` markdown
┌──────────────────┐
│  Amplify Hosting │  → Static HTML + JS (frontend)
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│   API Gateway    │  → Routes HTTP requests to Lambda
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│     Lambda       │  → Fast distance calculation logic
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│    DynamoDB      │  → Stores input/output + timestamp
└──────────────────┘
```

---

## AWS Services

### **1. AWS Amplify**

* Hosts a static frontend (`index.html`, CSS, JS)

### **2. AWS Lambda**

* Runs Python function that computes great-circle distance using the Haversine formula

### **3. Amazon API Gateway**

* Exposes RESTful API endpoint
* Integrates with Lambda using a `POST` method
* Handles CORS configuration for browser access

### **4. Amazon DynamoDB**

* Serves as a NoSQL database to persist user queries and results

### **5. AWS IAM**

* Manages least-privilege access between Lambda and DynamoDB
* Provides secure execution roles for Lambda functions

---

## Example Flow

1. **User** enters locations on the web interface, coordinates safely gotten from Geocoding API.
2. **Frontend** sends a POST request with coordinates to the API Gateway endpoint.
3. **API Gateway** triggers the **Lambda** function.
4. **Lambda** computes the distance and logs it to **DynamoDB**.
5. **Result** is sent back to the frontend and displayed instantly.

---

![GeoLink UI](/assets/geolink.png "Geolink UI")
