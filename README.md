# 🚀 Agentic Adaptive RAG System with Dynamic Routing and Retrieval Correction

## 📌 Overview

This project implements an **Agentic Adaptive RAG (Retrieval-Augmented Generation) system** using LangGraph.  
It enhances traditional RAG by introducing:

- Query Analysis (Pre-Retrieval Gating) to avoid unnecessary retrieval  
- Corrective RAG (CRAG) for handling low-quality retrieval  
- Dynamic routing between direct generation and retrieval pipelines  
- Web search fallback for out-of-domain or insufficient context  

The system behaves as a **workflow-based agent**, making decisions at runtime using LLM-powered nodes.

---

## 🧠 Key Features

- **LLM-based Query Routing**  
  Classifies queries to decide whether retrieval is needed or direct generation is sufficient.

- **Corrective Retrieval Pipeline (CRAG)**  
  Uses LLM-based grading to evaluate retrieved documents and triggers query rewriting + web search when needed.

- **Multi-LLM Modular Design**  
  Separate LLMs with dedicated prompts and schemas for:
  - Query Analysis (Router)
  - Retrieval Grading
  - Query Rewriting
  - Answer Generation

- **Structured Outputs (Pydantic)**  
  Ensures deterministic decision-making and eliminates unreliable string parsing.

- **Dynamic Execution Graph (LangGraph)**  
  Nodes and conditional edges define an adaptive, agent-like workflow.

---

## 🏗️ Architecture
<img width="335" height="734" alt="Screenshot 2026-03-19 131012" src="https://github.com/user-attachments/assets/99cef491-aba9-4f8b-80b2-3525557cc544" />


---

## ⚙️ System Design

### 🔹 Multi-LLM Setup

Each task uses a **dedicated LLM with task-specific prompts and schemas**:

| Component         | Role |
|------------------|------|
| Query Analysis   | Decides retrieve vs generate |
| Retriever        | Fetches relevant documents |
| Grader           | Evaluates document relevance |
| Query Rewriter   | Improves query for better retrieval |
| Generator        | Produces final answer |

---

### 🔹 Nodes Implementation

Each stage is implemented as a **LangGraph node**:

- `query_analysis()` → routing decision  
- `retrieve()` → vector search  
- `grade_documents()` → relevance filtering  
- `transform_query()` → query optimization  
- `web_search()` → external retrieval  
- `generate()` → response generation (RAG or direct)

---

### 🔹 Conditional Edges

- Route based on query type  
- Trigger fallback if retrieval quality is low  
- Dynamically switch execution path  

---

## 🧪 Example Use Cases

- **"How are you?"** → Direct LLM generation (no retrieval)  
- **"What is RAG?"** → Vector retrieval + generation  
- **"Latest AI news"** → Web search + generation  
- **Low-quality retrieval** → Query rewrite → web search fallback  

---

## 🛠️ Tech Stack

- LangChain, LangGraph  
- Groq LLM (openai/gpt-oss-120b)  
- Pydantic (Structured Outputs)  
- Vector Database (Chroma)  
- Tavily Web Search API  
- Python  

---

## ⚡ Key Improvements Over Basic RAG

| Feature | Basic RAG | This System |
|--------|----------|------------|
| Query Routing | ❌ | ✅ |
| Retrieval Validation | ❌ | ✅ |
| Query Rewriting | ❌ | ✅ |
| Web Fallback | ❌ | ✅ |
| Structured Decisions | ❌ | ✅ |

---

## 📈 Outcome

- Reduced unnecessary retrieval → lower latency & cost  
- Improved answer quality via retrieval correction  
- Increased robustness for out-of-domain queries  
- Modular design → easy to extend into full agent systems  

---

## 🔮 Future Improvements

- Add memory (conversation context)  
- Multi-hop reasoning  
- Tool selection beyond web search  
- Confidence-based routing  

---

## 🧠 Key Learning

This project demonstrates how to move from:

> Basic RAG → Adaptive, agentic retrieval systems

By introducing:
- Decision layers  
- Feedback loops  
- Structured LLM control  


### Flow Diagram
