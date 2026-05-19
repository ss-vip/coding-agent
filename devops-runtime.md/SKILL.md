---
name: devops-runtime
description: Non-blocking cross-OS runtime lifecycle management with detached execution, timeout enforcement, and anti-hang safeguards.
---

# DEVOPS RUNTIME SKILL

## PURPOSE
Govern development server startups, background process monitoring, and runtime environment lifecycles.

## 1. DETACHED LIFECYCLE PROTOCOL
- **Phase N (Spawn)**: Trigger detached processes -> Redirect stdout/stderr -> Record PID/port to `./temp/active_sessions.json` -> Exit immediately.
- **Phase N+1 (Verify)**: Confirm PID exists -> Inspect stderr delta -> Execute timeout-protected healthchecks -> NEVER infinite loop.
- **Rules**: Instant command return required. Zero blocking waits or inline sleep chains. Only terminate tracked PIDs.

## 2. FORBIDDEN ANTI-PATTERNS
```bash
npm run dev && curl localhost:3000   # Blocking sync chaining
bun dev ; sleep 5                   # Uncontrolled sleep wait
killall node                        # Global untracked wipe
pkill node                          # Global untracked wipe
taskkill /IM node.exe               # Global untracked wipe
```

## 3. TIMEOUT & NETWORK ENFORCEMENT
- Strict **2000ms MAX** timeout for ALL network-bound operations (HTTP, socket, IPC, fetch).

## 4. CROSS-OS COMMAND PARADIGMS
- **Windows (CMD/PowerShell)**:
  - Port Audit: `netstat -ano | findstr <port>`
  - Force Kill: `taskkill /F /PID <pid>`
- **Unix (Linux/macOS)**:
  - Port Audit: `lsof -i :<port> -t`
  - Force Kill: `kill -9 <pid>`

## 5. RECOVERY & CLEANUP SCOPE
- **On Failure**: Inspect stderr/log -> Retry exactly ONCE -> Shrink execution scope -> Log to `./temp/defects.md` -> Stop execution loop.
- **Verification Boundaries**: Clean up orphaned PIDs/ports, audit impacted sub-systems only, and ensure zero temp file leakage.
