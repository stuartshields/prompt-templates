<!-- Last updated: 2026-03-21 -->

# Template Conventions

## Structure
- Every template follows four parts: Task, Context, Constraints, Output.
- Section names can vary (Focus, Method, Requirements, Review For) but the four-part intent stays the same.
- Bracketed text `[like this]` is a placeholder. Never leave brackets in a finished prompt.

## Tone
- Direct, second person. "Investigate X" not "Could you please investigate X."
- Imperative verbs to open: Investigate, Implement, Review, Research, Audit, Compare.
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
- Build: "stop and ask rather than guessing." Investigation/Review: "state your assumption and flag it." Research: "say so explicitly."
- This prevents the agent from silently guessing and producing confident-sounding wrong output.

## Examples (Optional)
- Add 1-3 examples when the output format is ambiguous or unfamiliar.
- Wrap examples in the prompt, not in the template itself — templates stay generic.
- Anthropic recommends 3-5 examples for best results when format matters.

## Anti-Patterns
- Templates longer than 30 lines. Split or you're over-specifying.
- Multiple tasks in one template. One template, one job.
- Vague constraints like "be careful" or "keep it simple." State what specifically to avoid.
