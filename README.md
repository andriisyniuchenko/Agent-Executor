# ReAct Agent with LangGraph

A ReAct (Reason + Act) agent built with LangGraph and Groq LLama that can search the web and perform calculations.

## How it works

```
main.py      → defines HOW the graph flows (nodes, edges, conditions)
nodes.py     → defines WHAT each node does (LLM reasoning, tool execution)
react.py     → defines WHAT tools and model are used (Groq LLama + TavilySearch + triple)
```

### Flow

```
[START] → agent_reason → (has tool_calls?) → YES → act → agent_reason (loop)
                                           → NO  → [END]
```

1. `agent_reason` — LLM receives the conversation state and decides what to do
2. `act` — executes the tool chosen by the LLM and returns the result
3. Loop continues until LLM produces a final answer with no tool calls

### Tools

- `TavilySearch` — web search
- `triple(num)` — multiplies a number by 3

## Setup

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Copy `.env.example` to `.env` and fill in your API keys:

```bash
cp .env.example .env
```

## Run

```bash
python main.py
```