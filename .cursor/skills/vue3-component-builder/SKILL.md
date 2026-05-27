---
name: Vue 3 Component Builder
description: Use this skill when asked to create or modify Vue.js components, especially for the task management features.
---

# Instructions

When creating Vue components for this task management app, follow these strict rules:
1.  **Syntax:** Always use Vue 3 Composition API with `<script setup>`.
2.  **Styling:** Use scoped CSS `<style scoped>`. 
3.  **Task Logic:** 
    *   Tasks must have an `id`, `name`, `dueDate`, and `isCompleted` boolean.
    *   If `isCompleted` is true, apply a CSS class that adds a line-through (strikethrough) to the text and displays a checkmark icon.
4.  **Emits:** Use `defineEmits` for actions like edit, delete, and toggle completion if splitting into smaller components.
5.  **State:** Use Vue `ref` for primitive values and `reactive` for complex objects/arrays.
