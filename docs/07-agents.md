# 🤖 Agents in GenAI Systems

## 📌 Overview

Agents are systems that use Large Language Models (LLMs) to:
- Make decisions  
- Plan actions  
- Use tools  
- Execute multi-step workflows  

---

## 🧠 What is an Agent?

An agent is an LLM-powered system that can:

- Understand a goal  
- Break it into steps  
- Execute actions using tools  
- Iterate until completion  

---

### Example

```
User Query:
"Find my latest lab report and summarize glucose levels"

Agent Workflow:
1. Search document
2. Extract data
3. Summarize results
4. Return answer
```

---

## 🎯 Why Agents are Needed

Traditional pipelines:
- Fixed workflow  
- No adaptability  

---

Agents:
- Dynamic decision-making  
- Multi-step reasoning  
- Tool integration  

---

## ⚙️ Agent Architecture

```
User Input
   ↓
LLM (Planner)
   ↓
Tool Selection
   ↓
Tool Execution
   ↓
Observation
   ↓
LLM (Next Step)
   ↓
Final Output
```

---

## 🧩 Core Components

### 1. LLM (Brain)
- Reasoning  
- Planning  
- Decision-making  

---

### 2. Tools

Examples:
- Search APIs  
- Databases  
- Calculators  
- External services  

---

### 3. Memory

- Stores previous interactions  
- Maintains context  

---

### 4. Orchestration

- Controls execution flow  
- Frameworks: LangChain, LangGraph  

---

📚 References

- https://python.langchain.com/docs/  
- https://www.anthropic.com/index/building-effective-agents

## 🛠️ Tool Calling (Function Calling)

### 📌 What is Tool Calling?

Tool calling allows an LLM to:
- Identify when external tools are needed  
- Generate structured inputs  
- Call functions/APIs  

---

### Example

```
User Query:
"What is the glucose level in my report?"

LLM Decision:
→ Call function: get_lab_report()

Tool Output:
→ "Glucose: 180 mg/dL"

LLM:
→ Generate final answer
```

---

### How It Works

1. LLM receives query  
2. Determines if a tool is required  
3. Generates structured function call  
4. Tool executes  
5. LLM uses output  

---

### Benefits

- Access to real-time data  
- Improves accuracy  
- Extends LLM capabilities  

---

📚 References

- https://platform.openai.com/docs/guides/function-calling  
- https://python.langchain.com/docs/modules/agents/  

---

## 🧩 Types of Agents

---

### 1. Single-step Agent

- One decision → one action  

---

### 2. Multi-step Agent

- Breaks problem into steps  
- Iteratively solves  

---

### 3. Tool-using Agent

- Uses external APIs/tools  

---

### 4. Conversational Agent

- Maintains context  
- Supports multi-turn interactions  

---

## 🔁 ReAct Pattern (Reason + Act)

### 📌 Definition

ReAct combines:
- Reasoning (thinking)  
- Acting (tool usage)  

---

### Workflow

```
Thought → Action → Observation → Thought → Action → Final Answer
```

---

### Example

```
User:
"What is the normal glucose level?"

Agent:

Thought: I need medical information  
Action: search_medical_db  
Observation: "70–100 mg/dL"  

Thought: I now have the answer  
Final Answer: "Normal glucose is 70–100 mg/dL"
```

---

### Why ReAct is Powerful

- Transparent reasoning  
- Better decision-making  
- Handles multi-step tasks  

---

📚 Reference

- https://arxiv.org/abs/2210.03629  

---

## ⚖️ Trade-offs

| Feature | Benefit | Cost |
|--------|--------|------|
| Tool calling | Accurate data | Latency |
| Multi-step reasoning | Better results | Complexity |
| ReAct | Transparency | Token usage |

---

## 💡 Key Insight

> Agents extend LLMs from passive responders to active problem solvers.

## 🚫 When NOT to Use Agents

### 📌 Key Principle

Agents add flexibility but also introduce:
- Complexity  
- Latency  
- Cost  

---

### Avoid Agents When:

#### 1. Simple Workflows

```
Input → Process → Output
```

Example:
- Text summarization  
- Basic extraction  

---

#### 2. Deterministic Systems

- Financial calculations  
- Rule-based validation  

---

#### 3. Low Latency Requirements

- Real-time systems  
- High-frequency APIs  

---

#### 4. No Need for Multi-step Reasoning

- Single-step queries  
- Static responses  

---

## ⚠️ Agent Failure Modes

### 1. Infinite Loops

- Agent keeps calling tools repeatedly  

---

### 2. Wrong Tool Selection

- Calls incorrect API  

---

### 3. Hallucinated Actions

- Generates non-existent tool calls  

---

### 4. Context Loss

- Forgets previous steps  

---

## 🛠️ Failure Handling Strategies

### 1. Step Limits

```
Max steps = 5
```

---

### 2. Tool Validation

- Validate tool calls before execution  

---

### 3. Fallback Mechanisms

- Switch to simpler pipeline  
- Escalate to human  

---

### 4. Logging & Monitoring

- Track:
  - Tool usage  
  - Errors  
  - Failures  

---

## 🏭 Production Architecture

### Example Architecture

```
User Input
  ↓
API Layer
  ↓
Agent Orchestrator (LangGraph / LangChain)
  ↓
LLM (Planner)
  ↓
Tool Layer (APIs / DB / Services)
  ↓
Execution
  ↓
Response
```

---

### Supporting Components

- Cache (Redis)  
- Monitoring  
- Rate limiting  
- Error handling  

---

## ⚖️ Trade-offs

| Factor | Trade-off |
|-------|----------|
| Flexibility | Higher complexity |
| Multi-step reasoning | Higher latency |
| Tool usage | External dependency |

---

## 🚨 Common Mistakes

- Using agents for simple tasks  
- No step limit  
- No fallback strategy  
- Overusing tools  
- Ignoring latency  

---

## 🧠 Design Guidelines

- Start with simple pipelines  
- Use agents only when needed  
- Add guardrails  
- Monitor behavior  

---

## 💡 Key Insight

> Agents should be used only when dynamic decision-making and multi-step reasoning are required. Otherwise, they introduce unnecessary complexity.

---

## 📚 References

- https://python.langchain.com/docs/  
- https://www.anthropic.com/index/building-effective-agents  
