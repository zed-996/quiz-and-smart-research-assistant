# 🧠 Single Agent Pipeline Project

A **Single-Agent Smart Assistant** built in Python that understands user queries, routes tasks based on intent, uses the appropriate tool, and returns structured JSON output.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Tools](#tools)
- [Setup & Installation](#setup--installation)
- [Usage](#usage)
- [Output Format](#output-format)
- [Example Queries](#example-queries)
- [Project Structure](#project-structure)

---

## Overview

This project implements a single-agent pipeline that acts as a smart assistant. The agent receives a natural-language query, classifies the user's intent, routes the query to the correct tool, and returns a structured JSON response. It demonstrates core concepts of agentic AI - intent classification, conditional routing, tool integration, and error handling.

---

## Features

### Core
- **Intent Classification** - Keyword and regex-based classifier that detects user intent from natural language.
- **Conditional Routing** - Routes queries to the appropriate tool based on classified intent.
- **Tool Integration** - Modular tools that the agent can invoke.
- **Structured JSON Output** - Every response follows a consistent `{type, result}` schema.
- **Error Handling** - Graceful error handling at both the classification and tool-execution layers.

### Additional
- **Improved Routing** - Multiple trigger words per intent, regex-based math expression detection (e.g., `"2 + 3"` routes to calculator without the word "calculate").
- **Logging** - Full logging of queries, intent classification, tool inputs/outputs, and errors using Python's `logging` module.
- **3 Additional Tools** - Sentiment Analyzer, Text Summarizer, and Date/Time tool.

---

## Architecture

```
User Query
    │
    ▼
┌──────────────────┐
│ Intent Classifier │  ← keyword matching + regex patterns
└────────┬─────────┘
         │
         ▼
┌──────────────────────────────────────────────────┐
│              Conditional Router                   │
│                                                   │
│  calculation ──► Calculator Tool                  │
│  keywords    ──► Keyword Extractor Tool           │
│  sentiment   ──► Sentiment Analyzer Tool (Additional)  │
│  summarize   ──► Text Summarizer Tool (Additional)     │
│  datetime    ──► Date/Time Tool (Additional)           │
│  general     ──► Fallback Response                │
└────────┬─────────────────────────────────────────┘
         │
         ▼
   Structured JSON Response
```

---

## Tools

| # | Tool | Trigger Words | Description |
|---|------|---------------|-------------|
| 1 | **Calculator** | calculate, compute, solve, evaluate, math, or raw expressions like `2+3` | Evaluates mathematical expressions |
| 2 | **Keyword Extractor** | keywords, extract, key words, important words | Extracts up to 5 unique keywords (words with >4 characters) |
| 3 | **Sentiment Analyzer** *(Additional)* | sentiment, feeling, mood, opinion, tone | Rule-based positive/negative/neutral/mixed classification |
| 4 | **Text Summarizer** *(Additional)* | summarize, summary, brief, shorten, tldr | Extractive summarization using word-frequency scoring |
| 5 | **Date/Time** *(Additional)* | time, date, today, day, clock, now | Returns current date, time, and day of the week |

---

## Setup & Installation

### Prerequisites
- Python 3.8 or higher

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run the Notebook

```bash
jupyter notebook week_8_assignment.ipynb
```

Or run all cells non-interactively:

```bash
jupyter nbconvert --to notebook --execute week_8_assignment.ipynb --output week_8_assignment_executed.ipynb
```

> **Note:** The interactive mode cell at the end requires manual input. When running non-interactively, you may skip or comment out that cell.

---

## Usage

Run all cells in the notebook sequentially. The agent can be used in two ways:

### 1. Programmatic
```python
result = agent("Calculate 20 + 5")
print(result)
# {'type': 'calculation', 'input': '20 + 5', 'result': '25'}
```

### 2. Interactive Mode
The last cell launches an interactive loop where you can type queries and receive responses in real time. Type `exit` to quit.

---

## Output Format

Every response from the agent follows a consistent JSON structure:

```json
{
  "type": "calculation | keywords | sentiment | summarize | datetime | general | error",
  "input": "...(the extracted input sent to the tool)...",
  "result": "...(tool output)..."
}
```

---

## Example Queries

| Query | Type | Result |
|-------|------|--------|
| `Calculate 20 + 5` | calculation | `25` |
| `Extract keywords from Artificial Intelligence is transforming industries` | keywords | `['artificial', 'intelligence', 'transforming', 'industries']` |
| `What is machine learning?` | general | Fallback response |
| `Analyze the sentiment of This product is amazing` | sentiment | `{"sentiment": "positive", ...}` |
| `Summarize: ML is a branch of AI. It learns from data.` | summarize | Extractive summary |
| `What is the date and time now?` | datetime | `{"date": "...", "time": "...", "day": "..."}` |
| `Compute 100 * 3 + 50` | calculation | `350` |

---

## Project Structure

```
week8/
├── README.md                          
├── requirements.txt                   
└── week_8_assignment.ipynb     
```
