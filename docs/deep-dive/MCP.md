# 🧠 Model Context Protocol (MCP) — From Basics to Real-Time Implementation

## 📌 Overview

This document explains:

* What MCP is
* Difference between basic and real-time MCP
* How to implement a working MCP server
* How to integrate it with an LLM loop (real-time usage)
* End-to-end working example

---

# 🚀 1. What is MCP?

**Model Context Protocol (MCP)** is a structured way for an LLM (or agent) to interact with external tools.

Instead of hardcoding APIs, MCP exposes tools like:

* `get_weather`
* `query_db`
* `calculate`
* `read_file`

The LLM dynamically decides:

* When to call a tool
* Which tool to call
* How to use the result

---

## 🧩 Basic MCP vs Real-Time MCP

### ❌ Basic MCP (what most tutorials show)

```
Client → Tool → Response → End
```

* One request
* One response
* No reasoning loop

---

### ✅ Real-Time MCP

```
User → LLM → Tool → LLM → Tool → LLM → Final Answer
```

* Multi-step reasoning
* Dynamic tool usage
* Stateful
* Continuous loop

---

# 🏗️ 2. MCP Server Implementation (FastAPI)

## 📦 Install dependencies

```bash
pip install fastapi uvicorn
```

---

## 📁 server.py

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

# ---- Tool Schemas ----
class AddInput(BaseModel):
    a: int
    b: int

class WeatherInput(BaseModel):
    city: str

# ---- Tools ----
def add_tool(a: int, b: int):
    return {"result": a + b}

def weather_tool(city: str):
    # Mock response (replace with real API)
    return {"city": city, "temperature": "30°C", "condition": "Sunny"}

# ---- Tool Registry ----
TOOLS = {
    "add": add_tool,
    "get_weather": weather_tool
}

# ---- Tool Discovery ----
@app.get("/tools")
def list_tools():
    return {
        "tools": [
            {"name": "add", "description": "Add two numbers"},
            {"name": "get_weather", "description": "Get weather by city"}
        ]
    }

# ---- Generic Tool Executor ----
@app.post("/execute")
def execute(payload: dict):
    tool_name = payload["tool"]
    args = payload["args"]

    if tool_name not in TOOLS:
        return {"error": "Tool not found"}

    result = TOOLS[tool_name](**args)
    return {"tool": tool_name, "output": result}
```

---

## ▶️ Run Server

```bash
uvicorn server:app --reload
```

---

# 🤖 3. Real-Time MCP Client (Agent Loop)

This is the **core difference** — we simulate an LLM making decisions.

---

## 📁 client_agent.py

```python
import requests

BASE_URL = "http://127.0.0.1:8000"

# Simulated LLM decision function
def fake_llm(context):
    last_user_msg = context[-1]["content"]

    if "add" in last_user_msg:
        return {
            "action": "tool",
            "tool": "add",
            "args": {"a": 5, "b": 10}
        }

    elif "weather" in last_user_msg:
        return {
            "action": "tool",
            "tool": "get_weather",
            "args": {"city": "Bangalore"}
        }

    else:
        return {
            "action": "final",
            "content": "I don't know what to do."
        }

# ---- Agent Loop ----
def run_agent(user_input):
    context = [{"role": "user", "content": user_input}]

    while True:
        llm_output = fake_llm(context)

        if llm_output["action"] == "tool":
            print(f"🔧 Calling tool: {llm_output['tool']}")

            response = requests.post(
                f"{BASE_URL}/execute",
                json={
                    "tool": llm_output["tool"],
                    "args": llm_output["args"]
                }
            ).json()

            print("📦 Tool Output:", response)

            context.append({
                "role": "tool",
                "content": str(response)
            })

        elif llm_output["action"] == "final":
            print("✅ Final Answer:", llm_output["content"])
            break

# ---- Run ----
if __name__ == "__main__":
    run_agent("add two numbers")
    run_agent("what is weather today")
```

---

# 🔄 4. Real-Time MCP Flow Explained

### Example: "What is weather today?"

### Step-by-step:

1. User input:

```
"What is weather today?"
```

2. LLM decides:

```
→ Call tool: get_weather(city="Bangalore")
```

3. MCP server executes:

```
→ Returns: {"temperature": "30°C"}
```

4. LLM receives result:

```
→ Generates final response
```

---

# ⚡ 5. Real-Time Characteristics

## ✅ Multi-step reasoning

```
User → LLM → Tool → LLM → Tool → Final
```

---

## ✅ Dynamic tool selection

LLM chooses tools at runtime:

* No hardcoding
* Context-aware

---

## ✅ Stateful

Context keeps growing:

```python
context = [
    {"role": "user", "content": "..."},
    {"role": "tool", "content": "..."}
]
```

---

## ✅ Extensible

You can add tools like:

```python
def query_db():
def call_api():
def run_model():
```

---

# 🧠 6. Upgrade to Real LLM (Next Step)

Replace `fake_llm()` with:

### Option 1: OpenAI tool calling

### Option 2: LangGraph agent

### Option 3: Custom reasoning loop

---

## Example (conceptual)

```python
llm_output = llm_with_tools(context)

if llm_output["tool_call"]:
    call_tool(...)
```

---

# 🏗️ 7. Production Architecture

```
Frontend (Streamlit / Web)
        ↓
Agent Layer (LLM + Loop)
        ↓
MCP Server (FastAPI)
        ↓
Tools:
    - APIs
    - DB
    - ML Models
```

---

# ⚠️ 8. Limitations of This Example

This is **learning-grade**, not production:

* No authentication
* No async execution
* No retries
* No streaming (WebSockets)
* No schema validation enforcement

---

# 🚀 9. Where This is Used

* AI copilots
* HR bots
* Finance assistants
* Autonomous agents
* GenAI workflows

---

# 💡 Final Takeaway

👉 MCP is NOT just APIs
👉 MCP = **LLM + Tool Execution Loop**

---

# 🔥 Next Steps

* Add streaming (WebSockets)
* Integrate LangGraph
* Add memory (Redis / DB)
* Add observability (logs + tracing)

---

**End of Document**
