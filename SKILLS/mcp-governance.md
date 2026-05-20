---
name: mcp-governance
description: Adaptive MCP capability routing, cost-aware tool orchestration, memory governance, and execution safety control.
---

# MCP Governance

## PURPOSE

Govern:
- MCP capability discovery
- tool routing behavior
- reasoning escalation
- execution cost
- context pressure
- memory consistency

---

# MCP DISCOVERY RULE

Agent should:
- detect available MCP/tools dynamically
- infer capability from tool description and behavior
- prefer capability-based selection over hardcoded tool names

Examples of capabilities:
- persistent memory
- deep reasoning
- external search
- filesystem access
- browser automation
- runtime inspection

Do NOT depend on specific vendor/tool naming.

---

# CAPABILITY ROUTING

## DEFAULT PRIORITY

1. direct reasoning
2. local filesystem/tools
3. external retrieval/search
4. persistent memory
5. deep reasoning escalation

---

# MEMORY CAPABILITY

## ROLE
Persistent long-term knowledge layer

## STORE ONLY
- architecture decisions
- durable project facts
- user preferences
- cross-session continuity
- stable system state

## NEVER STORE
- logs
- runtime noise
- debug output
- temporary execution state

## RULE
Persistent memory != ./temp runtime state

- persistent memory = durable knowledge
- ./temp = ephemeral execution layer

Never duplicate both.

---

# DEEP REASONING CAPABILITY

## ROLE
High-cost cognitive escalation layer

## USE ONLY WHEN
- multi-step reasoning required
- repeated failure after retry
- cross-module/system analysis required
- architecture-level debugging required

## DO NOT USE WHEN
- localized fixes
- deterministic problems
- direct reasoning is sufficient

## COST RULE
- high latency
- high token usage
- not default behavior
- use sparingly

---

# EXTERNAL SEARCH CAPABILITY

## ROLE
External knowledge retrieval

## USE WHEN
- external/current information required
- documentation lookup required
- API/library behavior uncertain
- verification against external source needed

## DO NOT USE WHEN
- answer exists locally
- reasoning alone is sufficient
- local project state already contains truth

---

# TOOL SAFETY

- avoid repeated identical tool calls
- avoid broad repo scans
- avoid unbounded recursion
- prefer bounded scope
- truncate oversized outputs
- summarize before persistence

---

# CONTEXT CONTROL

- minimize raw tool output
- compress large results into summaries
- avoid replaying unchanged state
- avoid unnecessary context expansion

---

# FAILURE ESCALATION

retry once only

if failure persists:
1. reduce scope
2. switch strategy
3. log into ./temp/defects.md
4. stop infinite retry loops

---

# COST-AWARE EXECUTION

Prefer:
- direct reasoning
- targeted reads
- localized edits
- minimal tool usage

Avoid:
- excessive MCP chaining
- repeated reasoning escalation
- unnecessary external retrieval
- full repository analysis