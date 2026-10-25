<!-- SPECKIT START -->
For additional context about technologies to be used, project structure,
shell commands, and other important information, read the current plan
<!-- SPECKIT END -->

## Dual-Agent Workflow

This repository uses a two-agent split:

- **Planning agent (Hermes)** runs the constitution, clarify, specify, and plan phases and pushes the artifacts to `main`.
- **Implementation agent (Claude Code / OpenCode)** pulls, runs the tasks and implement phases against the committed plan, and delivers via pull requests.

Planning artifacts land directly on `main`; implementation lands only via PR. After every delivery to `main`, all clones must be synchronized (pull) before the next phase starts. Never re-implement or edit committed specs from the implementation side — raise it back through the planning agent.

`IDEA.md` is the concept source of truth until superseded by ratified specs; the constitution lives in `.specify/memory/constitution.md`.
