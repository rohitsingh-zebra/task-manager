# Task Manager

A Vite-powered Vue 3 task manager app built with Cursor using project-specific skills and rules.

## Project Overview

This app helps manage simple tasks with:

- Task creation with a required task name and due date.
- Task editing for both name and due date.
- Task deletion.
- Completion toggling.
- Completed task styling with a checkmark and line-through text.
- Due-date sorting so upcoming work stays easy to scan.

## Tech Stack

- Vue 3
- Vite
- JavaScript
- Scoped CSS

## Cursor Skills Used

This project includes custom Cursor skills in `.cursor/skills` that guided the work:

- `github-sync`: Used to commit and push project changes to the connected GitHub repository.
- `vercel-deploy`: Used to prepare the Vue app for Vercel deployment by installing dependencies, running the build, installing the Vercel CLI, logging in, and deploying.
- `vue3-component-builder`: Used to create Vue 3 components with the Composition API, `<script setup>`, scoped CSS, task data rules, emits, and Vue reactive state patterns.

Cursor used these skills as project instructions while building the app, syncing it to GitHub, and deploying it to Vercel.

## Cursor Rules

The project also includes `.cursorrules` to keep the code style consistent:

- JavaScript variables, functions, refs, and reactive properties use `camelCase`.
- Vue component filenames use `PascalCase`, such as `TaskItem.vue`.
- Vue template component tags use `kebab-case`, such as `<task-item />`.
- Global constants use `UPPER_SNAKE_CASE`.

The current Vue files follow these rules across component names, state names, event handlers, and template usage.

## Project Structure

```text
src/
  App.vue
  main.js
  style.css
  components/
    TaskForm.vue
    TaskItem.vue
```

## Local Development

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

Build for production:

```bash
npm run build
```

Preview the production build:

```bash
npm run preview
```

## Deployment

The app has been deployed to Vercel as a Vite project. Vercel uses:

- Build command: `npm run build`
- Output directory: `dist`

The project is also connected to GitHub so future updates can be pushed to the repository and deployed through Vercel.
