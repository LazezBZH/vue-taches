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

export default {
  name: "HomeView",
  components: {
    HelloWorld,
    MyForm,
  },
  setup() {
    function addTask(data) {
      console.log("Home.vue | addTask()", data);
    }
    return { addTask };
  },
};
</script>
