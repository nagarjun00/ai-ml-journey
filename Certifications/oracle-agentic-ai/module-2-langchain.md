# Module 2: LangChain for AI Agents

## Topics Covered

* Introduction to LangChain
* LangChain building blocks (demo)
* Building your first agent using LangChain
* LangChain Agent under the hood — Part 1 & 2

**Skill Check: 100%**

## Key Concept: What is LangChain?

LangChain is a framework for building applications powered by LLMs — it provides reusable building blocks so you don't have to wire everything (prompting, tool calls, memory, chaining steps together) by hand every time. It sits on top of a raw LLM API and adds the structure needed to build agents, not just single-turn chat completions.

## Key Concept: LangChain Building Blocks

The core pieces that get composed together:

- **LLM / Chat Model wrapper** — a standardized interface to call any underlying model (OpenAI, Anthropic, etc.) the same way
- **Prompt Templates** — reusable, parameterized prompts instead of hardcoded strings
- **Chains** — sequences of calls (e.g. prompt → LLM → parse output) linked together into a pipeline
- **Tools** — functions the agent can call (search, calculator, API calls, etc.) — conceptually the same "tools" idea from Module 1
- **Memory** — lets the agent retain context across multiple turns instead of starting fresh each call

## Key Concept: Building Your First Agent

A basic LangChain agent is assembled from:

1. An LLM (the reasoning engine)
2. A set of tools the agent is allowed to use
3. A prompt/instruction defining the agent's goal and how it should decide between reasoning and acting
4. An **agent executor** — the orchestration loop that repeatedly calls the LLM, checks if it wants to use a tool, executes the tool if so, feeds the result back in, and continues until the task is done

This directly mirrors the Goal → Reason → Act → Observe → Continue/Finish loop from Module 1 — LangChain is essentially a concrete implementation of that abstract loop.

## Key Concept: LangChain Agent Under the Hood

Underneath the abstraction, what's actually happening on each iteration:

- The LLM receives the current state — the original goal, the tools available (as descriptions/schemas), and the history of what's happened so far
- The LLM outputs either a **final answer** or an **action** (which tool to call, with what input)
- If it's an action, LangChain's executor parses that output, actually calls the specified tool, captures the result
- That result gets appended back into the context, and the LLM is called again with the updated state
- This repeats until the LLM signals it's done (returns a final answer instead of another action)

The important insight: the LLM isn't literally "calling" the tool itself — it's producing structured text output (e.g. "use tool X with input Y"), and the surrounding LangChain code is what actually parses that, executes the real function, and manages the loop. The "agency" is really a combination of the LLM's reasoning plus this orchestration code around it.

## Takeaway

LangChain turns the abstract "agent loop" from Module 1 into something concrete and buildable — prompt templates, tool wrappers, and an agent executor that handles the repeated reason → act → observe cycle. Seeing "under the hood" made it clear the LLM doesn't have some special ability to execute code — it just outputs structured intent, and the framework around it does the actual execution and looping.

## Questions I still have

* How does LangChain's agent executor decide when to stop looping if the LLM never cleanly signals "done" — is there a max iteration limit or timeout as a safety net?

---

*Part of Oracle Agentic AI Foundations — Module 2*
