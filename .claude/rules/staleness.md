<!-- Last updated: 2026-03-21 -->

# Staleness Check

Every file in this project that contains guidance based on current AI best practices has a `<!-- Last updated: YYYY-MM-DD -->` comment.

## On Session Start

- Compare the last-updated date against the current date.
- If any file is **more than 30 days old**, flag it to the user before making changes: "This file hasn't been reviewed since [date] — AI prompting best practices may have changed. Want me to check for updates before proceeding?"

## On File Edit

- When you edit any file that has a last-updated comment, **update the date to today**.

## Applies To

`CLAUDE.md`, all files in `templates/`, `rules/template-conventions.md`, and `skills/prompt/SKILL.md`.
