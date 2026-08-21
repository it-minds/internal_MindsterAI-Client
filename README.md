# LLM Gateway Chat Client (Single-File PWA)

A zero-dependency, single-file chat client for our internal LiteLLM gateway. One HTML file, no build step, no frameworks, no external CDNs. Open it in a browser, paste your gateway key, and chat with the models your key has access to.

This is an adapted edition of an OpenRouter client, repointed at our LiteLLM proxy.

## Changes from the original

- API base URL changed from `https://openrouter.ai/api/v1` to our LiteLLM gateway at `https://llm-gw.itmindsinternal.dk/v1` (`/v1/models` and `/v1/chat/completions`)
- Model list parsing fixed for the OpenAI response shape (LiteLLM returns `id` without `name`)
- OpenRouter-specific request headers removed

## How to use

1. Open `index.html` in a browser, or visit the hosted URL.
2. Open **Settings & API** in the sidebar.
3. Paste your LiteLLM virtual key and save.
4. Pick a model and start chatting. The model dropdown shows only the models your key is scoped to.

All data (key, threads, messages) is stored locally in your browser via IndexedDB. Nothing is sent anywhere except directly to the gateway.

### Installing as an app (PWA)

The page generates its own manifest and service worker at runtime, so it installs like a native app. Use the "Install App" button in the sidebar, or your browser's "Add to Home Screen".

## Known limitations

- **No streaming:** responses render only when the full completion arrives, so long generations look idle while running.
- Requests appear in the gateway's spend logs under your virtual key, as with any other client.

## Credit

Based on [OpenRouter-Client](https://github.com/jimliddle/OpenRouter-Client) by Jim Liddle, MIT licensed. All the heavy lifting (the single-file PWA design, IndexedDB storage, threading, and UI) is his work; this edition only repoints the API endpoints and adjusts response parsing for LiteLLM.

Licensed under MIT, same as the original.
