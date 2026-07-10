# Agent Latency Lab — VS Code Extension

Ships the existing Lab UI (trace waterfall, fork/join critical-path detection,
what-if optimizations, cost/RAG panel) inside a VS Code Webview, with no
changes to the standalone web app's behavior.

## What works in v0.1 (ship "A" — companion viewer)

- **Agent Latency Lab: Open** — opens the full Lab UI. Simulated-workload mode
  and "Paste your trace" both work exactly as they do in the browser, since
  neither depends on a network call.
- **Agent Latency Lab: Analyze Selected Trace** — right-click a trace block in
  any editor (or the Command Palette with a selection active) and it opens
  pre-loaded into the analyzer.
- **Agent Latency Lab: Analyze Trace from Clipboard** — same, from clipboard
  contents. Handy right after your instrumented server logs a paste-ready
  block to the terminal.

**What's intentionally inert here:** the live alert feed (which polls
`/debug/alerts` on a running server) has no server to reach inside a webview
and fails silently by design — it just doesn't render, exactly like the
standalone app when no server is running.

## Build & run locally

```bash
# from vscode-extension/
./build.sh
```

Then in VS Code: open this `vscode-extension/` folder, press **F5** — this
launches an Extension Development Host window with the extension active.

## Package as a `.vsix`

```bash
npm install
./build.sh
npm run package
```

Install the result with **Extensions view → "…" → Install from VSIX…**, or
`code --install-extension agent-latency-lab-0.1.0.vsix`.
