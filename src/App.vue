<template>
  <main id="app" class="container">
    <Todos />
  </main>
</template>

<script>
import Todos from "./components/Todos.vue";
export default {
  name: "App",
  components: {
    Todos,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  max-width: 600px;
  margin: 0 auto;
}
</style>
