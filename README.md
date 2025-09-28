# Conversation Management & Classification using Groq API

This project showcases two core conversational AI capabilities using the **Groq API** (with full OpenAI SDK compatibility), implemented entirely in a **Google Colab notebook** without additional orchestration frameworks.

---

## 📌 Main Tasks

### 1. Conversation History Management with Summarization
- Maintaining **user–assistant histories**.  
- Periodically **summarizing long dialogues** into compact contextual summaries.  
- Truncating conversation history by turns or character length for efficient context handling.  

### 2. JSON Schema Classification & Structured Information Extraction
- Extracting structured user details (**name, email, phone, location, age**) from free-form chat messages.  
- Enforcing a strict schema with **null values** where information is missing.  
- Forcing tool execution via Groq’s **function-calling interface** for predictable, schema-compliant results.  

---

## ✨ Features

### 🔹 Task 1: Conversation History Management
- **Configurable summarization**: Triggered automatically after every *k* assistant responses (default = 5).  
- **Custom summarizer role**: The Groq model is instructed to compress conversations into a concise, context-preserving summary.  
- **Truncation options**:  
  - By turns → Keep the last *n* turns (user+assistant pairs).  
  - By length → Retain recent messages up to a character limit.  
- **Resets history with summaries**: Instead of endlessly appending, summaries replace old dialogue, ensuring context stays manageable.  

### 🔹 Task 2: JSON Schema Classification & Information Extraction
- **Strict JSON Schema**: Enforces five required fields — name, email, phone, location, age.  
- **Groq Tool-Calling**: Defines a tool `extract_user_details`, forcing the model to return structured JSON.  
- **Automatic Validation**: Extracted outputs are checked against schema keys for correctness.  
- **Handles missing data**: Missing values are assigned `null` instead of being dropped.  

---

## 🚀 Getting Started

This project is designed to run in **Google Colab**.

### Prerequisites
- A **Google Account** (for Colab).  
- A **GroqCloud account & API Key** → available free at [groq.com](https://groq.com).  

### Setup Instructions
**1. Install library**
```bash
!pip install groq -q

