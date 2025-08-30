
# LLM Agent POC – Browser‑Based Multi‑Tool Reasoning

![AI Agent hero banner]({{file:file-E5hHe2YarCi5KgEnQKkfXC}})

An interactive chat interface that goes beyond plain text.  This proof‑of‑concept demonstrates how a client‑side LLM agent can orchestrate external tools — such as web search, AI Pipe completions and a secure JavaScript sandbox — to accomplish complex tasks.  Users choose their preferred LLM provider (OpenAI, Anthropic Claude, Google Gemini or AI Pipe) and the agent automatically loops through reasoning steps until it produces an answer or additional questions.

## Highlights

| Capability         | Details |
|-------------------|---------|
| **Provider Picker** | Users can switch between OpenAI, Anthropic, Gemini and AI Pipe.  The chosen provider determines the API endpoint and available models shown in the dropdown【631185742859394†L39-L71】. |
| **Tool Calls**      | The agent exposes three functions — `web_search`, `aipipe_proxy` and `js_exec` — using OpenAI‑style tool definitions【985835050613124†L106-L155】.  The LLM decides when to invoke them based on the conversation. |
| **Reasoning Loop** | Messages and tool results are accumulated in memory.  The loop repeatedly calls the LLM until there are no more tool requests or a maximum number of turns is reached【985835050613124†L246-L293】. |
| **Modern UI**       | A responsive dark/light theme with colourful chat bubbles, avatars and hover animations【966750401344927†L5-L12】.  Users can clear the conversation or export the chat history to JSON. |
| **Built‑in Search Fallback** | If Google Custom Search is not configured, the agent gracefully falls back to DuckDuckGo and Wikipedia to retrieve snippets【985835050613124†L523-L571】. |
| **Secure JS Execution** | Client‑side JavaScript is run in a sandboxed Web Worker.  Console logs, returned values and errors are streamed back to the UI【985835050613124†L602-L646】. |

## Project Structure

```text
├── index.html       # The web UI (provider selector, chat and status elements)
├── style.css        # Modern dark/light theme with gradients and animations
├── agent.js         # Core agent logic and tool integrations
└── vercel.json      # Vercel deployment config (optional)
```

### index.html

The HTML page defines the user interface: provider selection with optional Google API settings, a chat card with message bubbles and a code output panel.  Each message row displays an avatar and a coloured bubble indicating the role【631185742859394†L39-L90】.  Buttons allow users to clear the chat or export the conversation to JSON.

### agent.js

The core of the agent lives in `agent.js`.  It defines an array of tools where each entry describes the function name, description and JSON schema.  When the user sends a message, it triggers `agentLoop()`, which repeatedly calls the LLM with the conversation history and tool definitions until no further tool calls are requested or eight iterations have been performed【985835050613124†L246-L293】.  When the LLM requests a tool call, the agent dispatches the appropriate function:

* **Web search** – If Google API keys are present, the agent uses Google Custom Search to fetch snippets.  Otherwise DuckDuckGo and Wikipedia are queried as fallbacks【985835050613124†L523-L571】.
* **AI Pipe proxy** – Sends the prompt to the AI Pipe OpenRouter‑compatible endpoint and returns a short completion.  The code automatically retrieves a token from `aipipe.org` if the user is logged in.
* **JavaScript execution** – Runs untrusted code in a sandboxed Web Worker, capturing `console.log` output and return values for safe display【985835050613124†L602-L646】.

### Reasoning Strategy

The agent maintains a message array containing objects with `role` (`user`, `assistant` or `tool`) and `content`.  When the LLM returns a reply with tool calls, those calls are executed and appended as `tool` messages.  This pattern mirrors the Python pseudocode from the assignment and enables iterative reasoning.  After each tool invocation the LLM is called again with the updated context until it no longer requests any tool or the maximum iteration count is reached【985835050613124†L246-L293】.

## Running Locally

1. **Clone the repository**:

   ```bash
   git clone https://github.com/Mohdshaadsonofvakeel/LLM_Agent_helper.git
   cd LLM_Agent_helper
   ```

2. **Serve the static files**.  Because everything runs in the browser, you only need a web server.  For example, using Python:

   ```bash
   python -m http.server 8000
   ```

   Then open `http://localhost:8000` in your browser.

3. **Select your provider**.  Choose between OpenAI, AI Pipe, Anthropic or Gemini.  Paste your API key or token.  If using Google search, provide your Google API key and CSE ID (both optional).  Without these the agent falls back to DuckDuckGo and Wikipedia.

4. **Start chatting**.  Ask the agent to research topics, summarise articles, run JavaScript snippets or call pipelines.  The conversation and tool responses will appear in the chat area.

## Deployment

The project includes a `vercel.json` configuration that serves static assets for easy deployment on Vercel.  Alternatively, host the files on any static web hosting provider.

## Security & Privacy

- API keys are entered into the browser and sent directly to the selected provider.  They are **not stored or logged** by the application.
- The JavaScript execution environment is sandboxed within a Web Worker and cannot access the DOM or network.  It returns logs and results only【985835050613124†L602-L646】.
- When using AI Pipe, the script will attempt to obtain a token from `aipipe.org`.  If unavailable, users must provide their own token.

## Limitations & Future Work

- The agent currently supports three tools (web search, AI Pipe proxy and JavaScript execution).  Additional tools such as calculators, translation services or custom APIs could be integrated by extending the `tools` array.
- Google Custom Search requires a paid API key.  Without it the fallback to DuckDuckGo/Wikipedia may produce limited results【985835050613124†L523-L571】.
- Each provider imposes limits on conversation length and token usage.  The agent enforces a maximum of eight LLM turns per user message to prevent endless loops【985835050613124†L246-L293】.

## License

This project is released under the MIT License.  Feel free to modify and reuse it for your own applications.
