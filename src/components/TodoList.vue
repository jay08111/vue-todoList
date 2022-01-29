<template>
  <article>
    <p :class="done" @click="$emit('toggleTodo')">
      {{ todo.title }}
    </p>
    <div class="btn__container">
      <button @click="deleteTodo(todo.id)">x</button>
      <button @click="editTodo(todo.id, todo.title)">edit</button>
    </div>
  </article>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    todo: {
      type: Object,
    },
  },
  methods: {
    deleteTodo(id) {
      this.$emit("deleteTodo", id);
    },
    editTodo(id, title) {
      this.$emit("editTodo", id, title);
    },
  },
  computed: {
    done() {
      let classes = [""];
      if (this.todo.completed) {
        classes.push("done");
      }
      return classes;
    },
  },
};
</script>

<style lang="scss" scoped>
article {
  display: flex;
  justify-content: space-between;
  margin-top: 1.45rem;
  p {
    font-size: 1.6rem;
    cursor: pointer;
  }
  .done {
    text-decoration: line-through;
  }
  .btn__container {
    display: flex;
    flex-direction: row;
    gap: 20px;
    button {
      border: none;
      font-size: 1.2rem;
      background: transparent;
      cursor: pointer;
      transition: all 0.2s linear;
      &:nth-child(1) {
        font-size: 1.5rem;
        margin-right: 1.5rem;
        &:hover {
          color: red;
        }
      }
      &:nth-child(2) {
        &:hover {
          color: green;
        }
      }
    }
  }
}
</style>
