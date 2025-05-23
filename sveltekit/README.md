##  Dockerized MCP Server for SvelteKit Docs

This repository provides a Docker image that wraps the [`mcp-svelte-docs`](https://www.npmjs.com/package/mcp-svelte-docs) Model Context Protocol (MCP) server, enabling intelligent access to the SvelteKit documentation through tools like [Cursor](https://www.cursor.sh/) or VS Code with the MCP extension.

---

## 🚀 Quickstart


### 1. (Optional) Test it manually

```bash
docker run -i --rm mcp-svelte-docs:latest
```

This will launch the MCP server and wait for commands over `stdin`.

---

### 2. Use in Cursor or VS Code MCP config

#### For **Cursor IDE**:

Edit or create `.cursor/config.json` in your project root:

```json
{
  "mcpServers": {
    "mcp-svelte-docs": {
      "command": "docker",
      "args": [
        "run", "-i", "--rm",
        "mcp-svelte-docs:latest"
      ]
    }
  }
}
```

#### For **VS Code (with MCP extension)**:

Edit `.vscode/settings.json`:

```json
{
  "mcp.servers": {
    "mcp-svelte-docs": {
      "command": "docker",
      "args": [
        "run", "-i", "--rm",
        "mcp-svelte-docs:latest"
      ]
    }
  }
}
```

---

## 🛠 How It Works

* The `mcp-svelte-docs` package is an MCP-compliant server that indexes and exposes SvelteKit documentation.
* MCP-aware IDEs (like Cursor) can spawn this server to answer tool requests such as:

  * `"tool": "mcp.call", "resource": "svelte://docs", "operation": "search_docs"` or similar.

---

## 🧪 Example Call (from within IDE)

```json
{
  "tool": "mcp.call",
  "resource": "svelte://docs",
  "operation": "search_docs",
  "query": "page layout"
}
```

---

## 🧼 Clean Up

```bash
docker image rm mcp-svelte-docs
```

---

Let me know if you'd like this packaged into a GitHub repo structure or want to support mounting custom doc paths or caching.
