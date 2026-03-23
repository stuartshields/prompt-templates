<!-- Last updated: 2026-03-23 -->
<!--
Template: Review
When to use: You want a second opinion on work already done. Code review,
spec review, plan review, or checking work against a standard.
Sections:
  - Intent: what the code is supposed to do (helps reviewer assess correctness)
  - Scope: what to review (files, branch, diff range)
  - Review for: numbered angles to assess against
  - Constraints: read-only, severity levels
  - Output: findings format and overall verdict
-->

Review [what] against [standard].

Intent
[One sentence: what this code is supposed to do and why it exists]

Scope
[Files, branch, diff range]

Review for
1. [Angle 1 - e.g. does it match the spec]
2. [Angle 2 - e.g. are there edge cases missed]
3. [Angle 3 - e.g. does it follow project patterns]

Constraints
- Read only. Report findings, do not fix them.
- Flag severity: critical, should-fix, nitpick
- If you are unsure about intent, flag it as a question rather than a finding.

Output
- List of findings with severity, file, and one-line description
- Before finishing, re-read the Intent section and verify your findings are relevant to what this code is supposed to do — not just general style preferences
- Overall verdict: ship it, fix these first, or rethink the approach

Examples (optional)
[1-3 examples of the kind of findings you expect. Remove this section if not needed.]
