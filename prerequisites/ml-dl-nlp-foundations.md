# 📚 ML, DL & NLP Foundations

[⬅ Back to README](../../README.md)

---

## 🧠 Part 1: Machine Learning (ML)

---

## 📌 What is ML?

Learning patterns from data to make predictions.

---

## 🧩 Types of ML

| Type | Description | Example |
|------|------------|--------|
| Supervised | Labeled data | Spam detection |
| Unsupervised | No labels | Clustering |
| Reinforcement | Reward-based | Game playing |

---

## 📊 Key Concepts (VERY IMPORTANT)

---

### 1. Overfitting vs Underfitting

- Overfitting → memorizes data  
- Underfitting → fails to learn  

---

### 2. Bias vs Variance

| Concept | Meaning |
|--------|--------|
| Bias | Error due to simplicity |
| Variance | Error due to complexity |

---

### 3. Train / Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y)
```

---

## 📈 Common Algorithms

---

### Linear Regression

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)
```

---

### Logistic Regression

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression()
model.fit(X_train, y_train)
```

---

## 📊 Evaluation Metrics

---

### Classification

- Accuracy  
- Precision  
- Recall  
- F1-score  

---

### Example

```python
from sklearn.metrics import accuracy_score

accuracy = accuracy_score(y_test, y_pred)
```

---

## 💡 Key Insight

> ML focuses on learning patterns, but requires feature engineering and careful evaluation.

## 🧠 Part 2: Deep Learning (DL)

---

## 📌 What is DL?

Neural networks with multiple layers that learn representations automatically.

---

## 🧩 Core Components

---

### 1. Neuron

```
Output = Activation(Wx + b)
```

---

### 2. Activation Functions

- ReLU  
- Sigmoid  
- Tanh  

---

### Example

```python
import torch.nn as nn

layer = nn.Linear(10, 5)
activation = nn.ReLU()
```

---

## 🔄 Training Process

---

### 1. Forward Pass  
### 2. Loss Calculation  
### 3. Backpropagation  
### 4. Weight Update  

---

### Example

```python
import torch
import torch.nn as nn

model = nn.Linear(10, 1)
loss_fn = nn.MSELoss()

optimizer = torch.optim.Adam(model.parameters(), lr=0.01)

for x, y in data:
    pred = model(x)
    loss = loss_fn(pred, y)

    loss.backward()
    optimizer.step()
    optimizer.zero_grad()
```

---

## 🧱 Architectures

| Model | Use Case |
|------|---------|
| CNN | Images |
| RNN | Sequence |
| Transformer | NLP |

---

## 🚨 Important Concepts

- Gradient descent  
- Learning rate  
- Overfitting (again!)  

---

## 💡 Key Insight

> DL removes manual feature engineering by learning representations directly from data.

## 🧠 Part 3: NLP (Natural Language Processing)

---

## 📌 Traditional NLP Pipeline

---

### 1. Tokenization

```python
from nltk.tokenize import word_tokenize

tokens = word_tokenize("Glucose is high")
```

---

### 2. Stopword Removal

```python
from nltk.corpus import stopwords

filtered = [w for w in tokens if w not in stopwords.words("english")]
```

---

### 3. Stemming / Lemmatization

```python
from nltk.stem import PorterStemmer

stemmer = PorterStemmer()
stemmer.stem("running")
```

---

## 🔢 Text Representations

---

### Bag of Words

```python
from sklearn.feature_extraction.text import CountVectorizer

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(["glucose high"])
```

---

### TF-IDF

```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(["glucose high"])
```

---

## 🧠 Modern NLP (IMPORTANT)

---

### Word Embeddings

- Word2Vec  
- GloVe  

---

### Transformers

- Attention mechanism  
- Context understanding  

---

### LLMs

- GPT  
- BERT  

---

## 🔁 NLP → GenAI Connection

```
Tokenization → Embeddings → Transformer → LLM
```

---

## 🚨 Must Know for Interviews

- Tokenization  
- Embeddings  
- Attention  
- Fine-tuning vs RAG  

---

## 💡 Key Insight

> NLP evolved from rule-based → statistical → deep learning → transformers → LLMs.
