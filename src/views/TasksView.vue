<template>
  <h2>Toutes les tâches</h2>
  <div v-if="tasks.length > 0">
    <div class="task" v-for="task in tasks" :key="task.id">
      <h3>{{ task.name }}</h3>
      <p>{{ task.description }}</p>
      <p>Échéance: {{ convertCase(task.temporality) }}</p>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import tasksService from "@/services/tasks.js";
export default {
  name: "TasksView",
  setup() {
    const tasks = ref([]);
    tasks.value = tasksService.read();
    function convertCase(temporality) {
      return tasksService.convertCase(temporality);
    }
    return { tasks, convertCase };
  },
};
</script>

<style scoped>
.task {
  width: 50%;
  margin: auto;
  border: 0.3rem solid #42b983;
  border-radius: 1rem;
}
h2 {
  color: #42b983;
}
</style>
