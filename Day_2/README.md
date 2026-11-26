# Day 2: Advanced Prompting, Few-Shot Classification, Structured JSON & Memory State

> **Drive Ready – AI Agents | One Person Company (OPC) Initiative**  
> *Department of Technical Training, Aditya University*

---

## Overview

Day 2 focuses on advanced prompt engineering, few-shot in-context learning for intent classification, structured JSON data extraction, and conversational memory management.

The tasks are implemented using **DukaanMitra AI – Smart Kirana Business Agent**, an AI-powered assistant designed to help kirana store owners manage inventory, monitor product demand, coordinate with suppliers, and improve business operations.

---

## Tasks Covered

### Task 1: Prompt Anatomy & Negative Constraint Enforcement

- **Implementation:** Developed a customized system prompt for DukaanMitra AI with business-specific instructions and safety rules.
- **Test Input:** `"Can my supplier deliver the required stock within one day?"`

- **Logic & Behavior:**
  - **Without Strict Rules:** The assistant may provide a general answer about supplier delivery without verifying actual delivery information.
  - **With Explicit Negative Rules:** The assistant avoids promising unverified delivery times and informs the owner when supplier information is unavailable.

- **Key Rules:**
  - Never invent stock quantities or supplier prices.
  - Never guarantee delivery times without verified information.
  - Never place purchase orders without store owner approval.

### Task 2: Few-Shot In-Context Intent Classification

- **Implementation:** Used few-shot prompting with three example message pairs to classify kirana business queries into three categories: `inventory`, `supplier`, or `sales`.

- **Few-Shot Exemplars:**
  - `"My shop has only 5 soap packets remaining."` → `inventory`
  - `"Which wholesale supplier offers the lowest price?"` → `supplier`
  - `"My biscuit sales increased this week."` → `sales`

- **Test Messages:**
  1. `"Which products are running low in my store?"` → `inventory`
  2. `"Can you compare prices from different suppliers?"` → `supplier`
  3. `"How can I increase my kirana store profits?"` → `sales`
  4. `"Some products are nearing their expiry dates."` → `inventory`
  5. `"How much stock should I reorder for next week?"` → `inventory`

- **Outcome:** Explored how few-shot prompting helps an LLM identify and categorize different kirana business queries without training a separate classification model.

### Task 3: Structured JSON Extraction & Sanitization

- **Implementation:** Developed a structured information extraction prompt that converts kirana store owner's messages into valid JSON.

- **Required JSON Keys:**
  - `store_name` – Name of the kirana store.
  - `product` – Product required.
  - `quantity` – Required product quantity.
  - `supplier` – Preferred supplier.
  - `required_date` – Expected delivery date.

- **Input Query:**

  `"My store name is Sri Lakshmi Stores. I need 50 soap packets from ABC Wholesale by 30 November 2026."`

- **Parsing Logic:**

```python
import json

cleaned = reply.removeprefix("```json").removeprefix("```").removesuffix("```").strip()

order = json.loads(cleaned)

print(order["product"], order["quantity"])
```

- **Expected Parsed Output:**

```json
{
    "store_name": "Sri Lakshmi Stores",
    "product": "soap packets",
    "quantity": 50,
    "supplier": "ABC Wholesale",
    "required
