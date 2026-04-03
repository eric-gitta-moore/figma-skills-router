---
name: figma-skills-router
description: Unified entry for Figma workflows. Route requests to the right guide for implementing designs in code, editing Figma files, building screens, creating design systems, managing Code Connect, generating rules, or creating new files.
disable-model-invocation: false
---

# Figma Skills Router

Use this skill as the single entry point for Figma-related work. Start by identifying the user's intended deliverable, then load the most appropriate guide from `references/`.

## Core Routing Rule

Pick the guide that is closest to the final output the user wants. Prefer the most specific workflow over the more general one.

## Route By Deliverable

### Implement a Figma design in the codebase

Use this when the result should be application code in the repository, such as:

- implementing a component from Figma
- translating a frame into React, Vue, or other production code
- matching an existing design in the user's app

Load:

- [figma-implement-design](./references/figma-implement-design/GUIDE.md)

### Edit or inspect a Figma file directly

Use this when the task is to create, edit, delete, or inspect nodes inside Figma, or when `use_figma` is needed.

Load:

- [figma-use](./references/figma-use/GUIDE.md)

### Build or update a full screen in Figma

Use this when the result should be a full page, screen, or multi-section layout in Figma, created from code or from a description.

Load both:

- [figma-generate-design](./references/figma-generate-design/GUIDE.md)
- [figma-use](./references/figma-use/GUIDE.md)

### Build or update a Figma design system

Use this when the user wants variables, tokens, modes, component libraries, foundations, or a full design system structure in Figma.

Load both:

- [figma-generate-library](./references/figma-generate-library/GUIDE.md)
- [figma-use](./references/figma-use/GUIDE.md)

### Create or maintain Code Connect mappings

Use this when the task is specifically about Code Connect templates or Figma-to-code component mappings.

Load:

- [figma-code-connect](./references/figma-code-connect/GUIDE.md)

### Generate project-specific Figma rules

Use this when the user wants reusable rules for Figma-to-code work in files such as `AGENTS.md`, `CLAUDE.md`, or Cursor rules.

Load:

- [figma-create-design-system-rules](./references/figma-create-design-system-rules/GUIDE.md)

### Create a new Figma or FigJam file

Use this when the user only needs a blank file created before any additional work begins.

Load:

- [figma-create-new-file](./references/figma-create-new-file/GUIDE.md)

## Priority Rules

When multiple routes appear to match, use this priority:

1. If the final artifact is repository code, choose `figma-implement-design`.
2. If the final artifact is a Figma canvas update, choose `figma-use` or one of its paired workflows.
3. If the task is a full screen in Figma, choose `figma-generate-design` plus `figma-use`.
4. If the task is a design system in Figma, choose `figma-generate-library` plus `figma-use`.
5. If the request is only about Code Connect, choose `figma-code-connect`.

## Loading Discipline

- Load only the guide or guides needed for the current request.
- Do not load every Figma guide by default.
- When a paired workflow requires `figma-use`, always load it together with the higher-level guide.
- Follow the selected guide's required workflow in order instead of mixing steps from multiple guides arbitrarily.
