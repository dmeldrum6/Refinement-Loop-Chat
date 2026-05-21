# Refinement-Loop-Chat

A single-file, self-contained chat client for any OpenAI-compatible LLM API. Drop it in a browser — no build step, no dependencies, no server.

![Static Badge](https://img.shields.io/badge/single--file-HTML-cyan) ![Static Badge](https://img.shields.io/badge/no_dependencies-black)

---

## Features

- **Streaming responses** with a live cursor and real-time code fence preview
- **Refinement loop** — automatically sends the model's response back for self-critique and improvement, with configurable iterations and temperature
- **Markdown rendering** — bold, italic, headings, and fenced code blocks with language labels and copy buttons
- **Per-message stats** — response time (ms) and token counts (prompt ↑ / completion ↓) shown in each message header, including each refinement pass
- **Copy buttons** — one on every message header for full text, one on every code block
- **Session export / import** — save and restore full conversations as JSON, including all settings
- **Persistent settings** — endpoint, model, system prompt, temperature, and refinement config are saved to `localStorage`
- **Responsive layout** — sidebar collapses on narrow viewports

---

## Usage

1. Download `RefinementLoopChat.html`
2. Open it in any modern browser (file:// works fine)
3. Set your endpoint URL and model name in the sidebar
4. Chat

No installation, no npm, no bundler.

---

## Endpoint Presets

| Preset | URL |
|---|---|
| LM Studio | `http://127.0.0.1:1234/v1/chat/completions` |
| Ollama / OpenAI proxy | `http://127.0.0.1:11434/v1/chat/completions` |
| OpenAI | `https://api.openai.com/v1/chat/completions` |
| Custom | Any OpenAI-compatible endpoint |

An API key field is available for services that require one. Enabling "Remember API key" stores it in `sessionStorage` for the current browser session only.

---

## Refinement Loop

When enabled, after the model produces its initial response the client automatically sends it back with a critique prompt, asking the model to review and improve its own output. You can configure:

- **Iterations** (1–5) — how many review passes to run
- **Temperature** — typically lower than the main temperature for more focused revisions
- **Instruction** — the critique prompt itself, with `{{PROMPT}}` and `{{RESPONSE}}` placeholders
- **Show details** — toggle visibility of the refinement input/output in the chat log

---

## Extra JSON Params

The "Extra JSON Params" field accepts a JSON object that is merged into the request body, allowing you to pass model-specific parameters not exposed in the UI — for example:

```json
{"top_p": 0.9, "repeat_penalty": 1.1}
```

---

## Export Format

Exported sessions are plain JSON containing all settings, the conversation history, and a full transcript with timestamps. Importing a session restores the conversation and all sidebar settings exactly as they were.

---

## Browser Compatibility

Requires a browser with `fetch`, `ReadableStream`, and `navigator.clipboard` support. All current versions of Chrome, Firefox, Safari, and Edge work.
