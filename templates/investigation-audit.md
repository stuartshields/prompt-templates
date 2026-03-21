<!-- Last updated: 2026-03-21 -->
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
1. [First step]
2. [Second step]
3. [Third step]

Constraints
- Read only. Do not modify any files.
- [Any scope limits]
- If anything is ambiguous, state your assumption and flag it.

Output
For each finding, document:
- Where: file path and line
- What: the issue
- Why it matters: impact
- Suggested fix: one sentence

Finish with the top 3 highest-impact findings.
