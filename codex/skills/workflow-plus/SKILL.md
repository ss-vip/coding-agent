---
name: workflow-plus
description: For debugging, review, tests, Git, deploys or complex coding; skip Q&A/simple text edits.
---

Follow AGENTS.md.

- Baseline affected tests; separate old/new failures; check syntax/diff.
- Check write outcome before retry; avoid duplicates.
- API/deps/schema: check callers, compatibility/migrations.
- Servers: ports/timeouts; stop only own processes. UI: test interactions/mobile/desktop.
- Review read-only unless edits requested; refactor without behavior changes.
- Loop: check progress; stop at done/blocker/stall and report.
