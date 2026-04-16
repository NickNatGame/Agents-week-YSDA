# AI Shopping Agents

A small pet project that explores three practical agent patterns on top of a simple product catalog:

- tool-calling shopping agent
- memory-enabled shopping agent
- multi-agent recommendation pipeline

The implementation lives in [submission.ipynb](/home/nikita/proj/Agents_Week/Agents-week-YSDA/submission.ipynb).

## Features

- product search with category, brand, and price filters
- add-to-cart tool usage
- short-term memory through conversation history
- long-term memory through a JSON user profile
- multi-agent orchestration for retrieval, pros, cons, ranking, and cart actions

## Architecture

### Tool-Calling Agent

Uses an LLM with tools in a ReAct-style loop:

- `search_products`
- `add_to_cart`

Entry point:

- `run_shopping_agent(...)`

### Memory Agent

Extends the shopping agent with:

- short-term memory from previous messages
- long-term memory stored in a JSON profile

Main functions:

- `load_profile(...)`
- `save_profile(...)`
- `update_profile(...)`
- `run_memory_agent(...)`

### Multi-Agent System

Uses a shared `AgentContext` and a coordinator:

- `RetrieverAgent` finds candidates
- `ProsAgent` writes product strengths
- `ConsAgent` writes product weaknesses
- `RankerAgent` picks the best option using deterministic logic
- `CoordinatorAgent` runs the full pipeline and adds the best item to cart if requested

## Tech Stack

- `Python`
- `LangChain`
- `langchain-openai`
- `python-dotenv`
- Yandex Cloud LLM API via `ChatOpenAI`

## Run

Install dependencies:

```bash
pip install langchain-openai langchain-core python-dotenv jupyter
```

Create `MY_KEY.env`:

```env
YANDEX_CLOUD_FOLDER=your_folder_id
YANDEX_CLOUD_API_KEY=your_api_key
```

Start the notebook:

```bash
jupyter notebook submission.ipynb
```

## Example Queries

- `Find wireless headphones under 150 dollars`
- `Find a wireless mouse under 120 dollars and add the cheapest one to cart`
- `My name is Anna, I prefer Sony and my budget is 200 dollars`
- `Find the best wireless mouse under 120 dollars and add it to cart`