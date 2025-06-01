<template>
  <form @submit.prevent="formSubmitted">
    <label for="newTask">New Task</label>
    <textarea
      v-model="newTask"
      name="newTask"
      id="newTask"
      placeholder="Add a new task... (max 250 characters)"
      :class="{ 'has-error': !!error }"
      :aria-invalid="!!error || undefined"
      @input="error = ''"
      maxlength="250"
      rows="5"
    ></textarea>
    <div class="error-group">
      <small v-if="error" class="small-error">{{ error }}</small>
      <!-- <small v-else" class="small-ok">{{ }}</small> -->
    </div>

    <div class="btn-container">
      <button type="submit" class="btn">Add Task</button>
    </div>
  </form>
</template>

<script lang="ts" setup>
import { ref } from "vue";
const newTask = ref("");

const emit = defineEmits<{
  addTask: [newTask: string];
}>();

const error = ref("");

// functions
const formSubmitted = () => {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim());
    newTask.value = "";
  } else {
    error.value = "Task cannot be empty!";
  }
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  margin-top: 2.5rem;
  width: 100%;
  max-width: 600px;
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
  display: none;
}

textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  border: none;
  border-radius: 0.5rem;
  background: var(--hover-color);
  color: var(--text-color);
  font-size: 1rem;
  transition: box-shadow 0.2s, border 0.2s;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
  resize: vertical;
  min-height: 60px;
  max-height: 200px;
}

textarea:focus {
  outline: none;
  border: 2px solid var(--accent-color);
  box-shadow: 0 0 0 2px var(--accent-color) 33;
}

.btn-container {
  display: flex;
  justify-content: flex-end;
  width: 100%;
}

.error-group {
  width: 100%;
  display: flex;
  justify-content: flex-start;
}
.small-error {
  color: red;
  font-size: 0.8rem;
  margin-top: -0.5rem;
  text-align: left;
}

@media (max-width: 900px) {
  form {
    max-width: 98vw;
    padding: 1.2rem 0.5rem 1rem 0.5rem;
  }
  textarea {
    font-size: 0.98rem;
    padding: 0.7rem 0.7rem;
    min-height: 48px;
    max-height: 140px;
  }
  .btn-container {
    justify-content: center;
  }
}

@media (max-width: 600px) {
  form {
    max-width: 100vw;
    padding: 1rem 0.2rem 0.7rem 0.2rem;
  }
  textarea {
    font-size: 0.95rem;
    padding: 0.6rem 0.5rem;
    min-height: 36px;
    max-height: 100px;
  }
}
</style>
