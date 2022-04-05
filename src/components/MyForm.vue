<template>
  <h2>Créer une tâche</h2>
  <form v-on:submit.prevent="createTask">
    <input
      type="text"
      placeholder="Nom de la tâche"
      v-model="name"
      ref="txtName"
    />
    <br />
    <textarea
      name=""
      id=""
      cols="30"
      rows="10"
      v-model="description"
      placeholder="Description de la tâche"
    ></textarea>
    <br />
    <select name="" id="" v-model="temporality">
      <option
        v-for="tempo in temporalityTypes"
        :value="tempo.value"
        :key="tempo.id"
      >
        {{ tempo.name }}
      </option></select
    ><br />
    <button :disabled="!isFormValid">Créer</button>
  </form>
</template>
<script>
import { ref, onMounted, computed } from "vue";
export default {
  name: "MyForm",
  emits: ["createtask"],
  setup(props, context) {
    const name = ref("");
    const description = ref("");
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
    const temporality = ref("");
    let txtName = ref(null);

    function createTask() {
      const task = {
        id: Date.now(),
        name: name.value,
        description: description.value,
        temporality: temporality.value,
      };
      console.log("task", task);
      context.emit("createtask", task);
      resetForm();
    }
    function resetForm() {
      name.value = "";
      description.value = "";
      temporality.value = "";
      txtName.value.focus();
    }
    onMounted(() => {
      txtName.value.focus();
    });
    const isFormValid = computed(() => {
      if (
        name.value !== "" &&
        description.value !== "" &&
        temporality.value !== ""
      ) {
        return true;
      } else {
        return false;
      }
    });
    return {
      name,
      description,
      temporalityTypes,
      temporality,
      createTask,
      txtName,
      isFormValid,
    };
  },
};
</script>
<style scoped>
input,
textarea,
select,
button {
  width: 50%;
  height: 2rem;
  margin: 1rem auto;
  border: 0.2rem solid #42b983;
  border-radius: 0.3rem;
}
textarea {
  height: auto;
}
button {
  background-color: #85bba385;
  font-size: 1.2rem;
  font-weight: bolder;
}
h2 {
  color: #42b983;
}
button:disabled {
  color: rgba(255, 0, 0, 0.2);
  cursor: not-allowed;
}
</style>
