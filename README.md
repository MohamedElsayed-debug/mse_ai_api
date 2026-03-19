# 🔥 mse_ai_api - ChatGPT Proxy
🚀 Turn ChatGPT into a FREE OpenAI API in seconds (No API Key Required)
<div align="center">
  <img src="https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge&logo=playwright&logoColor=white" alt="Playwright" />
  <img src="https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge" alt="License" />
</div>

<br>

<div align="center">
  <h3>Watch the Full Tutorial on YouTube</h3>
  <a href="https://youtube.com/"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="YouTube Tutorial" /></a>
  <br>
  <em>Learn how to install, set up, and build AI workflows with mse_ai_api</em>
</div>

<br>

**The ultimate lightweight, open-source bridge to connect n8n with ChatGPT for FREE.**

---

## 🌟 Overview

**mse_ai_api** is a high-performance proxy server built with **FastAPI** and **Playwright**. It perfectly mimics the official OpenAI API structure, tricking ChatGPT's free web interface into acting as a legitimate API endpoint. It serves as a seamless drop-in replacement for n8n's OpenAI and HTTP nodes. 

Recently completely rewritten, this version now supports **Advanced AI Agent Tool Calling** effortlessly, bypassing strict JSON validation errors.

### ✨ Key Features
- 💸 **Zero API Costs**: Uses ChatGPT's web interface via background browser automation.
- ⚡ **Lightning Fast**: Built on asynchronous Python (FastAPI).
- 🤖 **Full n8n Agent Support**: Supports full ChatGPT tool calling and JSON parsing. 
- 🐳 **Dockerized**: Deploy flawlessly in seconds.
- 🔒 **Secure**: Protected by your own explicit API Secret Key.

---

## ⚙️ How It Works (Under the Hood)

This API relies on a clever technical architecture in `main.py` that makes it robust enough for production AI workflows:

1. **`AsyncBrowserThread` (The Engine)**: Instead of spinning up a new browser per request, the API launches a single detached Python thread running an asynchronous Chrome browser via Playwright. It uses deep anti-bot bypass techniques (`--disable-blink-features=AutomationControlled`, spoofed user agents, webdriver hiding) so ChatGPT thinks it's a real user.
2. **Smart Prompt Injection (`format_prompt` & `format_tools_instruction`)**: When n8n sends tools (using AI Agent nodes), the script dynamically rebuilds the user prompt. It forcefully injects precise system instructions that command ChatGPT to output **only valid JSON**. This guarantees that the web version of ChatGPT acts exactly like the programmatic API.
3. **Regex parsing (`parse_tool_calls`)**: Once ChatGPT replies, the proxy scans the response for JSON blocks. If ChatGPT signals intent to use a tool, the proxy extracts it, formats it gracefully to meet OpenAI's strict function calling schema, and alerts n8n to execute the tool locally.
4. **Flexible Endpoints**: It natively supports both `/v1/chat/completions` (Legacy n8n setups) and `/v1/responses` (Modern Responses API) ensuring broad compatibility.

---

## 🛠️ Quick Start

### 1. Using Docker (Highly Recommended)
Deploying with Docker guarantees that all dependencies (including headless Chrome and Google fonts) are perfectly configured.

```bash
# Clone the repository
git clone https://github.com/MohamedElsayed-debug/mse_ai_api.git
cd mse_ai_api

# Run with Docker Compose
docker-compose up --build -d
```
The server will now be listening silently on `http://localhost:7777`.

### 2. Manual Installation
Requires **Python 3.10** (Recommended).
```bash
pip install -r requirements.txt
python main.py
```

---

## 🔌 Connecting to n8n

### Using the HTTP Node
1. Add an **HTTP Request** node in your n8n workflow.
2. Set Method to `POST`.
3. Set URL to: `http://0.0.0.0:7777/v1/chat/completions` (or `/v1/responses`).
4. Add Header: `Authorization: Bearer change-secret-key-2026`.
5. Body (JSON): 
```json
{
  "messages": [{"role": "user", "content": "Hello, AI!"}],
  "model": "gpt-4o-mini"
}
```

### Using the OpenAI Node (Recommended)
1. In n8n, create a new **OpenAI Account** credential.
2. Set the Base URL to exactly: `http://0.0.0.0:7777/v1`
3. Set the API Key to your server's secret (`change-secret-key-2026` by default).
4. You can now use this credential across any AI Agent or LLM node seamlessly!

---

## 💎 Need Enterprise Power? Upgrade to PRO!

**mse_ai_api** is amazing for personal workflows, but scaling requires infrastructure. Meet the **PRO Version** — built on Django for multi-tenant SaaS environments.

| Feature | mse_ai_api (This Repo) 🚀 | PRO (Django Version) 👑 |
| :--- | :---: | :---: |
| Free ChatGPT Web Backend | ✅ | ✅ |
| Advanced n8n Tool Calling | ✅ | ✅ |
| **GUI Admin Dashboard** | ❌ | ✅ Included |
| **Multi-User Management** | ❌ | ✅ Track Hundreds of Users |
| **Usage Statistics & Logging** | ❌ | ✅ Detailed Database Logs |
| **Token Tracking & Quotas** | ❌ | ✅ Hard Limits per Key |
| **Commercial Support** | ❌ | ✅ Priority Support |

### 🚀 Get the PRO Version
Perfect for startup SaaS platforms or enterprise-grade process automations.

👉 **Interested in purchasing the source code or requesting a custom integration? Let's Connect!**
- [✉️ Telegram](https://t.me/MohMsE)  
- [💼 LinkedIn](https://linkedin.com/in/mohamed-elsayed-3a319939a)
- [📘 Facebook](https://www.facebook.com/Melsayed2001)
- [🐙 GitHub](https://github.com/MohamedElsayed-debug)

---

## 📄 License
This project is open-sourced under the MIT License. See the [LICENSE](LICENSE) file for details.



