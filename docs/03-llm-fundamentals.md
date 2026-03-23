# 🧠 LLM Fundamentals

## 📌 Overview

Large Language Models (LLMs) are deep learning models trained on massive text corpora to understand and generate human-like language.

They power:
- Chatbots
- Code generation
- Summarization
- Retrieval-Augmented Generation (RAG)

---

## 🧠 What is a Large Language Model?

An LLM is a neural network that:
- Predicts the next token in a sequence
- Learns language patterns from large-scale data
- Uses context to generate coherent responses

---

## ⚙️ How LLMs Work (High-Level)

### Training Objective

LLMs are trained using **next-token prediction**:

```
Input:  "The glucose level is"
Output: "high"
```

---

### Core Architecture

Most modern LLMs are based on the **Transformer architecture**.

Key components:
- Self-attention mechanism  
- Feedforward layers  
- Positional encoding  

---

📚 References:
- https://arxiv.org/abs/1706.03762 (Attention is All You Need)  
- https://platform.openai.com/docs/guides/gpt  

---

## 🔤 Tokens & Tokenization

### 📌 What is a Token?

A token is a unit of text used by the model.

Examples:
- Word → "glucose"
- Subword → "glu", "cose"
- Character → "g", "l", "u"

---

### Example

```
Text: "Glucose level is high"

Tokens:
["Glucose", "level", "is", "high"]
```

---

### Why Tokenization Matters

- Models process tokens, not raw text  
- Cost is based on token usage  
- Context window is measured in tokens  

---

### Tokenization Tools

- OpenAI Tokenizer  
  https://platform.openai.com/tokenizer  

- tiktoken (Python library)  
  https://github.com/openai/tiktoken  

---

### Token Limits (Context Window)

Each model has a maximum token limit.

Example:
- 4K tokens → small context  
- 32K / 128K tokens → larger context  

---

## 💡 Key Insight

> LLMs do not understand language like humans — they predict the most probable next token based on context.
