<template>
  <article>
    <form @submit="onSubmit">
      <div
        v-for="{ title, id, completed } in todos"
        :key="id"
        class="todo-item"
      >
        <p :class="{ done: completed }" @click="toggleTodo()">
          {{ title }}
        </p>
        <div class="btn__container">
          <button class="btn delete" @click="deleteTodo(id)">x</button>
          <button
            class="btn edit"
            @click="
              {
                editTodo($event, id);
                edit();
              }
            "
          >
            edit
          </button>
        </div>
      </div>
      <button type="submit">submit</button>
    </form>
  </article>
</template>
<script>
export default {
  props: {
    todos: Array,
    newTodo: String,
    isEditing: Boolean,
    editId: null,
  },

  methods: {
    onSubmit() {
      if (this.newTodo) {
        const newTodo = {
          id: Math.floor(Math.random() * 10000),
          title: this.newTodo,
          completed: false,
        };
        this.todos = [...this.todos, newTodo];
        this.newTodo = "";
      }
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
    toggleTodo() {
      this.todos.completed = !this.todos.completed;
      console.log(this.todos.completed);
    },

    editTodo($event, id) {
      this.isEditing = true;
      this.editId = id;
      this.newTodo = $event.target.value;
      console.log(this.isEditing, this.editId, this.newTodo);
    },
  },
  computed: {
    id() {
      return Math.floor(Math.random() * 10000);
    },
  },
};
</script>
<style lang="scss"></style>
