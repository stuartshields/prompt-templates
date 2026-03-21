# Prompt Templates

These are the prompt templates I use when working with AI coding agents. They give the agent a clear structure — what to do, how to do it, what not to touch, and what done looks like — so it stops guessing and starts delivering.

They work with Claude Code, Gemini, Codex, or anything else that takes a text prompt.

## Why These Exist

Most prompts are too vague. You say "review my auth code" and get back a vague summary, or worse, unwanted code changes. You say "add a login page" and get a half-built feature with no definition of done.

I kept writing the same structure into my prompts: scope it, constrain it, define the output shape. After doing that enough times, I pulled out the repeating parts into templates.

## The Templates

There are four, each for a different kind of task:

| When you need | Template | What you get |
|---|---|---|
| Findings, not changes | [Investigation / Audit](templates/investigation-audit.md) | A read-only report with per-finding detail and a prioritised summary |
| Working code with clear criteria | [Build / Implement](templates/build-implement.md) | Code that meets explicit acceptance criteria, with a plan-first checkpoint |
| A second opinion on existing work | [Review](templates/review.md) | Severity-rated findings and a ship/fix/rethink verdict |
| Options before a decision | [Research / Compare](templates/research-compare.md) | Trade-offs per option and a recommendation |

## How to Use Them

1. Pick the template that matches what you're trying to do
2. Copy it into your AI session
3. Replace the `[bracketed placeholders]` with your specifics
4. Send it

That's it. The structure does the work.

## Example

Here's the Investigation / Audit template filled in for a real task:

```
Investigate authentication flow in src/auth/.

Focus
- Token refresh logic
- Session expiry handling
- Error states when auth server is unreachable

Method
1. Trace the login flow from entry point to token storage
2. Check token refresh triggers and failure handling
3. Review session timeout behaviour

Constraints
- Read only. Do not modify any files.
- Stay within src/auth/ and its direct dependencies
- If anything is ambiguous, state your assumption and flag it.

Output
For each finding, document:
- Where: file path and line
- What: the issue
- Why it matters: impact
- Suggested fix: one sentence

Finish with the top 3 highest-impact findings.
```

## How They're Structured

Every template follows the same backbone:

```
[Task verb] [what] in [where].

Context / Focus / Scope        → what the agent needs to know
Requirements / Method          → the specific steps or criteria
Constraints                    → what not to do, scope limits
Verification / Output          → what "done" looks like
```

The section names change between templates, but the four parts stay the same. The key bits:

- **Direct tone.** "Investigate X" not "Could you please investigate X."
- **Constraints are explicit.** If you want analysis without changes, say "Read only." If you want it scoped to one directory, say so. Without this, agents wander.
- **Output has shape.** "For each finding: X, Y, Z" beats "give me results." Define what the deliverable looks like.
- **Uncertainty is handled.** Every template tells the agent what to do when it's unsure — ask, flag, or state its assumption. This stops it from guessing and sounding confident about wrong answers.

## Template Details

### Investigation / Audit

For when you want findings, not changes. Security audits, performance checks, code analysis.

Sections: Focus (what to look at), Method (ordered steps), Constraints (read-only + scope limits), Output (per-finding format and a top-3 summary).

### Build / Implement

For when you want working code. New features, bug fixes, refactors.

Sections: Context (what exists and why this is needed), Requirements (what to build), Done When (testable success criteria), Constraints (scope and patterns to follow), Verification (how to confirm it works), Plan Check (forces the agent to plan before coding and cross-check against your requirements).

### Review

For when you want a second opinion. Code review, spec review, checking work against a standard.

Sections: Scope (what to review), Review For (angles to assess), Constraints (read-only + severity levels), Output (findings list and a ship/fix/rethink verdict).

### Research / Compare

For when you need to compare options before committing to one. Library choices, architecture approaches, migration strategies.

Sections: Question (the decision you're making), Consider (options to evaluate), Constraints (read-only + verify claims against docs), Output (per-option trade-offs and a recommendation).

## Making New Templates

If you've written the same prompt structure three times, it's worth extracting. Pull out the repeating parts, replace the specifics with `[bracketed placeholders]`, add a comment block at the top explaining when to use it. Keep it under 30 lines — if it needs more, split it into two templates.

## Licence

MIT
