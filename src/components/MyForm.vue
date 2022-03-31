<template>
  <h2>Créer une tâche</h2>
  <form>
    <input type="text" placeholder="Nom de la tâche" v-model="name" /> <br />
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
    <button>Créer</button>
  </form>
</template>
<script>
import { ref } from "vue";
export default {
  name: "MyForm",
  setup() {
    const name = ref("");
    const description = ref("");
    const temporalityTypes = ref([
      {
        id: 1,
        name: "court terme",
        value: "short-terme",
      },
      {
        id: 2,
        name: "moyen terme",
        value: "medium-terme",
      },
      {
        id: 3,
        name: "long terme",
        value: "long-terme",
      },
    ]);
    const temporality = ref("");
    return { name, description, temporalityTypes, temporality };
  },
};
</script>
<style scoped>
input,
textarea,
select,
button {
  width: 80%;
  margin: 2rem 4rem;
}
</style>
