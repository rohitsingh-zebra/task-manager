<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['createTask'])

const taskForm = reactive({
  name: '',
  dueDate: '',
})

function submitTask() {
  const taskName = taskForm.name.trim()

  if (!taskName || !taskForm.dueDate) {
    return
  }

  emit('createTask', {
    name: taskName,
    dueDate: taskForm.dueDate,
  })

  taskForm.name = ''
  taskForm.dueDate = ''
}
</script>

<template>
  <form class="task-form" @submit.prevent="submitTask">
    <label class="form-field">
      <span>Task name</span>
      <input
        v-model="taskForm.name"
        type="text"
        placeholder="Plan the sprint"
        aria-label="Task name"
        required
      />
    </label>

    <label class="form-field">
      <span>Due date</span>
      <input v-model="taskForm.dueDate" type="date" aria-label="Due date" required />
    </label>

    <button type="submit">Add task</button>
  </form>
</template>

<style scoped>
.task-form {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 180px auto;
  gap: 1rem;
  align-items: end;
  padding: 1rem;
  border: 1px solid #d8dee9;
  border-radius: 18px;
  background: #ffffff;
  box-shadow: 0 16px 40px rgba(33, 43, 54, 0.08);
}

.form-field {
  display: grid;
  gap: 0.45rem;
  color: #44546a;
  font-size: 0.9rem;
  font-weight: 700;
}

input {
  width: 100%;
  border: 1px solid #cbd5e1;
  border-radius: 12px;
  padding: 0.85rem 0.95rem;
  color: #1f2937;
  font: inherit;
  background: #f8fafc;
}

input:focus {
  outline: 3px solid rgba(37, 99, 235, 0.18);
  border-color: #2563eb;
  background: #ffffff;
}

button {
  border: 0;
  border-radius: 12px;
  padding: 0.9rem 1.2rem;
  color: #ffffff;
  font: inherit;
  font-weight: 800;
  background: #2563eb;
  cursor: pointer;
  transition: transform 160ms ease, background 160ms ease;
}

button:hover {
  background: #1d4ed8;
  transform: translateY(-1px);
}

@media (max-width: 760px) {
  .task-form {
    grid-template-columns: 1fr;
  }
}
</style>
