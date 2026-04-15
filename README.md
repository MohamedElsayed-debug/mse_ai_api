# 🔥 mse_ai_api — ChatGPT AI Automation Helper

<div align="center">

[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com)
[![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge&logo=playwright&logoColor=white)](https://playwright.dev)
[![Python](https://img.shields.io/badge/Python_3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

**Turn ChatGPT into a FREE OpenAI-compatible API in seconds — no API key required.**

<br>

<div align="center">
  <h3>Watch the Full Tutorial on YouTube</h3>
  <a href="https://www.youtube.com/watch?v=e_9tMLRXeKY">
    <img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="YouTube Tutorial" />
  </a>
  <br>
  <em>Learn how to install, set up, and build AI workflows with mse_ai_api</em>
</div>

</div>

---

## ❤️ Sponsors

- [Kareem Adel](https://www.facebook.com/Kareemadel.official.account) — Owner & CEO at Wzila

---

## 🌟 Overview

**mse_ai_api** is a high-performance proxy server built with **FastAPI** and **Playwright**. It perfectly mimics the official OpenAI API structure by automating ChatGPT's free web interface in the background — making it a seamless drop-in replacement for n8n's OpenAI and HTTP nodes.

This version has been **completely rewritten** to support **Advanced AI Agent Tool Calling** reliably, bypassing strict JSON validation errors that plagued earlier approaches.

---

## ✨ Key Features

- 💸 **Zero API Costs** — Uses ChatGPT's web interface via background browser automation
- ⚡ **Lightning Fast** — Built on asynchronous Python with FastAPI
- 🤖 **Full n8n Agent Support** — Advanced ChatGPT tool calling and JSON parsing
- 🔌 **OpenAI-Compatible** — Drop-in replacement for OpenAI API clients
- 🐳 **Dockerized** — One-command deployment
- 🔒 **Secure** — Protected by your own configurable API secret key

---

## ⚙️ How It Works

This proxy relies on a robust technical architecture in `main.py` designed for production AI workflows:

1. **`AsyncBrowserThread` (The Engine)** — Instead of spinning up a new browser per request, the API launches a single detached Python thread running an async Chrome browser via Playwright. It uses anti-bot bypass techniques (`--disable-blink-features=AutomationControlled`, spoofed user agents, webdriver hiding) so ChatGPT treats it as a real user session.

2. **Smart Prompt Injection (`format_prompt` & `format_tools_instruction`)** — When n8n sends tool definitions (via AI Agent nodes), the script dynamically rebuilds the prompt and injects precise system instructions commanding ChatGPT to output **only valid JSON** — guaranteeing it behaves like the programmatic API.

3. **Regex Parsing (`parse_tool_calls`)** — Once ChatGPT replies, the proxy scans the response for JSON blocks. If a tool call is detected, it extracts and formats it to meet OpenAI's strict function calling schema, then signals n8n to execute the tool locally.

4. **Flexible Endpoints** — Natively supports both `/v1/chat/completions` (legacy n8n setups) and `/v1/responses` (modern Responses API) for broad compatibility.

---

## 🛠️ Quick Start

### Option 1 — Docker (Recommended)

Deploying with Docker guarantees all dependencies (including headless Chrome and fonts) are perfectly configured.

```bash
git clone https://github.com/MohamedElsayed-debug/mse_ai_api.git
cd mse_ai_api
docker-compose up --build -d
```

Server starts on `http://localhost:7777`

### Option 2 — Manual

Requires **Python 3.10+**.

```bash
pip install -r requirements.txt
python main.py
```

---

## 🔧 Configuration

| Variable | Default | Description |
|---|---|---|
| `API_SECRET_KEY` | `change-secret-key-2026` | Your server's API key |

---

## 📡 API Reference

**Base URL:** `http://localhost:7777`

**Endpoints:**
- `POST /v1/chat/completions` — Legacy OpenAI-compatible endpoint
- `POST /v1/responses` — Modern Responses API endpoint

**Header:** `Authorization: Bearer <your-secret-key>`

### Example — cURL

```bash
curl -X POST "http://localhost:7777/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer change-secret-key-2026" \
  -d '{
    "messages": [{ "role": "user", "content": "Hello, AI!" }],
    "model": "gpt-4o-mini"
  }'
```

---

## 🔌 Connecting to n8n

### Via HTTP Node

1. Add an **HTTP Request** node in your n8n workflow
2. Method: `POST`
3. URL: `http://localhost:7777/v1/chat/completions`
4. Header: `Authorization: Bearer change-secret-key-2026`
5. Body (JSON):

```json
{
  "messages": [{ "role": "user", "content": "Hello, AI!" }],
  "model": "gpt-4o-mini"
}
```

### Via OpenAI Node (Recommended)

1. In n8n, create a new **OpenAI Account** credential
2. Set Base URL to: `http://localhost:7777/v1`
3. Set API Key to your server's secret (`change-secret-key-2026` by default)
4. Use this credential across any AI Agent or LLM node seamlessly!

---

## 💎 PRO Version

**mse_ai_api** is great for personal workflows. The **PRO Version** is built for teams and production environments on Django.

| Feature | This Repo | PRO Version |
|---|:---:|:---:|
| Free ChatGPT Web Backend | ✅ | ✅ |
| Advanced n8n Tool Calling | ✅ | ✅ |
| **Image Analysis (HTTP URL)** | ❌ | ✅ |
| **Image Analysis (Base64/Binary)** | ❌ | ✅ |
| **Admin Dashboard (GUI)** | ❌ | ✅ |
| **Multi-User Management** | ❌ | ✅ |
| **Usage Statistics & Logging** | ❌ | ✅ |
| **Token Tracking & Quotas** | ❌ | ✅ |
| **Priority Support** | ❌ | ✅ |

---

## 📬 Contact

Interested in the PRO version or a custom integration?

- **Telegram:** [@MohMsE](https://t.me/MohMsE)
- **LinkedIn:** [Mohamed Elsayed](https://linkedin.com/in/mohamed-elsayed-3a319939a)
- **Facebook:** [Melsayed2001](https://www.facebook.com/Melsayed2001)
- **GitHub:** [@MohamedElsayed-debug](https://github.com/MohamedElsayed-debug)

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

> **Disclaimer:** This project automates a web browser for personal and educational use. Usage must comply with the terms of service of the underlying platforms. The authors are not responsible for misuse.
