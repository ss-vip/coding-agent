---
name: tool-governance-policy
description: Governance layer for tool execution routing, cost management, and memory split optimization.
---

# TOOL GOVERNANCE POLICY

## PURPOSE
Govern the execution strategy and cost budget of discovered tools (including MCP and system commands). Optimize reasoning-to-token efficiency.

## 1. STORAGE SPLIT RULE
- **./temp/**: Strict runtime ephemeral state, failure logs, and active debug sessions.
- **Memory Infrastructure**: Discovered persistent layers are ONLY for durable facts, architecture decisions, and cross-session truths.
- **NEVER** mix or duplicate data between these two layers.

## 2. ROUTING & COST PRIORITY
1. Direct Internal Reasoning (Highest priority, default)
2. Filesystem & Standard Workspace Tools
3. Discovered Long-Term Memory Services
4. Discovered Long-Reasoning Extensions (Last resort only)

## 3. COST CONTROL & ANTI-POLLUTION
- Prevent repetitive tool invocations with identical inputs.
- Prefer targeted, narrow-scope queries over global sweeps.
- **FORBIDDEN**: Running full repository scans via external reasoning tools.

## 4. RESOLUTION RETRY LIMIT
- Long-reasoning extensions must NOT be triggered consecutively for the same error.
- If failure persists:
  → Immediately shrink execution scope.
  → Fallback to direct reasoning.
  → Log root blockers to `./temp/defects.md`.
