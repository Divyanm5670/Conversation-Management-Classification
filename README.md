Conversation Management & Classification using Groq API

This project showcases two core conversational AI capabilities using the Groq API (with full OpenAI SDK compatibility), implemented entirely in a Google Colab notebook without additional orchestration frameworks.

The two main tasks are:

Conversation History Management with Summarization

Maintaining user–assistant histories.

Periodically summarizing long dialogues into compact contextual summaries.

Truncating conversation history by turns or character length for efficient context handling.

JSON Schema Classification & Structured Information Extraction

Extracting structured user details (name, email, phone, location, age) from free-form chat messages.

Enforcing a strict schema with null values where information is missing.

Forcing tool execution via Groq’s function-calling interface for predictable, schema-compliant results.
