<template>
  <div class="container">
    <header class="header">
      <h1 class="title">{{ title }}</h1>
    </header>
    <div class="content-wrapper">
      <article class="article-card">
        <h2 class="article-title">About This App</h2>
        <p class="article-subtitle">
          A modern Todo application showcasing Vue 3 and TypeScript capabilities
        </p>
        <div class="article-meta">
          <span>Vue 3</span>
          <span>•</span>
          <span>TypeScript</span>
          <span>•</span>
          <span>Composition API</span>
        </div>
        <div class="article-content">
          <p>
            This application demonstrates advanced features and best practices in Vue development,
            combining modern web technologies with a clean, intuitive interface.
          </p>
          <div class="article-section">
            <h3>Key Features</h3>
            <ul>
              <li>Vue 3 Composition API with TypeScript for type safety</li>
              <li>Responsive design with modern CSS and flexible layouts</li>
              <li>Component-based architecture for maintainable code</li>
              <li>State management using Vue's reactivity system</li>
              <li>Form handling and validation</li>
              <li>Task statistics and progress tracking</li>
            </ul>
          </div>
          <div class="article-section">
            <h3>Technical Highlights</h3>
            <ul>
              <li>TypeScript for enhanced development experience</li>
              <li>CSS Variables for consistent theming</li>
              <li>Responsive design with mobile-first approach</li>
              <li>Modern ES6+ JavaScript features</li>
              <li>Clean and maintainable code structure</li>
            </ul>
          </div>
        </div>
      </article>

      <div class="todo-section">
        <div class="form-limit-row">
          <div class="form-limit-flex">
            <TodoForm
              @add-task="addTask"
              :disabled="tasks.length >= 10"
              :tasks-length="tasks.length"
            />
          </div>
        </div>
        <div class="task-stats card" v-if="tasks.length">
          <div class="stat-item">
            <span class="stat-label">Total Tasks:</span>
            <span class="stat-value">{{ tasks.length }}</span>
          </div>
          <div class="stat-item">
            <span class="stat-label">Pending:</span>
            <span class="stat-value pending">{{ pendingTasks }}</span>
          </div>
          <div class="stat-item">
            <span class="stat-label">Completed:</span>
            <span class="stat-value completed">{{ completedTasks }}</span>
          </div>
        </div>
        <TaskList :tasks="tasks" @update-task="updateTask" @delete-task="deleteTask" />
      </div>
    </div>
    <Footer />
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from "vue";
import TodoForm from "./components/TodoForm.vue";
import TaskList from "./components/TaskList.vue";
import Footer from "./components/Footer.vue";
import { Task } from "./types";
const title = ref("Todo App with Vuejs 3 and TypeScript");

const tasks = ref<Task[]>([]);

const pendingTasks = computed(() => {
  return tasks.value.filter(task => !task.done).length;
});

const completedTasks = computed(() => {
  return tasks.value.filter(task => task.done).length;
});

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

const deleteTask = (taskId: string) => {
  tasks.value = tasks.value.filter(t => t.id !== taskId);
};
</script>

<style scoped>
.header {
  margin-bottom: var(--spacing-xl);
  text-align: center;
}

.todo-section {
  margin-top: var(--spacing-2xl);
}

.article-content {
  color: var(--text-color);
}

.article-content h3 {
  color: var(--accent-color);
  margin: var(--spacing-lg) 0 var(--spacing-md);
  font-size: var(--text-xl);
}

.article-content ul {
  list-style: disc;
  padding-left: var(--spacing-lg);
  margin-bottom: var(--spacing-md);
}

.article-content li {
  margin-bottom: var(--spacing-sm);
  color: var(--text-muted);
}

.article-content li:last-child {
  margin-bottom: 0;
}

.task-stats {
  display: flex;
  gap: var(--spacing-lg);
  margin: var(--spacing-md) 0;
}

.stat-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-xs);
}

.stat-label {
  font-size: var(--text-sm);
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.stat-value {
  font-size: var(--text-xl);
  font-weight: 700;
  color: var(--accent-color);
}

.stat-value.pending {
  color: var(--warning-color);
}

.stat-value.completed {
  color: var(--success-color);
}

@media (max-width: 900px) {
  .task-stats {
    flex-direction: row;
    justify-content: space-around;
    padding: var(--spacing-md);
  }
}

@media (max-width: 600px) {
  .article-content h3 {
    font-size: var(--text-lg);
  }

  .task-stats {
    flex-direction: column;
    gap: var(--spacing-md);
    padding: var(--spacing-md);
  }

  .stat-item {
    flex-direction: row;
    justify-content: space-between;
    width: 100%;
    padding: var(--spacing-sm) 0;
    border-bottom: 1px solid var(--border-color);
  }

  .stat-item:last-child {
    border-bottom: none;
  }

  .stat-label {
    font-size: var(--text-sm);
  }

  .stat-value {
    font-size: var(--text-lg);
  }
}
</style>
