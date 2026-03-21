<!-- Last updated: 2026-03-21 -->
---
name: prompt
description: Interactive wizard that interviews you, picks the right template, fills in the placeholders, and outputs a ready-to-use prompt.
argument-hint: "[optional: brief description of what you need]"
disable-model-invocation: true
allowed-tools: Read,Grep,Glob,AskUserQuestion
---

# Skill: prompt

## When to Use
- You have a task but aren't sure which template fits
- You want a filled-in prompt without manually editing a template
- You want to quickly generate a structured prompt for another AI session

## Method

### Phase 1: Classify the task

If $ARGUMENTS is provided, use it as a starting point. Otherwise ask:

> What do you need to get done? Describe it in a sentence or two.

Do NOT present a numbered menu of templates. Instead, classify the task yourself based on the user's description using these rules:

- **Wants code written** (new feature, bug fix, refactor, migration) → Build / Implement
- **Wants findings without changes** (audit, security check, performance review, "what's wrong with") → Investigate / Audit
- **Needs to choose between options** (library choice, architecture decision, "should I use X or Y") → Research / Compare
- **Wants a second opinion on existing work** (code review, spec review, "check my work") → Review

State which template you've selected and why in one line, e.g.: "This sounds like a build task — I'll use the Build / Implement template." Then move to Phase 2.

If the description doesn't clearly fit any template:
1. Ask one clarifying question: "Are you looking to **make changes**, **get findings**, **compare options**, or **review existing work**?"
2. If it still doesn't fit, tell the user their task might need a custom template. Build a one-off prompt using the four-part structure (Task, Context, Constraints, Output) and suggest they run `/create-template` afterward if the pattern recurs.

### Phase 1.5: Identify the target tool

Ask:

> Where will you use this prompt?
> 1. **Claude Code** (CLI, Cursor, Windsurf)
> 2. **Claude** (claude.ai, API)
> 3. **ChatGPT**
> 4. **Gemini**
> 5. **Other** — tell me which

Adapt the output in Phase 3 based on the answer:
- **Claude (API, claude.ai)**: Wrap sections in XML tags (`<context>`, `<requirements>`, `<constraints>`, etc.). Add a one-line role at the top (e.g. "You are a senior backend engineer.").
- **Claude Code / Cursor / Windsurf**: No role line (the tool sets this). No XML tags (Markdown headers are fine). Keep it concise — the agent already has project context.
- **ChatGPT**: Add a one-line role at the top. Use Markdown headers. Add explicit output format constraints (ChatGPT benefits from format specificity).
- **Gemini**: Add a one-line role at the top. Use clear input labelling. Add explicit verification steps (Gemini benefits from these).
- **Other**: Add a one-line role at the top. Use Markdown headers. Keep it tool-agnostic.

### Phase 2: Fill the template

For the selected template, ask questions to fill each bracketed placeholder. Ask one group of related questions at a time — do not dump all questions at once.

**Build / Implement** — ask in this order:
1. What are you building? Where does it go? (fills [what], [where])
2. What exists already that this connects to? Why is it needed? (fills [Context])
3. What specifically must it do? (fills [Requirements] — number each item)
4. How will you know it's done? What's the observable outcome? (fills [Done when])
5. What files should be touched? Any patterns to follow? Anything to avoid? (fills [Constraints])
6. How do you verify it works? What command to run, what output to expect? (fills [Verification])

**Investigate / Audit** — ask in this order:
1. What are you investigating? In what scope? (fills [what], [scope])
2. What specific areas should be examined? (fills [Focus])
3. What steps should the agent follow? (fills [Method])
4. Any scope limits beyond read-only? (fills [Constraints])

**Research / Compare** — ask in this order:
1. What topic? What's the context? (fills [topic], [context])
2. What's the specific decision you need to make? (fills [Question])
3. What options or angles to evaluate? (fills [Consider])
4. Any constraints beyond read-only? (fills [Constraints])

**Review** — ask in this order:
1. What are you reviewing? Against what standard? (fills [what], [standard])
2. What files, branch, or diff range? (fills [Scope])
3. What angles to assess? (fills [Review for])
4. Any constraints beyond read-only? (fills [Constraints])

### Phase 3: Output the prompt

Assemble the filled template and present it in a fenced code block so the user can copy it directly. The output must:

- Have no remaining `[brackets]` — every placeholder is filled
- Use imperative tone, no filler words
- Follow the conventions in `rules/template-conventions.md`
- Include an uncertainty handling line in Constraints (per template conventions)
- For **Build / Implement** prompts: append a **Plan Check** section instructing the agent to produce a plan first, cross-check every requirement and constraint in the prompt against the plan, flag gaps or deviations, and not proceed to implementation until the plan fully covers the prompt
- Be under 30 lines (excluding Plan Check section)

After presenting the prompt, ask: "Ready to use, or want to adjust anything?"

## Rules
- Do NOT modify any files. This skill only reads templates and produces output.
- Ask questions conversationally — don't dump a form.
- If the user's answers are vague, push back: "Can you be more specific about [X]?"
- Skip questions the user already answered via $ARGUMENTS or earlier in the conversation.
- If the task clearly doesn't fit any template and can't be adapted, say so and suggest `/create-template`.
