# 🏦 Smart Finance Assistant – Design & Planning Document

---

# 🧠 STEP 1: Understand the Problem

## 🎯 Problem Statement

Many individuals have access to their financial transaction data through bank-exported CSV files, but struggle to interpret this raw data in a meaningful way. While the data contains valuable information, it does not clearly show spending patterns, financial habits, or areas for improvement.

This project aims to develop a **Smart Finance Assistant (Budget Buddy)** that transforms raw transaction data into clear summaries, meaningful insights, and actionable financial recommendations.

---

## 💡 Core Problems Being Solved

### 1. Lack of Spending Awareness

Users often do not realise how much they spend in specific categories such as dining, entertainment, or subscriptions.

**Solution:**
Analyse and summarise spending by category to improve visibility.

---

### 2. Difficulty Interpreting Raw CSV Data

Transaction data is not presented in a user-friendly or insightful format.

**Solution:**
Automatically clean and process the data into readable summaries.

---

### 3. No Meaningful Financial Insights

Users can see transactions but cannot easily identify patterns or trends.

**Solution:**
Generate insights such as top spending categories, frequent purchases, and unusual spending behaviour.

---

### 4. Lack of Actionable Financial Advice

Users may recognise overspending but do not know how to fix it.

**Solution:**
Provide clear, practical recommendations for improving spending habits.

---

### 5. Inefficient Cash Flow Management

Users struggle to balance income and expenses effectively.

**Solution:**
Help users understand spending patterns and make better budgeting decisions.

---

## ✅ Final Problem Summary

The Smart Finance Assistant will convert raw financial data into structured insights and recommendations, enabling users to track their spending, identify inefficiencies, and make better financial decisions.

---

# 📥 STEP 2: Identify Inputs and Outputs

## 📥 Inputs

### Data Inputs

* CSV file containing transaction data:

  * Date
  * Amount
  * Category
  * Description

### User Inputs

* Questions entered through the chat interface
* CSV file uploads
* Values entered into financial tools (e.g., savings goals)

### Knowledge Inputs (RAG System)

* Transaction summaries
* Financial guidance documents or budgeting rules

---

## 📤 Outputs

### Data Outputs

* Cleaned and validated transaction dataset
* Spending totals by category
* Average transaction values
* Transaction counts

### Insight Outputs

* Spending patterns and trends
* Highest spending categories
* Percentage breakdown of spending
* Identification of frequent small expenses

### Recommendation Outputs

* Suggestions for reducing spending
* Budgeting advice
* Financial improvement strategies

### System Outputs

* Chatbot responses (finance assistant personality)
* Results from custom tools (e.g., savings calculator)
* Visual or structured outputs in the Gradio interface

---

## 🔄 Data Flow

CSV File → Data Cleaning → Analysis → Insights → Recommendations → User Interface

---

# ✋ STEP 3: Work the Problem by Hand

## 📊 Example 1 – Normal Spending

| Date       | Amount | Category  | Description |
| ---------- | ------ | --------- | ----------- |
| 2024-08-01 | $50.00 | Groceries | Coles       |
| 2024-08-02 | $20.00 | Transport | Uber        |
| 2024-08-03 | $30.00 | Dining    | McDonald's  |

### Data Cleaning

* "$50.00" → 50.00
* "$20.00" → 20.00
* "$30.00" → 30.00

### Calculations

* Total Spending = 50 + 20 + 30 = **$100**
* Average = 100 ÷ 3 = **$33.33**

### Insight

Groceries is the highest spending category.

---

## 📊 Example 2 – Refund Handling

| Date       | Amount  | Category      | Description   |
| ---------- | ------- | ------------- | ------------- |
| 2024-08-01 | $100.00 | Entertainment | Concert       |
| 2024-08-02 | -$20.00 | Refund        | Ticket Refund |

### Data Cleaning

* "$100.00" → 100.00
* "-$20.00" → -20.00

### Calculations

* Total Spending = 100 - 20 = **$80**

### Insight

Refunds reduce total spending but should be tracked separately for better analysis.

---

## 📊 Example 3 – Frequent Small Expenses

| Date       | Amount | Category | Description |
| ---------- | ------ | -------- | ----------- |
| 2024-08-01 | $5.00  | Coffee   | Cafe        |
| 2024-08-02 | $5.50  | Coffee   | Cafe        |
| 2024-08-03 | $6.00  | Coffee   | Cafe        |

### Calculations

* Total = 16.50

### Insight

Small, frequent expenses can accumulate into significant spending.

---

## 📊 Example 4 – Messy Data (Edge Case)

| Date       | Amount  | Category  | Description |
| ---------- | ------- | --------- | ----------- |
| 2024-08-01 | $45.00  | Groceries | Coles       |
| 2024-08-02 | invalid | Dining    | Cafe        |
| 2024-08-03 |         | Transport | Bus         |

### Data Cleaning

* "$45.00" → 45.00
* "invalid" → NaN
* empty value → NaN

### Handling

* Remove rows with invalid or missing amounts

### Insight

Real-world financial data requires validation and cleaning before analysis.

---

# 📝 STEP 4: Write Pseudocode

## 🧩 Core System Logic

```
FUNCTION run_finance_assistant(csv_file):

    LOAD csv_file into DataFrame

    VALIDATE required columns:
        IF missing columns:
            RETURN error

    CLEAN data:
        - Remove dollar signs and commas
        - Convert Amount to numeric
        - Handle invalid or missing values

    REMOVE invalid rows

    IF dataset is empty:
        RETURN message

    SEPARATE:
        - positive spending
        - refunds (negative values)

    GROUP spending by Category

    CALCULATE:
        - total per category
        - average transaction
        - count of transactions
        - percentage of total spending

    SORT categories by highest spending

    GENERATE insights:
        - identify top categories
        - detect frequent purchases
        - highlight unusual spending

    GENERATE recommendations:
        - suggest reduction in high categories
        - highlight unnecessary expenses
        - provide budgeting advice

    RETURN formatted results
```

---

## 💬 Chat System Logic

```
USER asks a question

IF question relates to transaction data:
    RETRIEVE relevant data (RAG)
    GENERATE response using finance assistant personality

ELSE:
    PROVIDE general financial advice
```

---

## 🛠️ Custom Tool Logic (Savings Calculator)

```
FUNCTION calculate_savings_time(current_savings, monthly_saving, target_amount):

    remaining = target_amount - current_savings

    IF monthly_saving == 0:
        RETURN error message

    months_needed = remaining / monthly_saving

    RETURN months_needed
```

---

## 🌐 Gradio UI Logic

```
USER uploads CSV

SYSTEM:
    - cleans data
    - runs analysis
    - displays results

USER can:
    - view insights
    - ask questions (chat)
    - use tools

DISPLAY everything in a simple interface
```

---
