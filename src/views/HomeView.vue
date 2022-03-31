<template>
  <div class="home">
    <HelloWorld msg="Tâches" />
    <MyForm />
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
};
</script>
