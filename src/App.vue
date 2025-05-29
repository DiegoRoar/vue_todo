<template>
  <div class="container">
    <main>
      <h1 class="title">{{ title }}</h1>
      <form @submit.prevent="">
        <label for="newTask">New Task</label>
        <input
          v-model="newTask"
          name="newTask"
          id="newTask"
          type="text"
          placeholder="Add a new task..."
        />
      </form>
    </main>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const title = ref("Todo App with Vuejs 3 and TypeScript");
const newTask = ref("");
</script>

<style>
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

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  margin-top: 2.5rem;
  width: 700px;
  max-width: 90%;
  margin-left: auto;
  margin-right: auto;
}

label {
  font-size: 1rem;
  color: var(--text-color);
  margin-bottom: 0.3rem;
  letter-spacing: 0.02em;
  font-weight: 600;
  align-self: flex-start;
}

input[type="text"] {
  width: 100%;
  padding: 0.75rem 1rem;
  border: none;
  border-radius: 0.5rem;
  background: var(--hover-color);
  color: var(--text-color);
  font-size: 1rem;
  transition: box-shadow 0.2s, border 0.2s;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
}

input[type="text"]:focus {
  outline: none;
  border: 2px solid var(--accent-color);
  box-shadow: 0 0 0 2px var(--accent-color) 33;
}
</style>
