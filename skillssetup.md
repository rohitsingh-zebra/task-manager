# Skills Setup

This guide explains how another developer can clone this repository, open it in Cursor, see the project skills, and add new skills.

## Clone And Open In Cursor

Clone the repository:

```bash
git clone https://github.com/rohitsingh-zebra/task-manager.git
cd task-manager
```

Open the folder in a new Cursor window:

```bash
cursor .
```

If the `cursor` command is not available, open Cursor manually and choose `File > Open Folder`, then select the cloned `task-manager` folder.

## Install And Run The App

Install dependencies:

```bash
npm install
```

Start the Vite development server:

```bash
npm run dev
```

Build the production version:

```bash
npm run build
```

## Where Project Skills Live

Project skills are stored in:

```text
.cursor/skills/
```

This repository currently includes:

```text
.cursor/skills/
  github-sync/
    SKILL.md
  vercel-deploy/
    SKILL.md
  vue3-component-builder/
    SKILL.md
```

Because these skills are inside the repository, anyone who clones the project and opens it in Cursor can use the same project-specific instructions.

## Current Skills

`github-sync` helps Cursor commit and push project changes to GitHub.

`vercel-deploy` helps Cursor install dependencies, run the production build, install or use the Vercel CLI, and deploy the app.

`vue3-component-builder` guides Cursor when creating Vue 3 task manager components. It requires `<script setup>`, scoped CSS, task objects with `id`, `name`, `dueDate`, and `isCompleted`, and completed-task styling with a checkmark and line-through text.

## Project Rules

The project also has `.cursorrules`, which gives Cursor coding standards for this repository:

- Use `camelCase` for JavaScript variables, functions, refs, and reactive properties.
- Use `PascalCase` for Vue component filenames.
- Use `kebab-case` for Vue template component tags.
- Use `UPPER_SNAKE_CASE` for global constants.

These rules work together with the skills so Cursor can generate code that follows this project style.

## How Cursor Used The Skills

Cursor used the `vue3-component-builder` skill to create the Vue 3 Task Manager app with Composition API components, scoped CSS, task creation, due dates, editing, deletion, and completion styling.

Cursor used the `github-sync` skill to stage, commit, and push the app to the connected GitHub repository.

Cursor used the `vercel-deploy` skill to check dependencies, run `npm run build`, install and use the Vercel CLI, log in, and deploy the app to Vercel.

## Add A New Project Skill

Create a new folder under `.cursor/skills`:

```bash
mkdir -p .cursor/skills/my-new-skill
```

Add a required `SKILL.md` file:

```text
.cursor/skills/my-new-skill/SKILL.md
```

Use this structure:

```markdown
---
name: my-new-skill
description: Describes what this skill does and when Cursor should use it.
---

# My New Skill

## Instructions

1. Explain the workflow Cursor should follow.
2. Include project-specific commands, naming rules, or checks.
3. Keep the instructions clear and focused.
```

Skill names should be lowercase and use hyphens. Descriptions should be specific so Cursor can understand when the skill applies.

## Project Skill Vs Personal Skill

Use a project skill when the instructions should travel with this repository:

```text
.cursor/skills/my-new-skill/SKILL.md
```

Use a personal skill when the instructions are only for your own Cursor setup across multiple projects:

```text
~/.cursor/skills/my-new-skill/SKILL.md
```

Do not add custom skills to Cursor's internal built-in skills folder.

## Recommended Skill Checklist

Before committing a new skill:

- Confirm the skill has a `SKILL.md` file.
- Confirm the frontmatter includes `name` and `description`.
- Keep the skill focused on one workflow.
- Add concrete commands or examples when useful.
- Commit the skill folder so other developers get it when they clone the repo.
