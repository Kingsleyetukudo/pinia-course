<template>
  <div>
    <main>
      <header>
        <img src="./assets/pinia-logo.svg" alt="" />
        <h1>Pinia Tasks</h1>
      </header>

      <div class="new-task-form">
        <TaskForm />
      </div>

      <nav class="filter">
        <button @click="filter = 'all'">All Tasks</button>
        <button @click="filter = 'fav'">Fav Tasks</button>
      </nav>

      <!-- loading -->
      <div class="loading" v-if="taskStore.loading">Loading tasks...</div>

      <!-- task list -->
      <div class="task-list" v-if="filter == 'all'">
        <p>You have {{ taskStore.totalCount }} tasks left to do</p>
        <div v-for="task in taskStore.tasks">
          <TaskDetails :task="task" />
        </div>
      </div>

      <div class="task-list" v-if="filter == 'fav'">
        <p>You have {{ taskStore.favCount }} tasks left to do</p>
        <div v-for="task in taskStore.isfav">
          <TaskDetails :task="task" />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import { ref } from "vue";
import TaskDetails from "./components/TaskDetails.vue";
import { useTaskStore } from "./stores/TaskStore";
import TaskForm from "./components/TaskForm.vue";
export default {
  components: {
    TaskDetails,
    TaskForm,
  },
  setup() {
    const taskStore = useTaskStore();

    taskStore.getTasks();
    const filter = ref("all");

    return {
      taskStore,
      filter,
    };
  },
};
</script>
