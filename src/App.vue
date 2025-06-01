<template>
  <div class="container">
    <h1 class="title">{{ title }}</h1>
    <main>
      <TodoForm @add-task="addTask" />
      <section v-if="tasks.length" class="todo-table">
        <div class="todo-table-header">
          <span>#</span>
          <span>Task</span>
          <span>Status</span>
        </div>
        <div v-for="(task, idx) in tasks" :key="task.id" class="todo-table-row">
          <span class="todo-task-index">{{ idx + 1 }}</span>
          <span class="todo-task-title">{{ task.title }}</span>
          <span>
            <input
              type="checkbox"
              v-model="task.done"
              :id="'done-' + task.id"
            />
            <label :for="'done-' + task.id" class="done-label">
              <span v-if="task.done" class="done-status">Done</span>
              <span v-else class="pending-status">Pending</span>
            </label>
          </span>
        </div>
      </section>
      <p v-else class="no-tasks">No tasks yet. Add your first task!</p>
    </main>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import TodoForm from "./components/TodoForm.vue";
import { Task } from "./types";
const title = ref("Todo App with Vuejs 3 and TypeScript");

const tasks = ref<Task[]>([]);

const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
};
</script>

<style scoped>
.title {
  font-size: clamp(0.9rem, 3.7vw, 1.7rem);
  color: #f5f5f5;
  text-align: center;
  margin: 10px auto 50px;
  text-shadow: var(--text-shadow);
  font-weight: 600;
  letter-spacing: 0.17em;
  text-transform: uppercase;
}

.todo-table {
  width: 100%;
  max-width: 900px;
  margin: 2.5rem auto 0 auto;
  border-radius: 1rem;
  overflow: hidden;
  background: rgba(39, 40, 50, 0.92);
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.1);
}

.todo-table-header,
.todo-table-row {
  display: grid;
  grid-template-columns: 40px 1fr 120px;
  align-items: center;
  padding: 1rem 1.2rem;
}

.todo-table-header {
  background: var(--hover-color);
  font-weight: 700;
  color: var(--accent-color);
  text-transform: uppercase;
  font-size: 1rem;
  letter-spacing: 0.08em;
}

.todo-table-row {
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  font-size: 1.05rem;
  color: var(--text-color);
  background: transparent;
  transition: background 0.2s;
}

.todo-table-row:last-child {
  border-bottom: none;
}

.todo-task-index {
  text-align: center;
  color: #aaa;
  font-size: 1.1em;
}

.todo-task-title {
  word-break: break-word;
  padding-right: 1rem;
}

.done-label {
  margin-left: 0.5em;
  font-size: 0.98em;
  cursor: pointer;
  user-select: none;
}

.done-status {
  color: #4ade80;
  font-weight: 700;
  margin-left: 0.2em;
}

.pending-status {
  color: #fbbf24;
  font-weight: 700;
  margin-left: 0.2em;
}

input[type="checkbox"] {
  accent-color: var(--accent-color);
  width: 1.1em;
  height: 1.1em;
  vertical-align: middle;
}

.no-tasks {
  color: #aaa;
  text-align: center;
  margin-top: 2.5rem;
  font-size: 1.1rem;
}

@media (max-width: 700px) {
  .todo-table,
  .todo-table-header,
  .todo-table-row {
    max-width: 98vw;
    grid-template-columns: 28px 1fr 80px;
    font-size: 0.98rem;
    padding: 0.7rem 0.5rem;
  }
}

@media (max-width: 480px) {
  .todo-table-header,
  .todo-table-row {
    grid-template-columns: 20px 1fr 60px;
    font-size: 0.93rem;
    padding: 0.5rem 0.2rem;
  }
}
</style>
