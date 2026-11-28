# Day 5 – Retrieval-Augmented Generation (RAG) | DukaanMitra AI

## 📌 Project Overview

**DukaanMitra AI** is an AI-powered business assistant designed to help small kirana store owners manage their daily business activities more efficiently.

On Day 5 of the Drive Ready – AI Agents | One Person Company (OPC) Initiative, I implemented a basic **Retrieval-Augmented Generation (RAG)** system using ChromaDB and LangChain.

This implementation allows DukaanMitra AI to retrieve relevant information from its knowledge base and use it to answer questions about inventory management, restocking, expiry prevention, sales analysis, and supplier selection.

## 🎯 Objectives

- Understand the concept of Retrieval-Augmented Generation (RAG).
- Create a knowledge base using ChromaDB.
- Store business-related information as documents.
- Retrieve relevant information based on user queries.
- Integrate the retrieval function with a LangChain tool.
- Connect the knowledge retrieval tool with the DukaanMitra AI agent.

## 🛠️ Technologies Used

- **Python** – Core programming language.
- **Google Colab** – Development environment.
- **Groq API** – Large Language Model access.
- **LangChain** – Agent and tool integration.
- **ChromaDB** – Vector database for storing and retrieving information.
- **Pydantic** – Data validation.

## 🧠 Key Concepts Implemented

### 1. Retrieval-Augmented Generation (RAG)

RAG combines information retrieval with an LLM.

Instead of relying only on the model's existing knowledge, the system first retrieves relevant information from a knowledge base and then uses that information to generate an answer.

**Workflow:**

1. User asks a question.
2. The system searches the ChromaDB knowledge base.
3. Relevant documents are retrieved.
4. The retrieved information is provided to the AI agent.
5. The agent generates a response based on the available information.

### 2. Creating a Knowledge Base

Created a collection of business-related information for DukaanMitra AI.

The knowledge base includes:

- Inventory management
- Low-stock identification
- Restocking recommendations
- Expiry prevention
- Sales analysis
- Demand trends
- Supplier selection
- Purchase requests
- Owner approval
- Profit analysis
- Business reports

### 3. ChromaDB Integration

Used ChromaDB to store and retrieve business knowledge.

The implementation includes:

- Creating a ChromaDB client.
- Creating a collection named `dukaanmitra_knowledge`.
- Storing FAQ documents with unique IDs.
- Retrieving relevant documents using user queries.
- Displaying the retrieved information.

### 4. Creating the Search FAQ Tool

Created a LangChain tool named `search_faq`.

This tool searches the DukaanMitra knowledge base and returns relevant information based on the user's question.

It helps the agent answer general business-related questions using retrieved knowledge.

### 5. Integrating RAG with the AI Agent

Integrated the `search_faq` tool with the existing DukaanMitra AI agent.

The agent uses different tools depending on the user's question:

| User Query | Tool Used |
|---|---|
| What is the price of soap? | `get_price` |
| How much rice is available? | `check_stock` |
| Which products have low stock? | `check_low_stock` |
| Which products are nearing expiry? | `check_expiry` |
| How can I prevent product expiry? | `search_faq` |
| How should I plan restocking? | `search_faq` |

Google Sheets tools provide inventory information, while ChromaDB provides general business knowledge.

## ⚙️ Implementation Workflow

```text
          User Query
               |
               v
        DukaanMitra AI Agent
               |
               v
       Select Appropriate Tool
               |
        +------+------+
        |             |
        v             v
   Google Sheets   ChromaDB
     Tools        Knowledge Base
        |             |
        v             v
 Inventory Data   Relevant Documents
        |             |
        +------+------+
               |
               v
        LLM Generates Answer
               |
               v
         Final Response
```

## 🧪 Sample Queries

The following queries can be used to test the implementation:

1. How can I identify products that need restocking?
2. How can I prevent products from expiring?
3. What are the benefits of inventory management?
4. How can I identify fast-moving products?
5. How should I choose wholesale suppliers?
6. Why is demand analysis important for a kirana store?
7. How can I reduce losses due to stock shortages?
8. How can I generate inventory reports?

## 📚 Key Learnings

- Understood the working of Retrieval-Augmented Generation (RAG).
- Learned how to create and manage ChromaDB collections.
- Stored business knowledge as documents.
- Retrieved relevant information using semantic search.
- Created a custom FAQ search tool using LangChain.
- Integrated the retrieval tool with an AI agent.
- Understood the difference between retrieving stored knowledge and accessing live inventory data.

## 🚀 Future Enhancements

- Add more business-related documents to the knowledge base.
- Support PDF and CSV document uploads.
- Implement advanced demand forecasting.
- Add supplier information and comparison capabilities.
- Generate personalized business insights.
- Support multiple kirana stores with separate knowledge and inventory data.

## 👨‍💻 Project Information

**Project Name:** DukaanMitra AI – Smart Kirana Business Agent

**Program:** Drive Ready – AI Agents | One Person Company (OPC) Initiative

**Department:** Department of Technical Training (DoTT)

**Institution:** Aditya University

**Day:** 5 – Retrieval-Augmented Generation (RAG)

---

*This repository contains the practical implementation and learning outcomes of Day 5. The current RAG implementation uses a sample business knowledge base; it does not automatically retrieve live inventory data from ChromaDB. Live inventory information is accessed separately through Google Sheets tools.*
