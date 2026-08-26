# Module 3: Introduction to Model Context Protocol (MCP)

## Topics Covered

* Why MCP exists — the problem it solves
* MCP architecture (client-server)
* The three core primitives — Tools, Resources, Prompts
* MCP lifecycle
* Transport mechanisms — stdio vs Streamable HTTP
* When to use MCP vs a direct function call

## Key Concept: Why MCP Exists

Without a standard, every agent needs a custom integration for every tool — this gets messy fast as agents and tools multiply. MCP fixes this by acting as a common protocol: one standard that lets any AI agent talk to any tool server, instead of building a new integration each time.

**Simple mental model:**

Without MCP: Agent ── Custom Integration ── Tool

With MCP:    Agent ── MCP ── MCP Server ── Tool


## Key Concept: Architecture

MCP is client-server: a **Host Application** (contains the agent/LLM) → **MCP Client** → **MCP Server** (exposes tools, resources, prompts). Communication happens via JSON-RPC 2.0, a standardized message format, so it stays consistent no matter the transport underneath.

## Key Concept: The Three Primitives

* **Tools** — let the agent perform actions (search, query a DB, call an API). Owned and executed by the server.
* **Resources** — give access to data/context (files, records, documents).
* **Prompts** — reusable, standardized instruction templates.

Tools are the most commonly used primitive — MCP is often thought of as mainly a "tool layer" even though it covers all three.

## Key Concept: Lifecycle

Initialize → Discover → Operate → Shutdown

- **Initialize** — client/server establish connection, negotiate capabilities
- **Discover** — client asks what's available (e.g. `tools/list`) — tools don't need to be hardcoded
- **Operate** — client requests a tool, server executes it, returns a structured result
- **Shutdown** — session closes

Dynamic discovery is the key win here: new tools can be added to the server without touching the agent's code.

## Key Concept: Transport Mechanisms

Same JSON-RPC message format, two different delivery methods:

- **stdio** — for local servers running as a child process on the same machine. Simple, no network needed.
- **Streamable HTTP** — for remote/cloud servers. Supports multiple clients, standard auth, and can stream responses via Server-Sent Events. Supersedes the older SSE-only transport.

## Key Concept: MCP Doesn't Change How the LLM Reasons

MCP only changes the *connection layer* between an agent and its tools — it doesn't change how the LLM decides whether to use a tool in the first place. The model's reasoning process works the same either way; MCP just standardizes how the resulting tool call actually gets executed.

## Key Concept: When to Actually Use MCP

For a simple, local, tightly-coupled tool, a direct function call is often easier — MCP adds unnecessary overhead. MCP earns its place when tools are external, remote, shared across multiple apps/teams, or need to be reusable and discoverable.

## Takeaway

MCP is essentially a standardized networking layer for AI tools — it decouples *agent logic* (deciding what to do) from *tool implementation* (how it gets done), enabling interoperability, dynamic discovery, and reuse across different agents and frameworks (like LangChain) without hardcoding every integration.

## Questions I still have

* What does actually setting up and running a local MCP server look like in practice — is this something I can spin up quickly to test discovery and tool calls myself?

---

*Part of Oracle Agentic AI Foundations — Module 3*
