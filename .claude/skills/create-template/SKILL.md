<!-- Last updated: 2026-03-23 -->
---
name: create-template
description: Creates a new prompt template from a repeated pattern. Interviews you about the use case, extracts the structure, and writes the template file.
argument-hint: "[description of what the template is for]"
allowed-tools: Read,Grep,Glob,Write,Edit,AskUserQuestion
---

# Skill: create-template

## When to Use
- You've written the same kind of prompt three or more times
- You want to formalise a recurring workflow into a reusable template
- You identified a gap in the existing templates

## Method

### Phase 1: Understand the pattern

If $ARGUMENTS is provided, use it as a starting point. Otherwise ask:

> What task does this template cover? Describe a situation where you'd use it.

Then ask:

> Can you paste an example prompt you've written for this task before, or describe the steps you always include?

### Phase 2: Check for overlap

Read all existing templates in `templates/` and `rules/template-conventions.md`. Check whether the user's task is already covered by an existing template — or could be covered by extending one.

If there's overlap, tell the user: "This overlaps with [template] — would you rather extend that template or create a new one?" Only proceed with a new template if they confirm.

### Phase 3: Extract the structure

From the user's description and example, extract the four-part structure:

1. **Task line**: imperative verb + what + where (e.g. "Migrate [what] from [source] to [target]")
2. **Context/Focus sections**: what the agent needs to know before starting. Draw section names from the Named Sections catalogue in `rules/template-conventions.md` where possible — invent new names only when nothing fits.
3. **Constraints section**: scope limits, read-only flags, things to avoid. Each constraint must be specific and verifiable (not "be careful" or "keep it simple"). Include the uncertainty handling line for the template type.
4. **Output/Verification section**: what the deliverable looks like, or how to verify the work.

Ask the user to confirm or adjust each section before writing.

### Phase 4: Validate and write

Before writing, run this checklist:

1. **Imperative opening** — starts with a verb (Implement, Fix, Investigate, Research, Review, Migrate, etc.)
2. **All details are bracketed placeholders** — no project-specific content baked in
3. **Constraints section exists** with at least one specific, verifiable constraint
4. **Constraints include motivation** — each scope limit or prohibition includes a brief reason why (e.g. "Only modify files in src/auth/ — the rest has a pending refactor")
5. **Uncertainty handling line exists** — pick the phrase that fits: "stop and ask rather than guessing" (action templates), "state your assumption and flag it" (investigation templates), "flag it as a question rather than a finding" (review templates), "say so explicitly" (research templates), or write a new one if none fits
6. **Self-check or Verification section exists** — action templates need Verification, report templates need a self-check line before the closing summary
7. **Body is under 30 lines** (excluding comment block). If over, suggest splitting.
8. **Comment block at top** explains: Template name, When to use, Sections list

Write the template to `templates/[descriptive-name].md` with a `<!-- Last updated: YYYY-MM-DD -->` comment.

After writing, tell the user:
- To update `rules/template-conventions.md` Named Sections if the template introduced new section names
- To update the `/prompt` skill's Phase 1 classifier and Phase 2 questions if they want the skill to support the new template

## Rules
- Read `rules/template-conventions.md` before generating any template. Follow it exactly.
- Use section names from the Named Sections catalogue when possible. Only invent new section names when nothing in the catalogue fits.
- Use imperative verbs to open: Investigate, Implement, Review, Research, Fix, Migrate, Compare, Audit.
- Every template must have a Constraints section. No exceptions.
- Keep the `Examples (optional)` section as a placeholder reminder — do not fill it with content.
- Do not duplicate an existing template. Check first.
