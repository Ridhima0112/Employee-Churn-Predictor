# 📊 Employee Attrition Analysis & Automation System

This project is an end-to-end HR Analytics solution that automates the collection of employee survey data, calculates flight-risk scores using a custom logic engine, and visualizes the results in a real-time dashboard.

## 🚀 Overview

The system bridges the gap between raw feedback and actionable HR insights by:
1.  **Automating Data Ingestion:** Monitoring survey entries via Google Sheets.
2.  **Scoring Risk:** Using a JavaScript-based weighted algorithm to identify high-risk employees.
3.  **Real-time Alerting:** Generating formatted alerts for immediate HR intervention.
4.  **Visual Analytics:** Providing a dashboard to track job satisfaction, career growth, and leave intent.

---

## ⚙️ Automation Workflow (n8n)

The workflow (`My workflow 7`) is built in **n8n** and consists of the following logic stages:

### 1. Data Trigger & Calculation
* **Google Sheets Trigger:** Polls for new survey responses every minute.
* **Risk Scoring Logic:** A custom JavaScript node evaluates five key dimensions to produce a `riskScore` (0-100) and a `riskLevel` (Low, Medium, or High).

### 2. The Weighted Scoring Algorithm
The `Calculate Risk Score` node applies the following weights:
| Factor | Condition | Risk Points |
| :--- | :--- | :--- |
| **Job Satisfaction** | Score ≤ 2 | +25 pts |
| **Manager Support** | Score ≤ 2 | +20 pts |
| **Work Hours** | 9+ hours/day | +10 to +20 pts |
| **Career Growth** | Response: "No" | +20 pts |
| **Leave Intent** | Score ≥ 4 | +15 pts |

### 3. Routing & Alerting
* **Conditional Routing:** If the `riskLevel` is "High" (score ≥ 60), the system triggers an alert.
* **Alert Formatting:** Generates a detailed message including the employee's email and specific survey results for context.<img width="1400" height="894" alt="Screenshot 2026-03-31 160641" src="https://github.com/user-attachments/assets/6493f9c8-807d-48c3-9839-cd215a791035" />


---

## 📈 Dashboard Insights

The associated dashboard provides a bird's-eye view of organizational health based on the processed data:

* **Average Job Satisfaction:** Currently sitting at **3.86**.
* **High-Risk Identification:** The dashboard highlights specific "High Risk" individuals (2 out of 7 total responses in the current dataset).
* **Career Growth Correlation:** A clear trend shows that employees who do not see career growth opportunities have significantly higher average risk scores.
* **Risk Level Distribution:** Visualized via a pie chart showing **29% High Risk** vs **71% Low Risk**.<img width="1374" height="761" alt="Screenshot 2026-04-01 111251" src="https://github.com/user-attachments/assets/fedcde5d-c3a2-4e77-8396-9f203a9ad67d" />


---

## 🛠️ Tech Stack

* **Automation Platform:** [n8n.io](https://n8n.io/)
* **Data Source:** Google Sheets
* **Logic Engine:** JavaScript (Node.js)
* **Visualization:** Power BI / Tableau

---

## 📂 Installation & Setup

1.  **n8n Workflow:**
    * Import the `My workflow 7 (1).json` file into your n8n instance.
    * Configure the **Google Sheets Trigger** with your own Spreadsheet ID and OAuth2 credentials.
2.  **Dashboard:**
    * Connect your BI tool to the output Google Sheet or database populated by the `Prepare Data for Storage` node.
    * Map the fields: `email`, `riskScore`, `riskLevel`, `jobSatisfaction`, `workHours`, and `leaveIntent`.

---

## 📝 License
Distributed under the MIT License.
