---
name: devops-runtime
description: OS-level process lifecycle, shell execution, anti-hang enforcement.
---

# DEVOPS-RUNTIME

## PURPOSE
Handle OS execution tasks:
- dev server
- build scripts
- process management
- port verification

---

# RULES

- all commands must be non-blocking
- no interactive processes
- detached execution required
- PID must be tracked if persistent

---

# ANTI-HANG

- no blocking chains
- no sleep-based waiting
- no interactive REPL

TIMEOUT:
<= 2000ms for network operations

---

# FORBIDDEN

- npm run dev && curl
- sleep loops
- pkill node (unless tracked PID)

---

# CROSS-OS

Windows:
netstat -ano | findstr <port>
taskkill /F /PID <pid>

Unix:
lsof -i :<port> -t
kill -9 <pid>

---

# OUTPUT

Always assume background execution.
Never block kernel flow.