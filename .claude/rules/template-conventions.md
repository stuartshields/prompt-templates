<!-- Last updated: 2026-03-23 -->

# Template Conventions

## Structure
- Every template follows four parts: Task, Context, Constraints, Output.
- Section names can vary (Focus, Method, Requirements, Review For) but the four-part intent stays the same.
- The Debug / Fix template uses a variant structure: symptom-focused (Expected / Actual / Error / Reproduction / Already tried) instead of context-focused. It omits Context and Output in favour of reproduction steps and verification.
- Bracketed text `[like this]` is a placeholder. Never leave brackets in a finished prompt.

## Named Sections
Each template uses a subset of these sections. When creating a new template, draw from this catalogue rather than inventing new names for the same concept.

- **Context**: what exists, what this connects to, why it's needed (Build)
- **Requirements**: numbered list of what must be done (Build)
- **Edge cases**: error scenarios and boundary conditions to handle (Build)
- **Done when**: success criteria — observable, testable outcomes (Build)
- **Expected / Actual / Error**: what should happen vs what does happen (Debug)
- **Reproduction**: numbered steps to trigger the bug (Debug)
- **Already tried**: what the user has checked or ruled out (Debug)
- **Focus**: specific areas to examine (Investigation)
- **Method**: ordered steps to follow (Investigation)
- **Question**: the specific decision to make (Research)
- **Priorities**: what matters most for the decision (Research)
- **Consider**: options or angles to evaluate (Research)
- **Intent**: one sentence on what the code is supposed to do (Review)
- **Scope**: files, branch, or diff range to review (Review)
- **Review for**: numbered angles to assess against (Review)
- **Constraints**: scope limits, read-only flags, things to avoid (all templates)
- **Verification**: how to confirm it works (Build, Debug)
- **Output**: per-finding format and summary (Investigation, Research, Review)
- **Examples (optional)**: 1-3 examples of expected input/output or findings (all templates)

## Tone
- Direct, second person. "Investigate X" not "Could you please investigate X."
- Imperative verbs to open: Investigate, Implement, Review, Research, Audit, Compare, Fix.
- No filler. No "please", no "I'd like you to", no "it would be great if."

## Constraints Section
- Always include. This is the most important section for consistent output.
- "Read only" or "Do not modify" must be explicit when you want investigation without changes.
- Scope limits prevent the agent wandering into adjacent work.

## Output Section
- Define the shape of the deliverable, not just "give me results."
- Per-item structure (For each finding: X, Y, Z) beats open-ended requests.
- "Finish with" or "Summarise as" gives the agent a clear stopping point.

## Success Criteria
- Build templates should define what "done" looks like, not just what to build.
- Success criteria are observable, testable outcomes — not restatements of the requirements.
- Verification tells you how to check. Success criteria tell you what to check for.

## Uncertainty Handling
- Every template should include one line telling the agent what to do when unsure.
- Build: "stop and ask rather than guessing." Debug: "report your findings and ask before changing code." Investigation: "state your assumption and flag it." Review: "flag it as a question rather than a finding." Research: "say so explicitly."
- This prevents the agent from silently guessing and producing confident-sounding wrong output.

## Examples (Optional)
- Add 1-3 examples when the output format is ambiguous or unfamiliar.
- Templates include an `Examples (optional)` section header as a reminder, except Debug / Fix where examples of expected output are rarely useful since the deliverable is a code fix. The section should only be filled in the assembled prompt — remove it if the user provides no examples.
- Anthropic recommends 3-5 examples for best results when format matters.

## Line Count
- The 30-line limit applies to the template body (the usable prompt content), not the comment block at the top. Comment blocks are metadata for template authors and are stripped when the prompt is assembled.
- If the body exceeds 30 lines, split into separate prompts or accept the length explicitly.

## Anti-Patterns
- Multiple tasks in one template. One template, one job.
- Vague constraints like "be careful" or "keep it simple." State what specifically to avoid.
