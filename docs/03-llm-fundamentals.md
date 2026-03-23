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

## ⚙️ Attention Mechanism

### 📌 What is Attention?

Attention allows the model to focus on the most relevant parts of the input when generating output.

---

### Why Attention is Needed

In long sentences, not all words are equally important.

Example:

```
"The patient who was diagnosed last year with diabetes has high glucose levels."
```

To predict "high", the model should focus on:
- "patient"
- "diabetes"
- "glucose"

---

### Self-Attention (Core Idea)

Each token:
- Looks at every other token
- Assigns importance (weights)
- Combines information accordingly

---

### Simplified View

```
Input Tokens → Compare with each other → Assign weights → Generate output
```

---

### Key Benefit

- Captures long-range dependencies  
- Works better than RNNs/LSTMs  

---

📚 Reference:
- https://arxiv.org/abs/1706.03762  

---

## 📏 Context Window

### 📌 Definition

The context window is the maximum number of tokens an LLM can process at once.

---

### Example

```
Model Limit: 8K tokens

Input + Output must fit within 8K tokens
```

---

### Why It Matters

- Limits how much information you can pass  
- Affects RAG system design  
- Impacts cost and latency  

---

### Problems

#### 1. Context Overflow

```
Input too large → truncated → information loss
```

---

#### 2. Lost-in-the-Middle Problem

- Important information in the middle gets ignored  

---

### Solutions

- Chunking  
- Retrieval (RAG)  
- Summarization  
- Sliding window  

---

## 🧾 Prompt Structure

### 📌 What is a Prompt?

A prompt is the input given to an LLM to guide its output.

---

### Components of a Prompt

#### 1. System Prompt
- Defines behavior and rules  

Example:
```
"You are a medical assistant. Provide accurate and concise answers."
```

---

#### 2. User Prompt
- Actual query  

Example:
```
"What is a normal glucose level?"
```

---

#### 3. Assistant Response
- Model output  

---

### Prompt Example

```
System:
"You are a medical expert."

User:
"Explain HbA1c levels."

Assistant:
"HbA1c measures average blood sugar levels over time..."
```

---

## 🎯 Prompt Types

### Zero-shot Prompting
- No examples provided  

---

### Few-shot Prompting
- Provide examples  

---

### Instruction-based Prompting
- Explicit instructions  

---

## 💡 Key Insight## 🎲 Sampling in LLMs

### 📌 Why Sampling Matters

LLMs generate text probabilistically by selecting the next token from a distribution of possible tokens.

Sampling controls:
- Creativity
- Diversity
- Determinism

---

## 🌡️ Temperature

### 📌 Definition

Temperature controls randomness in output.

---

### Behavior

| Temperature | Effect |
|------------|-------|
| 0.0 | Deterministic (same output every time) |
| 0.3–0.5 | Focused and factual |
| 0.7–1.0 | Creative and diverse |
| >1.0 | Very random (often incoherent) |

---

### Example

```
Prompt: "The glucose level is"

Temperature = 0.2 → "high"
Temperature = 0.9 → "elevated / abnormal / dangerously high"
```

---

## 🔢 Top-K Sampling

### 📌 Definition

Top-K sampling restricts the model to choose from the top K most probable tokens.

---

### Example

```
Top-K = 3

Possible tokens:
1. high (0.4)
2. normal (0.3)
3. elevated (0.2)
4. random (0.1)

Model selects from top 3 only
```

---

### Effect

- Reduces unlikely outputs  
- Improves coherence  

---

## 🎯 Top-P (Nucleus Sampling)

### 📌 Definition

Top-P selects tokens whose cumulative probability ≥ P.

---

### Example

```
Top-P = 0.9

Tokens:
high (0.4)
normal (0.3)
elevated (0.2)
random (0.1)

Selected until cumulative ≥ 0.9 → first 3 tokens
```

---

### Effect

- More adaptive than Top-K  
- Balances diversity and quality  

---

## ⚖️ Determinism vs Randomness

### Deterministic Output

- Temperature = 0  
- Same input → same output  
- Best for:
  - Extraction
  - Classification
  - Structured outputs  

---

### Random Output

- Higher temperature  
- Different outputs each time  
- Best for:
  - Content generation
  - Creative writing  

---

## 🧠 Hallucination in LLMs

### 📌 Definition

Hallucination is when an LLM generates:
- Incorrect  
- Fabricated  
- Unsupported information  

---

### Why Hallucination Happens

1. Training limitations  
2. Lack of grounding  
3. Over-generalization  
4. Probabilistic nature  

---

### Example

```
Prompt:
"What is the normal glucose level?"

Output:
"Normal glucose is 50 mg/dL" ❌ (Incorrect)
```

---

## 🚨 Types of Hallucination

### 1. Factual Errors
- Incorrect information  

---

### 2. Fabricated Data
- Made-up references or numbers  

---

### 3. Logical Errors
- Incorrect reasoning  

---

## 🛠️ Mitigation Strategies

- Use RAG (grounding)  
- Provide clear prompts  
- Reduce temperature  
- Add validation layers  
- Use structured outputs  

---

## ⚙️ Real-world Implications

### 1. Extraction Systems
- Use low temperature (0–0.3)  
- Ensure deterministic output  

---

### 2. Chatbots
- Balance temperature (0.5–0.7)  

---

### 3. Creative Applications
- Use higher temperature (0.7–1.0)  

---

## 💡 Key Insight

> LLMs are probabilistic systems. Sampling controls behavior, and hallucination is an inherent limitation that must be mitigated through system design.

---

## 📚 References

- https://platform.openai.com/docs/guides/text-generation  
- https://www.promptingguide.ai/  
- https://arxiv.org/abs/1706.03762  

> Attention enables understanding of relationships, context window limits memory, and prompts control behavior.


