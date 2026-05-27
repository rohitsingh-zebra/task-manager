<script setup>
import { reactive, ref, watch } from 'vue'

const props = defineProps({
  task: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['deleteTask', 'editTask', 'toggleTask'])

const isEditing = ref(false)
const editableTask = reactive({
  name: props.task.name,
  dueDate: props.task.dueDate,
})

watch(
  () => props.task,
  (task) => {
    editableTask.name = task.name
    editableTask.dueDate = task.dueDate
  },
  { deep: true },
)

function startEditing() {
  isEditing.value = true
}

function cancelEditing() {
  editableTask.name = props.task.name
  editableTask.dueDate = props.task.dueDate
  isEditing.value = false
}

function saveTask() {
  const taskName = editableTask.name.trim()

  if (!taskName || !editableTask.dueDate) {
    return
  }

  emit('editTask', {
    id: props.task.id,
    name: taskName,
    dueDate: editableTask.dueDate,
  })

  isEditing.value = false
}
</script>

<template>
  <li class="task-item" :class="{ 'is-completed': task.isCompleted }">
    <template v-if="isEditing">
      <form class="edit-form" @submit.prevent="saveTask">
        <input v-model="editableTask.name" type="text" aria-label="Edit task name" required />
        <input v-model="editableTask.dueDate" type="date" aria-label="Edit due date" required />

        <div class="task-actions">
          <button type="submit" class="primary-action">Save</button>
          <button type="button" class="secondary-action" @click="cancelEditing">Cancel</button>
        </div>
      </form>
    </template>

    <template v-else>
      <button
        type="button"
        class="completion-toggle"
        :aria-pressed="task.isCompleted"
        @click="emit('toggleTask', task.id)"
      >
        <span class="checkmark" aria-hidden="true">✓</span>
      </button>

      <div class="task-content">
        <p class="task-name">{{ task.name }}</p>
        <time class="due-date" :datetime="task.dueDate">Due {{ task.dueDate }}</time>
      </div>

      <div class="task-actions">
        <button type="button" class="secondary-action" @click="startEditing">Edit</button>
        <button type="button" class="danger-action" @click="emit('deleteTask', task.id)">Delete</button>
      </div>
    </template>
  </li>
</template>

<style scoped>
.task-item {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr) auto;
  gap: 1rem;
  align-items: center;
  padding: 1rem;
  border: 1px solid #e2e8f0;
  border-radius: 16px;
  background: #ffffff;
  transition: border 160ms ease, opacity 160ms ease;
}

.task-item.is-completed {
  border-color: #bbf7d0;
  background: #f0fdf4;
}

.completion-toggle {
  display: inline-grid;
  width: 2.35rem;
  height: 2.35rem;
  place-items: center;
  border: 2px solid #cbd5e1;
  border-radius: 999px;
  color: transparent;
  background: #ffffff;
  cursor: pointer;
}

.is-completed .completion-toggle {
  border-color: #16a34a;
  color: #ffffff;
  background: #16a34a;
}

.checkmark {
  font-size: 1rem;
  font-weight: 900;
  line-height: 1;
}

.task-content {
  min-width: 0;
}

.task-name {
  margin: 0;
  color: #1f2937;
  font-size: 1.05rem;
  font-weight: 800;
  word-break: break-word;
}

.is-completed .task-name {
  color: #64748b;
  text-decoration: line-through;
  text-decoration-thickness: 2px;
}

.due-date {
  display: inline-block;
  margin-top: 0.25rem;
  color: #64748b;
  font-size: 0.9rem;
}

.task-actions {
  display: flex;
  gap: 0.5rem;
  justify-content: flex-end;
  flex-wrap: wrap;
}

.edit-form {
  display: grid;
  grid-column: 1 / -1;
  grid-template-columns: minmax(0, 1fr) 170px auto;
  gap: 0.75rem;
  align-items: center;
}

input {
  width: 100%;
  border: 1px solid #cbd5e1;
  border-radius: 12px;
  padding: 0.75rem 0.85rem;
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
  border-radius: 10px;
  padding: 0.65rem 0.85rem;
  font: inherit;
  font-weight: 800;
  cursor: pointer;
  transition: transform 160ms ease, background 160ms ease;
}

button:hover {
  transform: translateY(-1px);
}

.primary-action {
  color: #ffffff;
  background: #2563eb;
}

.secondary-action {
  color: #1f2937;
  background: #e2e8f0;
}

.danger-action {
  color: #ffffff;
  background: #dc2626;
}

@media (max-width: 760px) {
  .task-item,
  .edit-form {
    grid-template-columns: 1fr;
  }

  .task-actions {
    justify-content: stretch;
  }

  .task-actions button {
    flex: 1;
  }
}
</style>
