<!-- Last updated: 2026-03-23 -->
<!--
Template: Investigation / Audit
When to use: You want findings, not changes. Code review, security audit,
performance check, or any task where the agent should report without modifying.
Sections:
  - Focus: what to look at (narrow the scope)
  - Method: steps to follow in order
  - Constraints: read-only, scope limits
  - Output: per-finding format and summary
-->

Investigate [what] in [scope].

Focus
- [Specific area 1]
- [Specific area 2]
- [Specific area 3]

Method
1. [Phase 1 — e.g. map all entry points]
2. [Phase 2 — e.g. trace data flow through each path]
3. [Phase 3 — e.g. check each path against criteria]

Constraints
- Read only. Do not modify any files.
- Limit scope to [boundary — e.g. only files in src/auth/]. [Why — e.g. the rest of the codebase is out of scope for this audit]
- If anything is ambiguous, state your assumption and flag it.

Output
For each finding, document:
- Where: file path and line
- What: the issue
- Why it matters: impact
- Suggested fix: one sentence

Before finishing, verify your findings are consistent — no contradictions, no duplicates, no findings outside the stated scope.

Finish with the top 3 highest-impact findings.

Examples (optional)
[1-3 examples of the kind of findings you expect. Remove this section if not needed.]
