# Drive Ready – AI Agents | One Person Company (OPC) Initiative

> **Department of Technical Training, Aditya University**  
> *Hands-on Curriculum: Building AI Agents and LLM Applications for One Person Companies (OPC)*

---

## 📌 Repository Overview

This repository contains the practical coursework, source code, and implementation artifacts completed as part of the **Drive Ready – AI Agents | One Person Company (OPC) Initiative** conducted by the Department of Technical Training, Aditya University.

Throughout this program, we explore Large Language Models (LLMs), prompt engineering, API integration, few-shot learning, structured JSON extraction, conversational memory, and AI agent development.

As part of the practical implementation, we are developing **DukaanMitra AI – Smart Kirana Business Agent**, an AI-powered business assistant designed to help kirana store owners manage their daily business operations efficiently.

The project focuses on inventory management, stock monitoring, product demand analysis, supplier coordination, restocking recommendations, and business insights.

---

## 📂 Repository Structure

```text
YOUR_ROLL_NUMBER_DriveReady_OPC_2026/
│
├── README.md
│
├── Day-1/
│   ├── README.md
│   ├── Day1_Task.ipynb
│   └── Day1_Task_practice.ipynb
│
├── Day-2/
│   ├── README.md
│   ├── Day2_Task.ipynb
│   └── Day2_Task_practice.ipynb
│
└── Day-3/
    ├── README.md
    └── task.py
```

*Note: Add each day's files after completing the respective workshop tasks.*

---

## 🗓️ Curriculum & Day-by-Day Roadmap

| Day | Topic | Highlights & Practical Implementations |
|---|---|---|
| **Day 1** | LLM Foundations & Prompt Engineering | Groq API integration, system prompts, LLM question answering, business-specific chatbot development, and prompt safety concepts |
| **Day 2** | Advanced Prompting, Few-Shot & Memory | Negative constraint enforcement, inventory/supplier/sales classification, structured JSON extraction, function logging, and conversational memory |
| **Day 3** | Upcoming Workshop Tasks | Implementation and documentation will be updated after completing the assigned tasks |

---

## 🛠️ Global Tech Stack & Prerequisites

- **Programming Language:** Python
- **Development Environment:** Google Colab
- **LLM Provider:** Groq API
- **LLM Model:** Llama 3.3 70B Versatile
- **Frameworks & Libraries:**
  - Groq Python SDK
  - LangChain
  - Python JSON
  - Pandas (for future data processing)
  - Python Functions and Decorators

### Installation

```bash
pip install groq
pip install langchain langchain-core
```

### Environment Variable Setup

The project requires a Groq API key.

Configure the API key securely using Google Colab Secrets with the name `GROQ_API_KEY`.

```python
import os
from google.colab import userdata

os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
```

**Security Warning:** Never hardcode your API key or upload it to your public GitHub repository.

---

## 🏪 The OPC Business Context: DukaanMitra AI

### Project Name

**DukaanMitra AI – Smart Kirana Business Agent**

### Problem Statement

Small kirana store owners often face difficulties in managing inventory, tracking product demand, preventing stock shortages, identifying expired products, and coordinating with wholesale suppliers.

Manual business operations can lead to inefficient purchasing decisions, product wastage, and financial losses.

### Proposed Solution

DukaanMitra AI is an intelligent business assistant that helps kirana store owners make better business decisions using AI and data analysis.

### Core Features

1. **Inventory Management:** Monitor product availability and stock levels.
2. **Stock Monitoring:** Identify products running low on stock.
3. **Demand Analysis:** Analyse sales trends and identify fast-selling products.
4. **Expiry Management:** Identify products nearing their expiry dates.
5. **Restocking Recommendations:** Suggest suitable product replenishment quantities.
6. **Supplier Coordination:** Compare wholesale suppliers based on price, availability, and delivery time.
7. **Purchase Order Assistance:** Prepare purchase order recommendations with store owner approval.
8. **Business Insights:** Provide sales, profit, and business performance suggestions.

---

## 🤖 AI Capabilities Developed

Throughout the workshop, the following AI capabilities are explored and applied to DukaanMitra AI:

- **LLM Integration:** Connecting Python applications with Groq API.
- **Prompt Engineering:** Designing business-specific system prompts and instructions.
- **Few-Shot Classification:** Categorizing user queries into inventory, supplier, and sales-related requests.
- **Structured JSON Extraction:** Extracting product and purchase request details from natural language.
- **Conversational Memory:** Maintaining context across multiple user interactions.
- **Function Logging:** Tracking Python function calls using decorators.
- **Error Handling:** Managing API authentication, rate limits, and connection errors.
- **Business Assistance:** Providing practical suggestions for kirana store operations.

---

## 🚀 Running the Tasks

### Option 1: Run Locally

Navigate to the required day folder and execute the Python script.

```bash
# Navigate to Day-1
cd Day-1

# Run the Python script
python task.py
```

Repeat the process for other completed day folders.

### Option 2: Run in Google Colab

1. Open the required `.ipynb` notebook in Google Colab.
2. Configure the Groq API key using Colab Secrets.
3. Install the required Python dependencies.
4. Execute the notebook cells in order.
5. Test the DukaanMitra AI assistant using kirana business-related questions.

---

## 📈 Future Enhancements

- Multi-store inventory management.
- CSV-based sales and inventory data uploads.
- AI-powered product demand forecasting.
- Automated low-stock alerts.
- Supplier price and availability comparison.
- Purchase order generation and approval workflow.
- Daily business performance reports.
- Interactive dashboard for store owners and suppliers.

---

## 📜 Acknowledgements

Developed as part of the **Drive Ready – AI Agents | One Person Company (OPC) Initiative** at:

**Aditya University**  
Department of Technical Training (DoTT)

---

**DukaanMitra AI – Your Intelligent Partner for Smarter Kirana Businesses.**

*Learn. Build. Implement. Grow.*
