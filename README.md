# LLM Agent POC – Browser‑Based Multi‑Tool Reasoning

 :agentCitation{citationIndex='0' label='AI Agent hero banner'}


An interactive chat interface that goes beyond plain text.  This proof‑of‑concept demonstrates how a client‑side LLM agent can orchestrate external tools — such as web search, AI Pipe completions and a secure JavaScript sandbox — to accomplish complex tasks.  Users choose their preferred LLM provider (OpenAI, Anthropic Claude, Google Gemini or AI Pipe) and the agent automatically loops through reasoning steps until it produces an answer or additional questions.

## Highlights

| Capability         | Details |
|-------------------|---------|
| **Provider Picker** | Users can switch between OpenAI, Anthropic, Gemini and AI Pipe.  The chosen provider determines the API endpoint and available models shown in the dropdown:contentReference[oaicite:0]{index=0}. |
| **Tool Calls**      | The agent exposes three functions — `web_search`, `aipipe_proxy` and `js_exec` — using OpenAI‑style tool definitions:contentReference[oaicite:1]{index=1}.  The LLM decides when to invoke them based on the conversation. |
| **Reasoning Loop** | Messages and tool results are accumulated in memory.  The loop repeatedly calls the LLM until there are no more tool requests or a maximum number of turns is reached:contentReference[oaicite:2]{index=2}. |
| **Modern UI**       | A responsive dark/light theme with colourful chat bubbles, avatars and hover animations:contentReference[oaicite:3]{index=3}.  Users can clear the conversation or export the chat history to JSON. |
| **Built‑in Search Fallback** | If Google Custom Search is not configured, the agent gracefully falls back to DuckDuckGo and Wikipedia to retrieve snippets:contentReference[oaicite:4]{index=4}. |
| **Secure JS Execution** | Client‑side JavaScript is run in a sandboxed Web Worker.  Console logs, returned values and errors are streamed back to the UI:contentReference[oaicite:5]{index=5}. |

## Project Structure

```text
├── index.html       # The web UI (provider selector, chat and status elements)
├── style.css        # Modern dark/light theme with gradients and animations
├── agent.js         # Core agent logic and tool integrations
└── vercel.json      # Vercel deployment config (optional)
