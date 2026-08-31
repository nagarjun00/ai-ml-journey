
# Module 4 — OpenAI Responses API and Agents SDK Basics

> Part of: **Oracle Agentic AI Foundations (2026)**

## Topics Covered

* OpenAI Agent Stack
* Responses API
* Agents SDK
* Tools and Function Calling
* Multi-Agent Systems and Handoffs
* Guardrails and Safety

**Skill Check: Module Completed**

## Key Concept: The Agent Stack

An AI agent is more than an LLM generating text. It combines:

- A model for reasoning
- Instructions that guide behavior
- Tools for performing actions
- Memory / conversation context
- Guardrails for safety

User → Agent/Application → LLM Reasoning → Tools/Functions/External Systems → Result


## Key Concept: Responses API

Built for agentic workflows, not just text generation — the model can generate a response, request a tool call, use conversation context, or return structured output.

App → Responses API → Model decides → generates response OR requests tool

→ App executes tool → result returned to model → final response

The model never executes code directly — it only *requests* a tool call; the application handles actual execution (same principle as LangChain's "under the hood" flow from Module 2).

## Key Concept: Agents SDK

A higher-level framework that organizes agents, instructions, tools, handoffs, and guardrails, instead of managing every interaction manually.


App → Responses API → Model decides → generates response OR requests tool

→ App executes tool → result returned to model → final response


The model never executes code directly — it only *requests* a tool call; the application handles actual execution (same principle as LangChain's "under the hood" flow from Module 2).

## Key Concept: Agents SDK

A higher-level framework that organizes agents, instructions, tools, handoffs, and guardrails, instead of managing every interaction manually

User Request → Agent → Reasoning → Tool or Another Agent → Result → Final Response

## Key Concept: Tools & Function Calling

Tools let an agent interact with systems outside the model — search, DB queries, APIs, calculations. The model decides *which* function to call, *when*, and *what arguments* to pass — but execution happens outside the model, in application code.

Question → Agent analyzes → needs a tool? → select tool → provide args

→ tool executes → result returned → agent responds

## Key Concept: Multi-Agent Systems & Handoffs

Complex problems can be split across specialized agents, coordinated by a main agent. A **handoff** is when one agent transfers a task to a more specialized one (e.g. support agent → billing agent). This keeps agents focused, reduces complexity, and scales better than one agent trying to do everything.

Main Agent → Support Agent / Billing Agent / Technical Agent

## Key Concept: Guardrails & Safety

Since agents can take real actions via tools, guardrails control what requests it handles, what tools it can access, and catch unsafe inputs/outputs — applied both before and after the agent processes a request.

User Input → Input Guardrail → Agent + Tools → Output Guardrail → Final Response

More tool access = more capability, but also more need for control.

## Takeaway

The core insight: **Agent = LLM + Instructions + Tools + Function Calling + Handoffs + Guardrails.** The LLM reasons and decides; tools let it act. Responses API provides the interaction interface, Agents SDK structures the full workflow. This mirrors Module 2's LangChain loop (reason → act → observe) — same underlying pattern, just OpenAI's own stack instead of LangChain's abstractions.

## Questions I still have

* How do handoffs preserve context — does the receiving agent get full conversation history or just a relevant summary?

---

*Part of Oracle Agentic AI Foundations — Module 4*
