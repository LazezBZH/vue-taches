<template>
  <div class="modal-background">
    <div class="modal">
      <div>
        <h2>Modifier cette tâche</h2>
        <form @submit.prevent="saveTask">
          <input
            type="text"
            v-model="taskToEdit.name"
            placeholder="Nom de la tâche"
          />
          <br />
          <textarea
            name=""
            id=""
            cols="30"
            rows="10"
            v-model="taskToEdit.description"
          ></textarea>
          <br />
          <select v-model="taskToEdit.temporality">
            <option
              v-for="tempo in temporalityTypes"
              :value="tempo.value"
              :key="tempo.id"
              :selected="tempo.value === taskToEdit.temporality"
            >
              {{ tempo.name }}
            </option></select
          ><br />
          <button :disabled="!isFormValid">Sauvegarder</button>
          <button @click="cancel">Annuler</button>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed } from "vue";
export default {
  name: "MyModal",
  props: {
    task: {
      require: true,
    },
  },
  setup(props, context) {
    let taskToEdit = ref({ ...props.task });
    const temporalityTypes = ref([
      {
        id: 1,
        name: "court terme",
        value: "short-term",
      },
      {
        id: 2,
        name: "moyen terme",
        value: "medium-term",
      },
      {
        id: 3,
        name: "long terme",
        value: "long-term",
      },
    ]);
    let temporality = ref("");
    function saveTask() {
      const taskUpdated = {
        id: taskToEdit.value.id,
        name: taskToEdit.value.name,
        description: taskToEdit.value.description,
        temporality: taskToEdit.value.temporality,
      };
      console.log("taskUpdated", taskUpdated);
      context.emit("updatetask", taskUpdated);
    }
    function cancel() {
      context.emit("cancel");
    }
    const isFormValid = computed(() => {
      if (
        taskToEdit.value.name !== "" &&
        taskToEdit.value.description !== "" &&
        taskToEdit.value.temporality !== ""
      ) {
        return true;
      } else {
        return false;
      }
    });
    return {
      temporalityTypes,
      temporality,
      taskToEdit,
      saveTask,
      cancel,
      isFormValid,
    };
  },
};
</script>

<style scoped>
.modal-background {
  position: fixed;
  z-index: 999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  display: table;
  transition: opacity 05s ease;
}
.modal {
  width: 50%;
  margin: 2rem auto;
  border: 0.3rem solid #42b983;
  border-radius: 0.8rem;
  background-color: white;
  padding-bottom: 2rem;
}
input,
textarea,
select {
  width: 60%;
  margin: 0.5rem auto;
}
input,
select {
  height: 1.7rem;
}
button {
  margin: 0.5rem;
  border: none;
  border-radius: 0.3rem;
  background: #42b983;
  color: white;
  padding: 0.4rem;
  cursor: pointer;
}
button:disabled {
  color: rgba(255, 0, 0, 0.4);
  cursor: not-allowed;
}
</style>
