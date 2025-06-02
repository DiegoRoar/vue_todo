<template>
  <form @submit.prevent="formSubmitted">
    <div class="form-header-row">
      <label for="newTask">New Task</label>
      <div class="tasks-limit-inline">
        <span v-if="tasksLength === 0">You can add 10 tasks</span>
        <span v-else-if="tasksLength < 10">
          You can add {{ 10 - tasksLength }} more task{{
            10 - tasksLength === 1 ? "" : "s"
          }}
        </span>
        <span v-else>You have reached the maximum of 10 tasks</span>
      </div>
    </div>
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
      :disabled="disabled"
    ></textarea>
    <div class="error-group">
      <small v-if="error" class="small-error">{{ error }}</small>
      <small v-else-if="disabled" class="small-error"
        >Task limit reached (10/10)</small
      >
    </div>
    <div class="btn-container">
      <button type="submit" class="btn" :disabled="disabled">Add Task</button>
    </div>
  </form>
</template>

<script lang="ts" setup>
import { ref, defineProps, watch } from "vue";
const props = defineProps<{ disabled?: boolean; tasksLength?: number }>();
const newTask = ref("");
const emit = defineEmits<{ addTask: [newTask: string] }>();
const error = ref("");

watch(
  () => props.disabled,
  (val) => {
    if (val) newTask.value = "";
  }
);

const formSubmitted = () => {
  if (props.disabled) return;
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
.form-header-row {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.2rem;
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
label {
  font-size: 1rem;
  color: var(--text-color);
  margin-bottom: 0.3rem;
  margin-left: 0.5rem;
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
  .form-header-row {
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
