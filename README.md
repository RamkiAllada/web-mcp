# web-mcp

## Overview
**WebMCP** is a browser-based standard that enables AI agents to interact directly with your application's user interface in a structured and reliable way.

Unlike traditional UI automation that relies on brittle selectors or visual inference, WebMCP exposes **explicit UI capabilities** to agents, making interactions deterministic and stable.

---

## What WebMCP Does

WebMCP operates at the **frontend layer** and provides:

- A **browser-based interface** for AI agents  
- Structured access to **UI actions and workflows**  
- Ability for agents to interact with **live web applications**  

---

## Key Characteristics

### Frontend-Oriented
- Runs entirely in the browser
- Works with the live DOM and user session

### Agent-Driven Interaction
- Enables AI agents to:
  - Click elements
  - Fill forms
  - Navigate pages
  - Trigger UI workflows

### Context-Aware
- Uses:
  - Active session
  - Cookies
  - Real-time page state

---

## Lifecycle Constraints

WebMCP is **ephemeral and context-bound**, meaning:

- Works only when:
  - The webpage is **open**
  - The user is **active in the browser tab**

-  Does NOT work:
  - In background processes
  - Without an active browser session

---

## When to Use WebMCP

Use WebMCP when you need:

- AI agents to interact with **real user interfaces**
- Reliable execution of **UI-based workflows**

---

## Limitations

- Not suitable for backend automation
- Not designed for headless or offline execution
- Requires an active browser environment

---

## Positioning

WebMCP is best used alongside backend protocols like MCP:

- **WebMCP (Frontend)** → UI interaction  
- **MCP (Backend)** → Data, APIs, business logic  

---

## Summary

> WebMCP transforms your website into an **agent-accessible interface**, enabling AI systems to interact with it as a structured, predictable environment rather than relying on fragile UI automation techniques.
