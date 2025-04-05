# 🧠 Multi-MCP Architecture with LangChain & OpenAI (Concept Guide)

This guide explains how to build an AI-powered system using **Model Context Protocol (MCP)** with multiple backends:

- One MCP server connected to **MongoDB** (for user management)
- One MCP server connected to a **Remote Web API** (like JSONPlaceholder)
- A frontend chat UI powered by **LangChain + OpenAI**

This is a **conceptual walkthrough**. You are encouraged to follow the architecture and implement your own version step-by-step.

---

## 🏗️ Architecture Overview

```bash
User Chat UI (Browser)
    ↓
LangChain Agent (OpenAI Model)
    ↓
 ┌──────────────┬──────────────┐
 ↓                             ↓
MCP Server (MongoDB)      MCP Server (Web API)
```

---

## 📘 Overview of Components

### 1. Chat UI (Frontend)
A simple HTML/JS frontend that:
- Takes natural language input
- Sends prompts to the backend (`/ask-ai`)
- Displays structured AI responses

### 2. LangChain Agent (Model Layer)
- Uses OpenAI (e.g. GPT-4) to interpret prompts
- Converts them into structured MCP actions like `create`, `filter`, `list`
- Chooses the appropriate tool/MCP server

### 3. MCP Server A – MongoDB (Local Backend)
- Accepts structured requests like `{ action: "create", data: { name, email } }`
- Performs DB operations
- Returns structured JSON results

### 4. MCP Server B – Web API (Remote Backend)
- Also exposes `/invoke`
- Forwards requests to a third-party API (e.g., JSONPlaceholder)
- Filters or lists results based on structured input

---

## 🔧 Implementation Guidance (Suggested Steps)

> 🛠 You will need to implement the following independently based on the architecture.

### ✅ Step 1: MongoDB MCP Server
- Build an Express.js server
- Add `/api/mcp/invoke`
- Handle actions: `create`, `list`, `filter`
- Use Mongoose or MongoDB native driver

### ✅ Step 2: Web API MCP Server
- Another Express.js server
- Still responds to `/api/mcp/invoke`
- Uses `axios` to call public APIs (like `https://jsonplaceholder.typicode.com/users`)
- Handles `list` and `filter` only

### ✅ Step 3: LangChain Agent
- Use `langchain@0.0.176` (CommonJS support)
- Define tools using `DynamicTool`
- Each tool maps to an action on an MCP server
- Use `ChatOpenAI` model to reason over input and invoke tools

### ✅ Step 4: Frontend Chat UI
- Use basic HTML/CSS/JS
- Input field + Send button
- Calls `/ask-ai` on your server
- Displays AI's structured result

---

## 🛠 Prompt Examples

```txt
Add a user named Lucky with email lucky@ai.com and role admin
List all local users
Show users with role editor
List all web users
Find web users named Leanne
```

---

## ✅ What You'll Learn

- How MCP separates **model** (reasoning) from **control** (execution)
- How to use **LangChain** to structure tool usage
- How to connect an AI model to both **databases** and **remote APIs**
- How to build scalable, pluggable AI tooling using simple JSON patterns

---

## 🌐 Tools & Tech Suggested

- [LangChain.js](https://js.langchain.com)
- [OpenAI API](https://platform.openai.com)
- [Express.js](https://expressjs.com)
- [MongoDB](https://www.mongodb.com)
- [Axios](https://axios-http.com)

---

## 🧙‍♂️ Created by
Rajendra Prasad Baral — Full-stack developer & LLM infra enthusiast

Have questions? Reach out on [LinkedIn](https://www.linkedin.com/in/rajendra13/)

---

> ✅ This guide is for learning and implementation reference. We encourage you to build your version from scratch for best understanding and customization.

