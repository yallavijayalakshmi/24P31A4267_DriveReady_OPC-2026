# Day 4: AI Agent Tools, Structured Output & Google Sheets Integration

> **Drive Ready – AI Agents | One Person Company (OPC) Initiative**  
> *Department of Technical Training, Aditya University*

---

## Overview

Day 4 focuses on developing tool-using AI agents with LangChain, implementing structured data validation using Pydantic, integrating Google Sheets for business data storage, and connecting Python functions with an AI agent.

As part of this practical work, these concepts are implemented using **DukaanMitra AI – Smart Kirana Business Agent**, an intelligent business assistant designed to help small kirana store owners manage inventory, monitor product availability, identify low-stock items, prevent product expiry and manage restocking requests.

Unlike a basic chatbot that only provides text responses, DukaanMitra AI uses Python tools to retrieve inventory information, perform calculations and record business requests.

---

## Tasks Covered

### Task 1: Understanding AI Agent Tools

**Implementation:**

Introduced the concept of LangChain tools and understood how an AI agent can use Python functions to perform specific business operations.

In DukaanMitra AI, tools are used for:

- Checking product prices.
- Checking available stock.
- Identifying low-stock products.
- Finding products nearing expiry.
- Recording restocking requests.

**Key Learning:**

Tools allow an AI agent to interact with external data and perform operations instead of relying only on information provided in its system prompt.

### Task 2: Creating Custom Tools Using LangChain

**Implementation:**

Created custom Python functions using the `@tool` decorator from LangChain.

The following tools were developed for DukaanMitra AI:

**1. get_price()**

Calculates the total price of a product based on its unit price and requested quantity.

**2. check_stock()**

Retrieves the available quantity of a product from the Google Sheets inventory.

**3. check_low_stock()**

Identifies products whose available stock is below or equal to a specified threshold.

**4. check_expiry()**

Identifies products that are approaching their expiry dates within a specified number of days.

**5. log_restock_request()**

Validates and records a restocking request in a separate Google Sheets worksheet.

**Key Learning:**

- The `@tool` decorator converts Python functions into LangChain tools.
- Function names and descriptions help the agent understand when to use each tool.
- Type hints and docstrings make tool usage clearer.
- Python functions perform the actual operations when invoked by the agent.

### Task 3: Structured Output and Data Validation Using Pydantic

**Implementation:**

Used Pydantic to define and validate structured restocking request data.

Created a `RestockRequest` model with the following fields:

| Field | Description |
|---|---|
| `product_name` | Name of the product to reorder |
| `quantity` | Number of units required |
| `supplier` | Wholesale supplier name |
| `required_date` | Requested delivery date |

Example implementation:

```python
from pydantic import BaseModel, Field

class RestockRequest(BaseModel):
    """A restocking request for a kirana store."""

    product_name: str = Field(
        description="Name of the product"
    )

    quantity: int = Field(
        description="Quantity to reorder",
        ge=1
    )

    supplier: str = Field(
        description="Supplier name"
    )

    required_date: str = Field(
        description="Required delivery date"
    )
```

**Key Learning:**

- Pydantic defines the expected structure of business records.
- Field descriptions explain the purpose of each value.
- Validation rules help prevent invalid data from being stored.
- The `ge=1` constraint ensures that the requested quantity is at least one.

### Task 4: Google Sheets Integration Using gspread

**Implementation:**

Integrated Google Sheets with Python using the `gspread` library to store and retrieve kirana inventory information.

Created a spreadsheet named:

`DukaanMitra Inventory Management`

The inventory worksheet contains the following fields:

| Column | Purpose |
|---|---|
| `product_name` | Product name |
| `category` | Product category |
| `quantity` | Available stock |
| `unit_price` | Price per unit |
| `supplier` | Supplier name |
| `expiry_date` | Product expiry date |
| `last_updated` | Last inventory update |

A separate worksheet named `Restock Requests` is used to record restocking requests.

Its fields include:

- Product name
- Requested quantity
- Supplier
- Required date
- Request status

**Important Operations:**

- `gc.create()` – Creates a new Google spreadsheet.
- `gc.open()` – Opens an existing spreadsheet.
- `sh.sheet1` – Accesses the first worksheet.
- `ws.get_all_records()` – Retrieves inventory records.
- `ws.append_row()` – Adds a new record to the worksheet.

**Key Learning:**

Google Sheets can act as a simple business data storage system for a prototype. Python can retrieve and update records using the gspread library.

### Task 5: Creating the DukaanMitra AI Agent with Tools

**Implementation:**

Created a tool-using AI agent using LangChain's `create_agent()` function.

Connected the following tools to the agent:

```python
from langchain.agents import create_agent

tools = [
    get_price,
    check_stock,
    check_low_stock,
    check_expiry,
    log_restock_request
]

agent = create_agent(
    model=llm,
    tools=tools,
    system_prompt=SYSTEM
)
```

**Agent Responsibilities:**

- Understand questions from kirana store owners.
- Select the appropriate tool based on the request.
- Retrieve inventory information from Google Sheets.
- Provide product price and stock information.
- Identify low-stock and near-expiry products.
- Help manage restocking requests.
- Communicate results in simple language.

**Key Learning:**

The agent can decide which registered tool to call based on the user's request. The tool executes the Python operation, and its result is returned to the agent to prepare a response.

### Task 6: Conversation Memory and Agent Interaction

**Implementation:**

Implemented conversation memory using a message history list.

```python
history = []

def chat(text: str) -> str:
    global history

    try:
        result = agent.invoke({
            "messages": history + [
                {"role": "user", "content": text}
            ]
        })

        history = result["messages"]

        return history[-1].content

    except Exception as e:
        print("Agent error:", e)
        return (
            "Sorry, DukaanMitra AI is temporarily unavailable. "
            "Please try again."
        )
```

**Key Learning:**

- The `chat()` function accepts user messages.
- `agent.invoke()` executes the agent.
- The complete message history is maintained between interactions.
- The latest message contains the agent's final response.
- Error handling provides a user-friendly response when execution fails.

### Task 7: Restocking Request Management

**Implementation:**

Created a restocking workflow to help kirana store owners record products that need replenishment.

The workflow includes:

1. The owner identifies a product that needs restocking.
2. DukaanMitra collects the product name, quantity, supplier and required date.
3. The agent checks whether the required information is available.
4. The owner must explicitly approve the request.
5. The `log_restock_request()` tool validates the request using Pydantic.
6. The request is recorded in the Google Sheets `Restock Requests` worksheet.
7. The agent confirms the recorded request and its status.

**Example Interaction:**

Owner: "I want to restock 50 soap packets from ABC Wholesale by 30 November 2026."

DukaanMitra AI: "I have prepared your restocking request for 50 soap packets from ABC Wholesale. Shall I record this request?"

Owner: "Yes, approve it."

DukaanMitra AI: Confirms the request after it has been successfully recorded.

**Key Learning:**

Business operations involving records should be validated before saving. Owner approval is important before recording a restocking request.

---

## Tech Stack & Setup

### Technologies Used

- Python
- Google Colab
- LangChain
- LangChain Groq
- Groq API
- GPT-OSS-20B model
- Pydantic
- Google Sheets API
- gspread
- Google Authentication

### Required Libraries

```bash
pip install -q langchain langchain-groq gspread pydantic
```

### Environment Setup

Configure the Groq API key using Google Colab Secrets.

```python
import os
from google.colab import userdata

os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
```

### Initialize the Language Model

```python
from langchain_groq import ChatGroq

llm = ChatGroq(
    model="openai/gpt-oss-20b",
    temperature=0.2,
    max_retries=3
)
```

### Google Sheets Authentication

```python
from google.colab import auth
auth.authenticate_user()

import gspread
from google.auth import default

creds, _ = default()
gc = gspread.authorize(creds)
```

---

## How to Run

### Option 1: Google Colab

1. Open the DukaanMitra AI notebook in Google Colab.
2. Install the required Python libraries.
3. Add your `GROQ_API_KEY` to Colab Secrets and enable notebook access.
4. Initialize the Groq language model.
5. Authenticate your Google account.
6. Connect to Google Sheets using gspread.
7. Create or open the inventory spreadsheet.
8. Define the Pydantic model and LangChain tools.
9. Create the DukaanMitra AI agent.
10. Execute the `chat()` function to interact with the agent.

### Option 2: GitHub Repository Structure

```text
YOUR_ROLL_NUMBER_DriveReady_OPC_2026/
│
├── README.md
│
├── Day-1/
│   ├── README.md
│   └── Day1_Task.ipynb
│
├── Day-2/
│   ├── README.md
│   └── Day2_Task.ipynb
│
├── Day-3/
│   ├── README.md
│   └── Day3_Task.ipynb
│
└── Day-4/
    ├── README.md
    └── Day4_Task.ipynb
```

---

## Key Observations & Learnings

1. **AI Agent Tools:** Learned how to convert Python functions into tools using LangChain's `@tool` decorator.
2. **Function Calling:** Understood how an LLM selects tools and how Python executes the requested operations.
3. **Structured Output:** Learned how Pydantic defines and validates structured business information.
4. **Google Sheets Integration:** Connected Python applications with Google Sheets to retrieve and store inventory data.
5. **Inventory Management:** Implemented tools for checking product prices, available stock, low-stock items and expiry dates.
6. **Agent Architecture:** Learned how to create an AI agent with multiple tools using `create_agent()`.
7. **Conversation Memory:** Maintained previous messages to support continuous interactions.
8. **Error Handling:** Added exception handling to manage unexpected failures during agent execution.
9. **Business Workflow Automation:** Understood how AI agents can support inventory and restocking operations.

---

## Future Enhancements

- Integrate a permanent database for multi-store inventory management.
- Add CSV and Excel uploads for bulk inventory updates.
- Implement AI-based product demand forecasting.
- Generate automatic low-stock and expiry alerts.
- Compare wholesale suppliers based on price, availability and delivery time.
- Add owner-approved purchase order workflows.
- Generate sales, inventory and profit reports.
- Develop a user-friendly business management dashboard.
- Support multiple kirana stores and supplier accounts.

---

## Conclusion

Day 4 helped develop a practical understanding of LangChain tools, function calling, structured data validation and Google Sheets integration.

By applying these concepts to **DukaanMitra AI – Smart Kirana Business Agent**, the project moves beyond a basic chatbot towards a tool-using AI assistant capable of retrieving inventory information, identifying stock-related issues and managing restocking requests.

The implementation establishes a foundation for building a smarter and more efficient kirana business management platform.
