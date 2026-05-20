---
name: devops-runtime
description: Cross-OS detached runtime lifecycle management with anti-hang safeguards, timeout enforcement, and safe process orchestration.
---

# DevOps Runtime

## PURPOSE

Use for:
- dev server startup
- background services
- runtime lifecycle management
- port verification
- deployment/dev workflows

---

# CORE RULES

- commands must return immediately
- detached execution only
- no blocking waits
- no inline sleep chains
- timeout required for all network checks
- verify PID before port checks
- terminate tracked PIDs only

---

# FORBIDDEN

BAD:

```bash
npm run dev && curl localhost:3000
bun dev ; sleep 5
pkill node
killall node
taskkill /IM node.exe
```

---

# DETACHED LIFECYCLE

## Phase N

- spawn detached process
- redirect stdout/stderr
- persist PID/port/state
- exit immediately

Persist runtime state into:

```text
./temp/active_sessions.json
```

---

## Phase N+1

- verify PID exists
- inspect stderr delta
- verify port readiness
- use timeout-protected health checks
- never infinite loop

---

# TIMEOUT RULES

All:
- HTTP
- socket
- fetch
- IPC

must enforce:

```text
timeout <= 2000ms
```

---

# CROSS-OS COMMANDS

## Windows

Port check:

```powershell
netstat -ano | findstr <port>
```

Kill process:

```powershell
taskkill /F /PID <pid>
```

---

## Unix/Linux/macOS

Port check:

```bash
lsof -i :<port> -t
```

Kill process:

```bash
kill -9 <pid>
```

Only terminate tracked PIDs.

---

# FILE RULES

- avoid broad scans
- avoid massive rewrites
- prefer targeted reads
- prefer line-range modifications

---

# SANDBOX RULES

Temporary/debug scripts:
- must remain inside ./temp/
- should use timestamp-based names
- must be deleted after successful verification

---

# FAILURE RECOVERY

1. inspect stderr/log delta
2. retry once only
3. reduce execution scope
4. log into ./temp/defects.md
5. stop infinite retry loops

---

# VERIFICATION

Verify impacted scope only:
- relevant tests
- relevant lint/typecheck
- PID cleanup
- orphan port cleanup
- temp leakage check

---

# COMMUNICATION

- concise
- structured
- zh-Hant-TW explanations
- English technical terminology