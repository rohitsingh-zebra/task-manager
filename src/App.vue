<script setup>
import { computed, reactive } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TaskItem from './components/TaskItem.vue'

const initialTasks = [
  {
    id: crypto.randomUUID(),
    name: 'Review project priorities',
    dueDate: new Date().toISOString().slice(0, 10),
    isCompleted: false,
  },
]

const tasks = reactive([...initialTasks])

const completedTaskCount = computed(() => tasks.filter((task) => task.isCompleted).length)
const pendingTaskCount = computed(() => tasks.length - completedTaskCount.value)
const sortedTasks = computed(() => [...tasks].sort((firstTask, secondTask) => firstTask.dueDate.localeCompare(secondTask.dueDate)))

function createTask(taskDetails) {
  tasks.push({
    id: crypto.randomUUID(),
    name: taskDetails.name,
    dueDate: taskDetails.dueDate,
    isCompleted: false,
  })
}

function editTask(updatedTask) {
  const task = tasks.find((currentTask) => currentTask.id === updatedTask.id)

  if (!task) {
    return
  }

  task.name = updatedTask.name
  task.dueDate = updatedTask.dueDate
}

function deleteTask(taskId) {
  const taskIndex = tasks.findIndex((task) => task.id === taskId)

  if (taskIndex !== -1) {
    tasks.splice(taskIndex, 1)
  }
}

function toggleTask(taskId) {
  const task = tasks.find((currentTask) => currentTask.id === taskId)

  if (task) {
    task.isCompleted = !task.isCompleted
  }
}
</script>

<template>
  <main class="app-shell">
    <section class="hero-card" aria-labelledby="app-title">
      <p class="eyebrow">Vue Task Manager</p>
      <h1 id="app-title">Plan work, track dates, and finish with clarity.</h1>
      <p class="hero-copy">
        Add tasks with due dates, edit them as plans change, and mark completed work with a clear
        checkmark and cross-lined styling.
      </p>

      <div class="task-summary" aria-label="Task summary">
        <span>{{ tasks.length }} total</span>
        <span>{{ pendingTaskCount }} pending</span>
        <span>{{ completedTaskCount }} complete</span>
      </div>
    </section>

    <task-form @create-task="createTask" />

    <section class="task-list-card" aria-labelledby="tasks-title">
      <div class="list-heading">
        <h2 id="tasks-title">Tasks</h2>
        <p>Sorted by due date</p>
      </div>

      <ul v-if="tasks.length" class="task-list">
        <task-item
          v-for="task in sortedTasks"
          :key="task.id"
          :task="task"
          @delete-task="deleteTask"
          @edit-task="editTask"
          @toggle-task="toggleTask"
        />
      </ul>

      <p v-else class="empty-state">No tasks yet. Add your first task above.</p>
    </section>
  </main>
</template>

<style scoped>
.app-shell {
  width: min(980px, calc(100% - 2rem));
  margin: 0 auto;
  padding: 4rem 0;
}

.hero-card,
.task-list-card {
  border: 1px solid rgba(148, 163, 184, 0.28);
  border-radius: 28px;
  background: rgba(255, 255, 255, 0.82);
  box-shadow: 0 24px 70px rgba(15, 23, 42, 0.1);
  backdrop-filter: blur(18px);
}

.hero-card {
  margin-bottom: 1.25rem;
  padding: clamp(1.5rem, 4vw, 3rem);
}

.eyebrow {
  margin: 0 0 0.75rem;
  color: #2563eb;
  font-size: 0.8rem;
  font-weight: 900;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

h1 {
  max-width: 760px;
  margin: 0;
  color: #111827;
  font-size: clamp(2.4rem, 7vw, 5rem);
  line-height: 0.95;
  letter-spacing: -0.06em;
}

.hero-copy {
  max-width: 650px;
  margin: 1.25rem 0 0;
  color: #526174;
  font-size: 1.1rem;
  line-height: 1.7;
}

.task-summary {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: 1.5rem;
}

.task-summary span {
  border-radius: 999px;
  padding: 0.55rem 0.85rem;
  color: #1f2937;
  font-weight: 800;
  background: #e0ecff;
}

.task-list-card {
  margin-top: 1.25rem;
  padding: 1.25rem;
}

.list-heading {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  align-items: baseline;
  margin-bottom: 1rem;
}

h2,
.list-heading p {
  margin: 0;
}

h2 {
  color: #111827;
  font-size: 1.5rem;
}

.list-heading p {
  color: #64748b;
  font-weight: 700;
}

.task-list {
  display: grid;
  gap: 0.8rem;
  padding: 0;
  margin: 0;
  list-style: none;
}

.empty-state {
  margin: 0;
  padding: 2rem;
  border: 1px dashed #cbd5e1;
  border-radius: 18px;
  color: #64748b;
  text-align: center;
  background: #f8fafc;
}

@media (max-width: 640px) {
  .app-shell {
    width: min(100% - 1rem, 980px);
    padding: 1rem 0;
  }

  .list-heading {
    display: grid;
  }
}
</style>
