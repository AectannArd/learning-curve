<!-- SPECKIT START -->
For additional context about technologies to be used, project structure,
shell commands, and other important information, read the current plan
<!-- SPECKIT END -->

## Implementation Agent Guide

You are the implementation agent in this repository's dual-agent workflow. Specs and plans arrive via git from the planning agent.

- Run the **tasks** and **implement** phases strictly against the committed plan; do not re-specify or redesign.
- Follow the constitution in `.specify/memory/constitution.md` (test-first development, quality gate, CI-green completion).
- Course content (chapters, task statements) and reference solutions are production code here: every user-visible change ships with its documentation delta in the same PR.
- Deliver through pull requests only; watch CI until all jobs are green before reporting completion.
