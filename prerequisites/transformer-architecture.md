# 🧠 Transformer Architecture & Attention Mechanism

[⬅ Back to README](../README.md)

---

## 📌 Overview

The Transformer is the core architecture behind modern LLMs like GPT, BERT, etc.

It replaces RNNs/CNNs using:
- Self-attention  
- Parallel processing  

---

## ⚙️ High-Level Architecture

```
Input → Embedding → Positional Encoding
       ↓
   Transformer Block (× N)
       ↓
     Output
```

---

## 🧩 Transformer Block Components

---

### 1. Multi-Head Self-Attention

- Captures relationships between tokens  
- Core innovation  

---

### 2. Feed Forward Network (FFN)

- Applies non-linear transformations  

---

### 3. Add & Norm

- Residual connections  
- Layer normalization  

---

## 🧠 Attention Mechanism (Core Concept)

---

### 📌 Idea

Each word looks at other words to understand context.

---

### Example Sentence

```
"The animal didn't cross the street because it was tired"
```

👉 "it" refers to "animal"  
→ Attention helps capture this relationship  

---

## ⚙️ Attention Formula

:contentReference[oaicite:0]{index=0}


<img width="940" height="446" alt="image" src="https://github.com/user-attachments/assets/b243a31e-982f-4093-b2c0-34784cbfb51a" />


---

### Components

- Q (Query) → what we are looking for  
- K (Key) → what we match against  
- V (Value) → actual information  

---

## 🔄 Step-by-Step Attention

---

### Step 1: Compute similarity

```
Q × Kᵀ
```

---

### Step 2: Scale

```
/ √d_k
```

---

### Step 3: Softmax

- Convert to probabilities  

---

### Step 4: Weighted sum with V

- Final representation  

---

## 🧩 Multi-Head Attention

---

### 📌 Why?

- Capture different relationships  

---

### Example

Head 1 → Grammar  
Head 2 → Meaning  
Head 3 → Position  

---

### Formula

:contentReference[oaicite:1]{index=1}

---

## 📍 Positional Encoding

---

### 📌 Problem

Transformers don’t understand order  

---

### Solution

Add position information:

```
Token + Position Encoding
```

---

## 🔁 Encoder vs Decoder

---

### Encoder (BERT)

- Bidirectional  
- Understands context  

---

### Decoder (GPT)

- Autoregressive  
- Generates text  

---

## ⚖️ Transformer vs RNN

| Feature | Transformer | RNN |
|--------|------------|-----|
| Parallelism | Yes | No |
| Long context | Better | Limited |
| Speed | Faster | Slower |

---

## 🚨 Common Interview Questions

- Why scale by √d_k?  
- Difference between self-attention and cross-attention  
- Why multi-head attention?  
- Why positional encoding is needed?  

---

## 💡 Key Insight

> Attention allows the model to dynamically focus on relevant parts of the input, making Transformers highly effective for language understanding.
