<template>
  <main id="app">
    <Todo />
  </main>
</template>

<script lang="ts">
import Vue from "vue";
import Todo from "./components/Todo.vue";
export default Vue.extend({
  name: "App",
  components: {
    Todo,
  },
});
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  max-width: 750px;
  margin: 0 auto;
}
</style>
