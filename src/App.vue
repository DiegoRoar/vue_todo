<template>
  <div class="container">
    <h1 class="title">{{ title }}</h1>
    <main>
      <TodoForm @add-task="addTask" :disabled="tasks.length >= 10" />
      <TaskList :tasks />
      <div class="tasks-limit">
        <p v-if="tasks.length === 0">You can add 10 tasks</p>
        <p v-else-if="tasks.length < 10">
          You can add {{ 10 - tasks.length }} more task{{
            10 - tasks.length === 1 ? "" : "s"
          }}
        </p>
        <p v-else>You have reached the maximum of 10 tasks</p>
      </div>
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

.tasks-limit {
  position: absolute !important;
  top: 505px;
  right: 380px;
  width: 100vw;
  text-align: center;
  z-index: 100;
  pointer-events: none;
}

.tasks-limit p {
  display: inline-block;
  background: rgba(39, 40, 50, 0.92);
  color: #fbbf24;
  font-size: 1rem;
  margin: 0 auto;
  font-weight: 600;
  border-radius: 0.5em;
  padding: 0.5em 1.2em;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}
</style>
