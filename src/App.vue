<template>
  <div class="container">
    <h1 class="title">{{ title }}</h1>
    <main>
      <TodoForm @add-task="addTask" />
      <article v-for="task in tasks" :key="task.id">{{ task.title }}</article>
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
</style>
