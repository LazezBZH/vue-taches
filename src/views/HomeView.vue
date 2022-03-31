<template>
  <div class="home">
    <HelloWorld msg="Tâches" />
    <MyForm @createtask="addTask" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import MyForm from "@/components/MyForm.vue";
import tasksServices from "@/services/tasks.js";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
    MyForm,
  },
  setup() {
    function addTask(data) {
      console.log("Home.vue | addTask()", data);
      tasksServices.create(data);
    }
    return { addTask };
  },
};
</script>
