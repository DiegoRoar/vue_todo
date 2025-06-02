<template>
  <div class="container">
    <h1 class="title">{{ title }}</h1>
    <main>
      <div class="form-limit-row">
        <div class="form-limit-flex">
          <TodoForm
            @add-task="addTask"
            :disabled="tasks.length >= 10"
            :tasks-length="tasks.length"
          />
        </div>
      </div>
      <TaskList :tasks="tasks" @update-task="updateTask" />
    </main>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import TodoForm from "./components/TodoForm.vue";
import TaskList from "./components/TaskList.vue";
import { Task } from "./types";
const title = ref("Todo App with Vuejs 3 and TypeScript");

const tasks = ref<Task[]>([]);

const addTask = (newTask: string) => {
  if (tasks.value.length < 10) {
    tasks.value.push({
      id: crypto.randomUUID(),
      title: newTask,
      done: false,
    });
  }
};

const updateTask = (taskId: string, done: boolean) => {
  const task = tasks.value.find(t => t.id === taskId);
  if (task) {
    task.done = done;
  }
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

.form-limit-row {
  width: 100%;
  margin-bottom: 1.2rem;
}

.form-limit-flex {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.2rem;
  width: 100%;
}

.tasks-limit-inline {
  align-self: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-width: 160px;
  font-size: 1rem;
  color: #fbbf24;
  font-weight: 600;
  background: rgba(39, 40, 50, 0.92);
  border-radius: 0.5em;
  padding: 0.5em 1.2em;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  margin-top: 0;
  height: fit-content;
}

@media (max-width: 900px) {
  .form-limit-flex {
    flex-direction: column;
    align-items: stretch;
    gap: 0.5rem;
  }
  .tasks-limit-inline {
    margin-top: 0.5em;
    align-self: stretch;
    width: 100%;
    text-align: left;
    font-size: 0.95rem;
    padding: 0.4em 0.8em;
  }
}

@media (max-width: 600px) {
  .tasks-limit-inline {
    font-size: 0.9rem;
    padding: 0.3em 0.5em;
  }
}
</style>
