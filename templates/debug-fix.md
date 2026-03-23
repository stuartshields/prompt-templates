<!-- Last updated: 2026-03-23 -->
<!--
Template: Debug / Fix
When to use: Something is broken and you need it fixed. Bug reports, error
investigation, or any task where the starting point is broken behaviour.
Distinct from Build (starts from a blank slate) and Investigation (reports
without fixing).
Sections:
  - Expected / Actual: what should happen vs what happens
  - Error: exact error message, log output, or screenshot
  - Reproduction: steps to trigger the bug
  - Already tried: what you've ruled out (prevents the agent retreading ground)
  - Constraints: scope limits, things to avoid
  - Verification: how to confirm the fix works
-->

Fix [symptom] in [where].

Expected
[What should happen]

Actual
[What happens instead]

Error
[Exact error message, stack trace, or screenshot. "No error" if it fails silently.]

Reproduction
1. [Step to trigger the bug]
2. [Step]
3. [Observe: symptom]

Already tried
- [What you've already checked or ruled out. "Nothing yet" if fresh.]

Constraints
- Only modify files in [scope]. [Why — e.g. other areas have a pending refactor]
- Do not [specific thing to avoid — e.g. do not refactor surrounding code, do not change the test suite]
- If the root cause is unclear after investigation, report your findings and ask before changing code.

Verification
- Run [command] and confirm [expected output]
- Confirm no regressions: [how to check]
- Verify the fix addresses the root cause, not just the observable symptom
