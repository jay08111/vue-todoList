<template>
  <article>
    <div v-for="({ id, title, completed }, index) in todos" :key="id">
      <p
        :class="{ done: completed }"
        @click="(e) => e.target.classList.toggle('done')"
        v-if="!isEditing"
      >
        <span>{{ index + 1 }})</span> {{ title }}
      </p>
      <div class="btn__container">
        <button @click="deleteTodo(id)">x</button>
        <button @click="editTodo(id, title)">edit</button>
      </div>
    </div>
    <div class="delete__all__btn">
      <button class="delete__all" @click="deleteAll">Delete all</button>
    </div>
  </article>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    title: {
      type: String,
      default: "",
    },
    todos: {
      type: Array,
    },
    isEditing: {
      type: Boolean,
    },
  },
  data() {
    return {};
  },
  methods: {
    deleteTodo(id) {
      this.$emit("delete-todo", id);
    },
    toggleTodo() {
      this.$emit("toggle-todo");
    },
    deleteAll() {
      this.$emit("delete-all");
    },
    editTodo(event, id) {
      this.$emit("edit-todo", event, id);
    },
  },
};
</script>

<style lang="scss">
article {
  display: flex;
  flex-direction: column;
  gap: 30px;
  margin-top: 2rem;
  div {
    font-size: 1.2rem;
    display: flex;
    justify-content: space-between;
    p {
      cursor: pointer;
      span {
        margin-right: 7px;
      }
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
        transition: all 0.2s linear;
        cursor: pointer;
        &:nth-child(1) {
          margin-right: 15px;
          font-size: 1.5rem;
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
  .delete__all__btn {
    display: flex;
    justify-content: center;
    margin-top: 1rem;
    .delete__all {
      width: 20%;
      border: none;
      background: transparent;
      font-size: 1rem;
      border: 1px solid red;
      padding: 10px 0;
      transition: all 0.2s linear;
      cursor: pointer;
      &:hover {
        background: crimson;
        color: #fff;
        border-radius: 10px;
      }
    }
  }
}
</style>
