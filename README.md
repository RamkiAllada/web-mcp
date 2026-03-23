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

### How to use webmcp

- Google Chrome Canary browser Version 148.0.7743.0 (Official Build) canary (arm64) provides a [Web-mcp extension](https://chromewebstore.google.com/detail/webmcp-model-context-tool/gbpdfapgefenggkahomfgkhfehlcenpd?pli=1).
- Installing the extension will help to scan the tools defined in the respective website page that is opened by agents to perform the defined activites under the tools.
- WebMCP proposes two new APIs that allow browser agents to take action on behalf of the user:
    --Declarative API: Perform standard actions that can be defined directly in HTML forms.
    --Imperative API: Perform complex, more dynamic interactions that require JavaScript execution.

I will be adding a sample snippet for imperative way. Adding a sample table to perform a filter operation using imperative api.
```
useEffect(() => {
  if (!('modelContext' in navigator)) return;
  const toolName = "apply_filter_v1"; // New name to ensure fresh indexing
  const mcp = (navigator as any).modelContext;
  // Cleanup old versions
  try { mcp.unregisterTool(toolName); } catch (e) {}
  const tool = mcp.registerTool({
    name: toolName,
    description: "Filters the table. Args: gender (male/female), age (number).",
    // CRITICAL CHANGE: 'inputSchema' is the correct property name for WebMCP
    inputSchema: {
      type: "object",
      properties: {
        gender: {
          type: "string",
          enum: ["male", "female", "both"],
          description: "gender type: male or female or both"
        },
        age: {
          type: "number",
          description: "Type: number. Age of the person"
        },
        searchTerm: {
          type: "string",
          description: "A specific name, age, gender to be used to search/filter the table from search box."
        }
      }
    },
    execute: async (args: any) => {
      console.log("🚀 SUCCESS! AI SENT ARGS:", args);
      // 1. filter Gender
      gender = args.gender
      // 2. filter Age
      age = args.age 
      // 3. Handle Search Term
      if (args.searchTerm !== undefined) {
        // assuming searchBoxRef is created
        const input = searchBoxRef.current?.querySelector('input');
        console.log(input)
        console.log(args.searchTerm)
          if (input) {
            input.value = args.searchTerm;
          }
        if (searchFunctionRef.current) {
              searchFunctionRef.current(args.searchTerm);
          }
      }

      dispatch(setTableFilter(gender, age)); // dispatching the action

      // 5. Provide Feedback to AI
      const results = tableDataRef.current?.data?.slice(0, 3).map(d =>{
        console.log(d)
        return {
           name: d.name,
          age: d.age,
          gender: d.gender
        }
      }) || [];

      return {
        success: true,
        message: `Filters applied: ${args.gender || 'Any'} ${args.age || ''}. Search: ${args.searchTerm || 'None'}`,
        preview: results
      };
    }
  });

  return () => {
    if (tool && typeof tool.unregister === 'function') tool.unregister();
  };
}, [dispatch]);
```


## Summary

> WebMCP transforms your website into an **agent-accessible interface**, enabling AI systems to interact with it as a structured, predictable environment rather than relying on fragile UI automation techniques.
