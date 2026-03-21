---
name: create-template
description: Creates a new prompt template from a repeated pattern. Interviews you about the use case, extracts the structure, and writes the template file.
argument-hint: "[description of what the template is for]"
disable-model-invocation: true
allowed-tools: Read,Grep,Glob,Write,Edit
---

# Skill: create-template

## When to Use
- You've written the same kind of prompt three or more times
- You want to formalise a workflow into a reusable template
- Use $ARGUMENTS to describe what the template should cover

## Method

1. Ask what task the template is for and what tools/agents it targets.
2. Ask for an example prompt the user has written for this task before, or describe the steps they always follow.
3. Extract the repeating structure into four sections: Task, Context, Constraints, Output.
4. Replace project-specific details with `[bracketed placeholders]`.
5. Add a comment block at the top explaining when to use the template and what each section does.
6. Write the template to `templates/` with a descriptive filename.

## Rules
- Keep templates under 30 lines. If it's longer, suggest splitting into two templates.
- Use imperative verbs to open: Investigate, Implement, Review, Research.
- Every template must have a Constraints section. No exceptions.
- Every template must have an Output section defining the deliverable shape.
- Do not add examples or explanations inside the template itself. The comment block at the top handles that.
