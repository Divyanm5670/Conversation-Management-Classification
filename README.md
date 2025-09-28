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
```
**2. Import dependencies**
- `groq` → for API calls  
- `json` → for parsing schema outputs  
- `os` and `google.colab.userdata` → for managing secrets  

**3. Configure API Key in Colab**
- Go to **Colab left sidebar → Key icon (Secrets)**  
- Add a new secret:  
  - Name: `GROQ_API_KEY`  
  - Value: *your Groq API key*  
- Toggle **Notebook access ON**  

**4. Run the Notebook**
- Execute the colab notebbok [here](https://bit.ly/4gHdlcs)
- The notebook installs dependencies, configures the API client, and demonstrates **Task 1** and **Task 2** step by step.  

---
### 🛠️ Demonstrations

#### 🔹 Task 1: Conversation Management

The `ConversationManager` class handles message history, periodic summarization, and truncation.  

**Example flow:**
- A dialogue about AI in mental health after COVID is simulated.  
- After every 5 assistant replies, a summary replaces the old history.  

**Sample Output (Summarization):**

```bash
--- Triggering summarization after 5 runs. ---
--- Conversation summarized and history replaced. ---
[
  {
"role": "system",
"content": "Summary of previous conversation: **Summary:**\n\nThe conversation revolves around the impact of COVID-19 on mental health and the role of AI in addressing this issue. Key points include:\n\n- The WHO reported a 25% global increase in anxiety and depression cases during the pandemic.\n- Young adults, healthcare workers, and those who lost jobs were disproportionately affected.\n- AI tools are being used to screen symptoms, run chatbots, and analyze speech for early signs of depression.\n- AI-powered chatbots, such as Woebot and Wysa, have shown reduced anxiety symptoms in users within two weeks.\n- AI is intended to support human therapists, providing 24/7 access and supplementing treatment, rather than replacing it."
  }
]
```


**Truncation Demonstration:**
- By last 2 turns → keeps the final two exchanges.  
- By last 150 characters → trims history to fit within the limit.  

---

#### 🔹 Task 2: JSON Schema Extraction

The tool is configured as:
```python
extraction_tool = {
  "type": "function",
  "function": {
    "name": "extract_user_details",
    "description": "Extracts user information and returns JSON.",
    "parameters": user_details_schema
  }
}

```
**Example Input:**
```
'Hi, I'm Rajesh Kumar, 28 years old, based in Mumbai, India. After recovering from COVID, I participated in a hospital's AI-driven monitoring program for long-COVID symptoms. My email is rajesh.kumar@email.com.'
```

**Extracted Output:**
```
{
    "age": 28,
    "email": "rajesh.kumar@email.com",
    "location": "Mumbai, India",
    "name": "Rajesh Kumar",
    "phone": null
}
```

**Validation:**
- ✅ SUCCESS → Output matches the required schema keys.


**Missing Data Handling:**
- When details are missing, the tool returns null values, ensuring strict compliance.
---

## 📦 Dependencies
- `groq` → official Python client for Groq API
- `google.colab.userdata` → securely storing secrets in Colab
- Standard libraries → `os`, `json`



## 📌 Notes
- Summarization ensures scalable long conversations without exceeding model limits.
- Tool-calling enforces reliability in structured data extraction.
- All demonstrations use Groq models:
  - `llama-3.1-8b-instant` → for conversation summarization
  - `llama-3.3-70b-versatile` → for schema-based extraction
