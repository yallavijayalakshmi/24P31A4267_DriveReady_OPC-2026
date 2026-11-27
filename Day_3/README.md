# Day 3: LangChain Expression Language (LCEL), Automated Evaluation & Agent Architectures

> **Drive Ready – AI Agents | One Person Company (OPC) Initiative**  
> *Department of Technical Training, Aditya University*

---

## Overview

Day 3 focuses on building and improving LLM applications using **LangChain Expression Language (LCEL)**, implementing automated testing and evaluation frameworks, comparing prompt versions, understanding temperature sensitivity, and identifying when to use an AI Agent instead of traditional Python code or a single LLM call.

As part of this practical work, these concepts are implemented using **DukaanMitra AI – Smart Kirana Business Agent**, an AI-powered assistant designed to help small kirana store owners manage inventory, analyse sales, prevent product expiry, and make better restocking decisions.

---

## Tasks Covered

### Task 1: Conversational Chains with LCEL

**Implementation:**

Created a conversational AI chain using LangChain Expression Language (LCEL).

```python
from langchain_core.prompts import ChatPromptTemplate, MessagesPlaceholder
from langchain_core.output_parsers import StrOutputParser

SYSTEM = """ROLE: You are DukaanMitra AI, a friendly assistant
for kirana store owners.

FACTS:
- Help manage inventory and stock.
- Analyse product sales and demand.
- Identify low-stock and near-expiry products.
- Suggest restocking quantities.
- Help compare wholesale suppliers.

RULES:
- Never invent stock levels or sales figures.
- Never provide unverified supplier information.
- Never place orders without owner approval.
- If information is missing, ask the store owner.

FORMAT:
Reply in simple, friendly language under 100 words."""

prompt = ChatPromptTemplate.from_messages([
    ("system", SYSTEM),
    MessagesPlaceholder("history"),
    ("human", "{question}"),
])

chain = prompt | llm | StrOutputParser()

history = []

def ask(question: str) -> str:
    answer = chain.invoke({
        "history": history,
        "question": question
    })

    history.extend([
        ("human", question),
        ("ai", answer)
    ])

    return answer
```

**Test Verification:**

- Turn 1: `"Hi, I'm Ravi. Can you help me manage my kirana store inventory?"` → Provides inventory management guidance.
- Turn 2: `"What's my name?"` → Uses the previous conversation to identify the store owner's name as Ravi.

**Key Learning:** Implemented conversational memory using `MessagesPlaceholder` to maintain context across multiple interactions.

### Task 2: Automated Testing & Evaluation Framework (`run_tests`)

**Implementation:**

Developed a custom testing function called `run_tests` to evaluate DukaanMitra AI responses using test cases stored in a CSV file.

The evaluation framework:
- Reads test questions from a CSV file.
- Sends each question to the LCEL chain.
- Checks whether the expected keyword appears in the response.
- Displays PASS or FAIL for each test.
- Calculates the overall pass percentage.

**Benchmark Test Suite – DukaanMitra AI:**

| No. | Test Question | Expected Keyword |
|---|---|---|
| 1 | How can I manage my kirana store inventory? | inventory |
| 2 | What should I do when products are running low? | stock |
| 3 | How can I prevent products from expiring? | expiry |
| 4 | How can I compare wholesale suppliers? | supplier |
| 5 | How can I analyse my product sales? | sales |
| 6 | How can I identify fast-selling products? | products |
| 7 | Can you suggest restocking quantities? | restock |
| 8 | Can you place an order without my approval? | approval |
| 9 | What are the benefits of inventory management? | inventory |
| 10 | Can you provide my current stock levels without store data? | provide |

**Key Design Principle:**

Each test invocation uses an isolated, empty conversation history:

```python
answer = chain.invoke({
    "history": [],
    "question": row["question"]
})
```

This prevents previous test conversations from influencing the current test.

**Evaluation Metric:**

The test framework calculates the percentage of successful keyword matches. Actual test results should be recorded after running the evaluation.

### Task 3: Prompt Engineering Iteration & Comparative Evaluation

**Implementation:**

Improved the system prompt through multiple versions to make DukaanMitra AI more reliable and business-focused.

**Prompt improvements:**

- **SYSTEM_V1:** Basic role definition for a kirana business assistant.
- **SYSTEM_V2:** Added specific instructions for inventory, sales, expiry management and supplier comparisons.
- **SYSTEM_V3:** Added stronger restrictions against inventing stock data, sales figures and supplier information.

**Important Prompt Rule:**

"If the required store information is unavailable, ask the owner to provide the relevant details. Never invent business information."

**Comparative Evaluation:**

| Version | Main Improvement | Evaluation |
|---|---|---|
| SYSTEM_V1 | Basic business assistance | Test after execution |
| SYSTEM_V2 | Improved task-specific instructions | Test after execution |
| SYSTEM_V3 | Stronger accuracy and safety rules | Test after execution |

**Key Learning:** Prompt engineering improves the clarity, reliability and relevance of AI responses. Comparing different prompt versions helps identify which instructions work best.

### Task 4: Temperature Sensitivity & Stability Testing

**Implementation:**

Tested how different temperature settings influence the responses generated by DukaanMitra AI.

Temperature controls the randomness of model responses.

Example:

```python
llm = ChatGroq(
    model="llama-3.3-70b-versatile",
    temperature=0.0
)
```

A second model instance can be configured with a higher temperature, if supported by the selected Groq model.

**Test Protocol:**

- Execute the same CSV test suite with a low temperature.
- Execute it again with a higher temperature.
- Compare the generated responses.
- Observe differences in wording and keyword matching.
- Record the pass percentages for both runs.

**Expected Observations:**

- Low temperature generally produces more consistent responses.
- Higher temperature can produce greater variation in wording.
- Keyword-based tests may fail when the model uses synonyms instead of the expected keyword.

**Key Learning:** Low temperature settings (such as 0.0–0.2, where supported) are generally preferable for repeatable automated evaluation. Temperature does not guarantee factual accuracy.

### Task 5: Architectural Decision Framework – "Agent or Not?"

Established a decision framework to determine when DukaanMitra AI should use traditional Python code, a single LLM call, or an autonomous AI Agent.

**1. Plain Python Code (Deterministic Operations)**

Examples:
- Checking available stock from an inventory dictionary.
- Calculating the total cost of products.
- Identifying products below a minimum stock threshold.
- Calculating the quantity that needs to be reordered.

Why?
- Faster execution.
- No LLM token cost.
- Predictable results.
- Suitable for mathematical and rule-based operations.

**2. Single LLM Call (Language Understanding & Generation)**

Examples:
- Explaining how to manage kirana store inventory.
- Providing suggestions to reduce product wastage.
- Generating a simple business report from supplied information.
- Explaining sales trends provided by the store owner.

Why?
- Suitable for understanding and generating natural language.
- Does not require multiple tool executions.
- Simple implementation.

**3. AI Agent (Multi-Step & Goal-Oriented Tasks)**

Example:

"Check my current inventory, identify products running low, analyse recent sales, compare available suppliers, recommend the best supplier, and prepare a purchase order for my approval."

Why?
- Requires multiple tool calls.
- Needs information from different sources.
- Requires sequential decision-making.
- Uses conditional logic based on tool results.
- Requires owner approval before finalising an order.

**Architectural Decision:**

DukaanMitra AI can combine all three approaches:
- Python functions for stock calculations and inventory operations.
- LLM for understanding owner requests and generating business insights.
- AI Agent for coordinating multi-step inventory and supplier workflows.

---

## Tech Stack & Setup

### Technologies Used

- Python
- Google Colab
- LangChain
- LangChain Expression Language (LCEL)
- Groq API
- Llama 3.3 70B Versatile model
- CSV and JSON
- Python functions and dictionaries

### Required Libraries

```bash
pip install -q groq langchain langchain-core langchain-groq pandas
```

### API Key Configuration

```python
from google.colab import userdata
from langchain_groq import ChatGroq

llm = ChatGroq(
    model="llama-3.3-70b-versatile",
    temperature=0.2,
    api_key=userdata.get("GROQ_API_KEY")
)
```

Store your Groq API key securely in Google Colab Secrets using the name `GROQ_API_KEY`.

---

## How to Run

### Option 1: Google Colab

1. Open your DukaanMitra AI notebook in Google Colab.
2. Install the required libraries.
3. Configure your Groq API key using Colab Secrets.
4. Execute the LCEL conversational chain.
5. Create the CSV test dataset.
6. Execute the `run_tests()` function.
7. Compare different prompt versions and temperature settings.
8. Execute the LangChain agent example.

### Option 2: Run Locally

Ensure Python and the required libraries are installed.

Keep the following files inside the Day-3 folder:

```text
Day-3/
├── README.md
├── Day3_Task.ipynb
├── task.py
└── dukaanmitra_tests.csv
```

Run the Python script:

```bash
cd Day-3
python task.py
```

---

## Key Observations & Learnings

1. **LCEL:** Learned how to create declarative LLM pipelines using the pipe operator (`|`).
2. **Conversational Memory:** Learned how to maintain conversation context using `MessagesPlaceholder` and message history.
3. **Automated Evaluation:** Implemented CSV-based testing to evaluate AI responses using expected keywords.
4. **Prompt Engineering:** Understood how improving system prompts can make AI responses more reliable and relevant.
5. **Temperature Testing:** Learned how temperature influences response variation and evaluation stability.
6. **Agent Architecture:** Understood the difference between traditional Python code, single LLM calls and autonomous AI Agents.
7. **Business Application:** Applied LLM and agent concepts to real-world kirana store management problems.

---

## Future Enhancements

- Connect real inventory data through a database.
- Enable CSV uploads for sales and stock information.
- Implement demand forecasting.
- Add automated low-stock and expiry alerts.
- Integrate supplier comparison tools.
- Generate purchase orders with owner approval.
- Build a multi-store management dashboard.

---

## Conclusion

Day 3 helped strengthen the practical understanding of LangChain, LCEL, automated evaluation and AI Agent architectures. These concepts form the foundation for developing **DukaanMitra AI**, an intelligent business assistant that can help small kirana store owners make smarter inventory, purchasing and business decisions.
