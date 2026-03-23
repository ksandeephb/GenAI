# ⚡ Quantization in LLMs

## 📌 Overview

Quantization is a technique to reduce the memory and compute requirements of models by lowering the precision of weights.

---

## 🧠 What is Quantization?

LLMs normally use:

```
32-bit floating point (FP32)
```

Quantization reduces precision to:

- 16-bit (FP16)
- 8-bit (INT8)
- 4-bit (INT4)

---

## 🎯 Why Quantization is Needed

LLMs are:
- Large (GBs in size)  
- Expensive to run  
- Slow in inference  

---

### Benefits

- Reduced memory usage  
- Faster inference  
- Lower cost  
- Enables running on smaller hardware  

---

## 📊 Example

```
FP32 model → 28 GB  
INT8 model → ~14 GB  
INT4 model → ~7 GB  
```

---

## 🧩 Types of Quantization

---

### 1. FP16 (Half Precision)

- Common in GPUs  
- Good balance  

---

### 2. INT8 Quantization

- Moderate compression  
- Minimal accuracy loss  

---

### 3. INT4 Quantization

- High compression  
- Slight accuracy drop  

---

### Comparison

| Type | Memory | Speed | Accuracy |
|------|-------|------|---------|
| FP32 | High | Slow | Best |
| FP16 | Medium | Faster | Very good |
| INT8 | Low | Fast | Slight drop |
| INT4 | Very low | Very fast | Moderate drop |

---

## ⚖️ Trade-offs

| Factor | Trade-off |
|-------|----------|
| Lower precision | Faster, cheaper |
| Accuracy | Slight degradation |

---

## 💡 Key Insight

> Quantization is the most effective way to reduce cost and improve inference speed without retraining the model.

# ⚡ Quantization in LLMs

## 📌 Overview

Quantization is a technique to reduce the memory and compute requirements of models by lowering the precision of weights.

---

## 🧠 What is Quantization?

LLMs normally use:

```
32-bit floating point (FP32)
```

Quantization reduces precision to:

- 16-bit (FP16)
- 8-bit (INT8)
- 4-bit (INT4)

---

## 🎯 Why Quantization is Needed

LLMs are:
- Large (GBs in size)  
- Expensive to run  
- Slow in inference  

---

### Benefits

- Reduced memory usage  
- Faster inference  
- Lower cost  
- Enables running on smaller hardware  

---

## 📊 Example

```
FP32 model → 28 GB  
INT8 model → ~14 GB  
INT4 model → ~7 GB  
```

---

## 🧩 Types of Quantization

---

### 1. FP16 (Half Precision)

- Common in GPUs  
- Good balance  

---

### 2. INT8 Quantization

- Moderate compression  
- Minimal accuracy loss  

---

### 3. INT4 Quantization

- High compression  
- Slight accuracy drop  

---

### Comparison

| Type | Memory | Speed | Accuracy |
|------|-------|------|---------|
| FP32 | High | Slow | Best |
| FP16 | Medium | Faster | Very good |
| INT8 | Low | Fast | Slight drop |
| INT4 | Very low | Very fast | Moderate drop |

---

## ⚖️ Trade-offs

| Factor | Trade-off |
|-------|----------|
| Lower precision | Faster, cheaper |
| Accuracy | Slight degradation |

---

## 💡 Key Insight

> Quantization is the most effective way to reduce cost and improve inference speed without retraining the model.

