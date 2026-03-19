# 🔬 Chunking Deep Dive

## 📌 Overview

Chunking is the process of splitting large documents into smaller, manageable pieces for processing by Large Language Models (LLMs).

It is critical in Retrieval-Augmented Generation (RAG) systems because:
- LLMs have limited context windows
- Retrieval operates at chunk-level granularity
- Poor chunking leads to irrelevant or incomplete answers

---

## 🧠 Why Chunking Matters

Effective chunking directly impacts:

- Retrieval accuracy
- Context preservation
- Token efficiency
- Latency and cost

> Poor chunking is one of the most common causes of RAG system failure.

---

## 🧩 Chunking Strategies

---

### 1. Fixed-size Chunking

#### Description
Splits text into equal-sized chunks based on:
- Characters
- Tokens

#### Example

```
Input:
"Patient has high glucose levels. HbA1c is elevated. Cholesterol is normal."

Chunk Size = 50 characters

Chunks:
1. "Patient has high glucose levels. HbA1c is"
2. " elevated. Cholesterol is normal."
```

#### Pros
- Simple and fast
- Easy to implement

#### Cons
- Breaks semantic meaning
- Leads to poor retrieval quality

---

### 2. Token-based Chunking

#### Description
Splits text based on token count using model tokenizer.

#### Example

```
Chunk Size = 20 tokens

Chunks:
- Tokens 0–20
- Tokens 20–40
```

#### Tools
- https://platform.openai.com/tokenizer

#### Pros
- Aligns with model limits
- Better cost control

#### Cons
- Ignores semantic boundaries

---

### 3. Sentence-based Chunking

#### Description
Splits text into sentences using NLP parsing.

#### Example

```
Input:
"Glucose is high. HbA1c is elevated. Cholesterol is normal."

Chunks:
1. "Glucose is high."
2. "HbA1c is elevated."
3. "Cholesterol is normal."
```

#### Pros
- Preserves meaning
- Improves retrieval accuracy

## 🧩 Chunking Strategies (Advanced)

---

### 4. Semantic Chunking

#### Description
Splits text based on **meaning and context** rather than fixed size.

This is typically done by:
- Sentence embeddings
- Similarity grouping
- Topic segmentation

---

#### Example

```
Input:
"Glucose is high. HbA1c is elevated. Stock market is volatile."

Chunks:
1. "Glucose is high. HbA1c is elevated."
2. "Stock market is volatile."
```

---

#### Tools
- LlamaIndex SemanticSplitter  
  https://docs.llamaindex.ai/en/stable/  

- Embedding-based clustering (custom pipelines)

---

#### Pros
- Preserves semantic meaning
- Improves retrieval accuracy

#### Cons
- Computationally expensive
- Requires tuning

---

### 5. Recursive Chunking (Most Used in Practice)

#### Description
Splits text hierarchically:
- Paragraph → Sentence → Word

If a chunk is too large, it is recursively split using smaller units.

---

#### Example (LangChain)

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=50
)

chunks = splitter.split_text(text)
```

---

#### Reference
- https://python.langchain.com/docs/concepts/text_splitters/

---

#### Pros
- Balanced approach
- Maintains structure better than fixed chunking
- Widely used in production

#### Cons
- Requires tuning (chunk size, overlap)
- Still not fully semantic

---

### 6. Document Structure-based Chunking

#### Description
Splits documents based on their **layout and structure**:
- Headings
- Sections
- Tables
- Paragraph blocks

---

#### Example

```
Document:
[Section: Blood Report]
Glucose: 180 mg/dL

[Section: Lipid Profile]
Cholesterol: Normal

Chunks:
1. Blood Report → Glucose: 180 mg/dL
2. Lipid Profile → Cholesterol: Normal
```

---

#### Tools

- Docling (layout-aware parsing)  
  https://github.com/DS4SD/docling  

- Unstructured.io  
  https://unstructured.io/  

- LlamaParse  
  https://docs.llamaindex.ai/

---

#### Pros
- Best for PDFs and reports
- Preserves real-world structure
- Ideal for enterprise data

#### Cons
- Requires additional parsing tools
- More complex pipeline

---

### 7. Sliding Window Chunking

#### Description
Creates overlapping chunks to preserve context continuity.

---

#### Example

```
Chunk size: 100 tokens
Overlap: 20 tokens

Chunk 1: tokens 0–100  
Chunk 2: tokens 80–180
```

---

#### Pros
- Reduces context loss
- Improves retrieval continuity

#### Cons
- Increases storage
- Higher embedding and retrieval cost

## ⚙️ Key Parameters

### Chunk Size

Defines how large each chunk is (in tokens or characters).

#### Typical Values
- 300–500 tokens → faster, less context  
- 500–1000 tokens → balanced (recommended)  
- 1000+ tokens → better context, higher cost  

---

#### Impact

| Chunk Size | Impact |
|-----------|-------|
| Small | Faster retrieval, context loss |
| Medium | Balanced performance |
| Large | Better context, higher latency & cost |

---

### Chunk Overlap

Defines how much overlap exists between consecutive chunks.

#### Typical Values
- 10–20% overlap

---

#### Example

```
Chunk size: 100 tokens
Overlap: 20 tokens

Chunk 1: tokens 0–100  
Chunk 2: tokens 80–180
```

---

#### Why Overlap Matters
- Preserves context across boundaries  
- Prevents information loss  

---

## 🧪 Real-world Example (Medical Report)

### Input

```
Patient Name: John Doe
Glucose: 180 mg/dL (High)
HbA1c: 8.2% (Elevated)
Cholesterol: Normal
```

---

### Poor Chunking (Fixed)

```
Chunk 1: "Patient Name: John Doe Glucose: 180"
Chunk 2: "mg/dL (High) HbA1c: 8.2%"
```

❌ Context is broken → incorrect retrieval

---

### Better Chunking (Semantic / Structured)

```
Chunk 1:
"Glucose: 180 mg/dL (High)"

Chunk 2:
"HbA1c: 8.2% (Elevated)"
```

---

### Best Approach (Structure + Metadata)

```
Chunk:
{
  "biomarker": "Glucose",
  "value": "180 mg/dL",
  "status": "High",
  "source": "Blood Report"
}
```

✅ Enables precise retrieval and reasoning

---

## ⚖️ Trade-offs

| Strategy | Pros | Cons |
|---------|------|------|
| Fixed | Fast | Context loss |
| Semantic | Accurate | Slow |
| Recursive | Balanced | Needs tuning |
| Structure-based | Best for PDFs | Complex |
| Sliding window | Preserves context | Higher cost |

---

## 🧠 Advanced Techniques

### 1. Metadata-aware Chunking

Attach metadata to each chunk:
- Source document  
- Section name  
- Timestamp  
- Category  

---

#### Example

```
{
  "text": "Glucose: 180 mg/dL",
  "section": "Blood Report",
  "patient_id": "123"
}
```

---

### 2. Query-aware Chunking

Adjust chunking strategy based on query type:

- Search queries → smaller chunks  
- Analytical queries → larger chunks  

---

### 3. Dynamic Chunking

Use different strategies for different data types:

| Data Type | Strategy |
|----------|---------|
| PDFs | Structure-based |
| Logs | Fixed-size |
| Articles | Semantic |

---

### 4. Multi-stage Chunking

Pipeline:
1. Structure-based split  
2. Recursive refinement  
3. Add overlap  

---

## 🚨 Common Mistakes

- Using fixed chunking for complex documents  
- No overlap → context breaks  
- Ignoring document structure  
- Too large chunks → token overflow  
- Too small chunks → poor retrieval  

---

## 💡 Key Insight

> Chunking strategy often has more impact on retrieval accuracy than the choice of embedding model.

---

## 📚 References

- https://python.langchain.com/docs/concepts/text_splitters/  
- https://docs.llamaindex.ai/  
- https://github.com/DS4SD/docling  
- https://unstructured.io/  
- https://platform.openai.com/docs/guides/embeddings  
- https://cloud.google.com/architecture/gen-ai-rag  
#### Cons
- May create very small chunks
- Loss of broader context
