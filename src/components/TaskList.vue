<template>
  <section v-if="tasks.length" class="todo-table">
    <div class="todo-table-header">
      <span>#</span>
      <span>Task</span>
      <span>Status</span>
      <span>Actions</span>
    </div>
    <div v-for="(task, idx) in tasks" :key="task.id" class="todo-table-row">
      <span class="todo-task-index">{{ idx + 1 }}</span>
      <span class="todo-task-title">{{ task.title }}</span>
      <span>
        <input 
          type="checkbox" 
          :checked="task.done" 
          @change="handleDoneChange(task.id, !task.done)"
          :id="'done-' + task.id" 
        />
        <label :for="'done-' + task.id" class="done-label">
          <span v-if="task.done" class="done-status">Done</span>
          <span v-else class="pending-status">Pending</span>
        </label>
      </span>
      <span class="task-actions">
        <button @click="handleDelete(task.id)" class="delete-btn" title="Delete task">
          <span class="delete-icon">×</span>
        </button>
      </span>
    </div>
  </section>
  <p v-else class="no-tasks">No tasks yet. Add your first task!</p>
</template>

<script lang="ts" setup>
import { Task } from "../types";
const props = defineProps<{
  tasks: Task[];
}>();

const emit = defineEmits<{
  'update-task': [taskId: string, done: boolean],
  'delete-task': [taskId: string]
}>();

const handleDoneChange = (taskId: string, done: boolean) => {
  emit('update-task', taskId, done);
};

const handleDelete = (taskId: string) => {
  emit('delete-task', taskId);
};
</script>

<style scoped>
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
  grid-template-columns: 40px 1fr 120px 80px;
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
  border-radius: 0.5rem 0.5rem 0 0;
  margin-bottom: 0.2rem;
  padding-bottom: 0.3rem;
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

.task-actions {
  display: flex;
  justify-content: center;
  align-items: center;
}

.delete-btn {
  background: none;
  border: none;
  color: #ff4444;
  cursor: pointer;
  padding: 0.3em 0.6em;
  border-radius: 0.3em;
  transition: all 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.delete-btn:hover {
  background: rgba(255, 68, 68, 0.1);
}

.delete-icon {
  font-size: 1.4em;
  font-weight: bold;
  line-height: 1;
}

@media (max-width: 900px) {
  .todo-table {
    max-width: 100vw;
    margin: 1.5rem 0 0 0;
    border-radius: 0.7rem;
  }
  .todo-table-header,
  .todo-table-row {
    grid-template-columns: 28px 1fr 80px 60px;
    font-size: 0.98rem;
    padding: 0.7rem 0.5rem;
  }
}

@media (max-width: 600px) {
  .todo-table {
    max-width: 100vw;
    margin: 1rem 0 0 0;
    border-radius: 0.5rem;
    font-size: 0.93rem;
  }
  .todo-table-header {
    display: none;
  }
  .todo-table-row {
    display: grid;
    grid-template-columns: 1fr;
    background: rgba(39, 40, 50, 0.92);
    border-radius: 0.4rem;
    margin-bottom: 0.7em;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
    padding: 0.8em;
    gap: 0.5em;
  }
  .todo-table-row span {
    display: block;
    width: 100%;
    text-align: left;
    padding: 0.1em 0;
  }
  .todo-task-index {
    font-size: 0.85em;
    color: #aaa;
    margin-bottom: 0.1em;
    font-weight: 600;
  }
  .todo-task-title {
    padding-right: 0;
    margin-bottom: 0.2em;
    font-weight: 600;
    color: var(--text-color);
    font-size: 1.05em;
    line-height: 1.4;
  }
  .task-actions {
    display: flex;
    justify-content: flex-end;
    margin-top: 0.3em;
    padding-top: 0.3em;
    border-top: 1px solid rgba(255, 255, 255, 0.06);
  }
  .delete-btn {
    padding: 0.3em 0.6em;
    font-size: 1.1em;
  }
  .delete-icon {
    font-size: 1.2em;
  }
  .done-label {
    margin-left: 0;
    margin-top: 0.2em;
    display: flex;
    align-items: center;
    gap: 0.5em;
  }
  input[type="checkbox"] {
    margin-right: 0.5em;
    width: 1.2em;
    height: 1.2em;
  }
}

@media (max-width: 400px) {
  .todo-table-row {
    padding: 0.6em;
    gap: 0.4em;
  }
  .todo-task-title {
    font-size: 1em;
  }
  .todo-task-index {
    font-size: 0.8em;
  }
  .done-label {
    font-size: 0.9em;
  }
  .delete-btn {
    padding: 0.2em 0.5em;
  }
}
</style>
