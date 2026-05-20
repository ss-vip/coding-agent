---
name: mcp-governance
description: MCP tool routing, memory policy, reasoning escalation control.
---

# MCP-GOVERNANCE

## PURPOSE
Control:
- memory
- reasoning
- external search
- tool selection

---

# MEMORY RULE

Store ONLY durable knowledge:
- architecture decisions
- stable facts

Never store:
- logs
- runtime state

---

# TOOL ROUTING

Prefer order:

1. direct reasoning
2. memory (MCP)
3. external search
4. deep reasoning (last resort)

---

# ESCALATION RULE

Use long-reasoning-mcp ONLY IF:
- repeated failure
- system-level ambiguity

---

# COST CONTROL

Avoid unnecessary:
- MCP calls
- reasoning escalation
- external search

Prefer direct execution.