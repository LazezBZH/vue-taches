<template>
  <h2>Toutes les tâches</h2>
  {{ isInEditMode }}
  <MyModal
    v-if="isInEditMode"
    :task="taskToEdit"
    @updatetask="updateTask($event)"
    @cancel="cancelEdit"
  />
  <input
    type="search"
    name=""
    id="search"
    placeholder="Filtrer"
    v-model="letters"
    @keyup="filter"
  />
  <div class="radio-filters">
    <label for="all"
      ><input
        type="radio"
        id="all"
        value=""
        v-model="selectedTemporality"
      />Toutes</label
    >
    <label for="short-term"
      ><input
        type="radio"
        id="short-term"
        value="short-term"
        v-model="selectedTemporality"
      />Court terme</label
    >
    <label for="medium-term"
      ><input
        type="radio"
        id="medium-term"
        value="medium-term"
        v-model="selectedTemporality"
      />Moyen terme</label
    >
    <label for="long-term"
      ><input
        type="radio"
        id="long-term"
        value="long-term"
        v-model="selectedTemporality"
      />Long terme</label
    >
  </div>
  <div v-if="tasks.length > 0">
    <div class="task" v-for="task in tasksFiltered" :key="task.id">
      <h3>{{ task.name }}</h3>
      <p>{{ task.description }}</p>
      <p>Échéance: {{ convertCase(task.temporality) }}</p>
      <button class="btn" @click="() => deleteTask(task.id)">suppr</button>
      <button class="btn" @click="() => toggle(task)">modif</button>
    </div>
  </div>
</template>

<script>
import { ref, watch } from "vue";
import tasksService from "@/services/tasks.js";
import MyModal from "../components/MyModal.vue";
export default {
  name: "TasksView",
  components: {
    MyModal,
  },
  setup() {
    const tasks = ref([]);
    const letters = ref("");
    const selectedTemporality = ref("");
    let tasksFiltered = ref([]);
    let isInEditMode = ref(false);
    let taskToEdit = ref(null);
    tasks.value = tasksService.read();

    filter();

    function convertCase(temporality) {
      return tasksService.convertCase(temporality);
    }
    function filter() {
      console.log(letters.value);
      if (letters.value.length === 0) {
        tasksFiltered.value = tasks.value;
      } else {
        tasksFiltered.value = tasks.value.filter((t) =>
          t.name.toLocaleLowerCase().includes(letters.value.toLocaleLowerCase())
        );
      }
      if (selectedTemporality.value !== "") {
        tasksFiltered.value = tasksFiltered.value.filter(
          (t) => t.temporality === selectedTemporality.value
        );
        console.log("tasksFiltered", tasksFiltered);
        console.log("selectedTemporlity.value", selectedTemporality.value);
      }
    }

    function toggle(task) {
      taskToEdit.value = task;
      isInEditMode.value = true;
    }

    function updateTask(task) {
      console.log("updateTask", task);
    }

    function cancelEdit() {
      isInEditMode.value = false;
      taskToEdit.value = null;
    }

    function deleteTask(id) {
      tasksService.deleteTask(id);
      tasks.value = tasksService.read();
      filter();
    }

    watch(selectedTemporality, (newValue, oldValue) => {
      console.log("new: ", newValue, "   ", "old: ", oldValue);
      if (newValue !== "") {
        filter();
      } else {
        tasksFiltered.value = tasks.value;
        filter();
      }
    });

    return {
      tasks,
      letters,
      selectedTemporality,
      tasksFiltered,
      convertCase,
      filter,
      deleteTask,
      isInEditMode,
      taskToEdit,
      toggle,
      updateTask,
      cancelEdit,
    };
  },
};
</script>

<style scoped>
.task {
  width: 50%;
  margin: 0.5rem auto;

  border: 0.3rem solid #42b983;
  border-radius: 1rem;
}
h2 {
  color: #42b983;
}
.radio-filters {
  display: flex;
  justify-content: center;
}
#search {
  height: 2rem;
  color: rgb(9, 103, 192);
  font-size: 1.5rem;
}
</style>
