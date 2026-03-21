<!-- Last updated: 2026-03-21 -->

# Prompt Templates

## What This Is

A collection of reusable prompt templates for structuring how you communicate with AI agents. Each template removes guesswork by defining the deliverable format, scope constraints, and verification steps up front.

## Origins

These templates were derived on 2026-03-21 from two sources:

1. **A blog post on AI-augmented workflows** that demonstrated structured prompting patterns. The key insight was separating prompts into explicit sections: Role, Method, Constraints, and Output. Their UX review prompt and executing-plans prompt showed how numbered steps, phase separation, and explicit output formats produce consistently better results than unstructured requests.

2. **The global `~/.claude/` configuration (v2026.2)** which already encodes many of these patterns as rules, hooks, and agent definitions. The templates formalise what the config enforces structurally - scope control, read-only enforcement, verification before completion - into a format you can use in ad-hoc prompts.

## When to Use

When starting a Claude session in any project and you need to:
- Investigate or audit something without changes being made
- Build a feature with clear acceptance criteria
- Get a second opinion on work already done
- Research options before making a decision

Open the relevant template, fill in the bracketed sections, and use it as your prompt. The structure is the point - it stops the agent from guessing what you want.

## Project Conventions

- Templates live in `templates/` as plain Markdown files
- Each template has a comment block at the top explaining when to use it and what each section does
- Bracketed text `[like this]` marks where you fill in project-specific details
- Templates are tool-agnostic - they work across Claude Code, Gemini, Codex, or anything else
- Keep templates short. If a template needs more than 30 lines, it's doing too much - split it

## Structure of a Template

Every template follows the same backbone:

```
[Task verb] [what] in [where].

Context / Focus / Scope
- What the agent needs to know before starting

Requirements / Method / Review For
- The specific steps or criteria (numbered)

Constraints
- What not to do, scope limits, read-only flags

Verification / Output
- What the deliverable looks like, how to confirm it worked
```

The section names vary by template type, but the four-part structure stays the same: **what you want, how to do it, what to avoid, what done looks like.**

## Using Templates

Use the `/prompt` skill to interactively build a ready-to-use prompt. It interviews you, picks the right template, fills in the placeholders, and outputs a prompt you can paste directly into any AI session.

## Creating New Templates

Use the `/create-template` skill, or follow this process:

1. Identify a prompt you've written more than twice
2. Extract the repeating structure - what sections did you always include?
3. Replace project-specific details with `[bracketed placeholders]`
4. Add a comment block explaining when to use it
5. Test it on a real task before committing

The threshold for a new template is the same as for any abstraction: if you've written the same instructions three times, it's worth extracting.

## Commands

- **Build/test/lint**: N/A (documentation project, no build step)
