<template>
  <section class="wrapper">
    <h1>Todo - List</h1>
    <input
      type="text"
      class="todo-input"
      placeholder="what needs to be done"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
    <TodoList
      :todos="todos"
      :newTodo="newTodo"
      :isEditing="isEditing"
      :editId="editId"
    />
    <button v-if="hasTodos" class="btn deleteAll" @click="deleteAll">
      delete all
    </button>
  </section>
</template>

<script>
import TodoList from "./TodoList.vue";
export default {
  name: "todos",
  components: {
    TodoList,
  },
  data() {
    return {
      newTodo: "",
      todos: [
        {
          id: 1,
          title: "Studying Vue.js",
          completed: false,
        },
        {
          id: 2,
          title: "Talk with my dad",
          completed: true,
        },
        {
          id: 3,
          title: "Go outside and meet friends",
          completed: false,
        },
      ],
      isEditing: false,
      editId: null,
    };
  },
  methods: {
    deleteAll() {
      this.todos = [];
    },
  },
  computed: {
    hasTodos() {
      return this.todos.length > 0;
    },
  },
};
</script>

<style lang="scss">
.wrapper {
  margin-top: 5rem;
  h1 {
    font-size: 2.2rem;
    margin-bottom: 1rem;
  }
  .todo-input {
    width: 100%;
    padding: 10px;
    font-size: 1rem;
    margin-top: 1.2rem;
    margin-bottom: 1rem;
    border-radius: 5px;
    border-color: #333;
    &:focus {
      outline: 0;
    }
  }
  .todo-input::placeholder {
    font-size: 1rem;
  }
  .btn {
    border: none;
    padding: 12px;
    background: transparent;
    font-size: 1.4rem;
    cursor: pointer;
    transition: all 0.3s ease;
  }
  article {
    position: relative;
    margin-top: 15px;
    display: flex;
    gap: 15px;
    flex-direction: column;
    font-size: 1.2rem;
    .todo-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      .btn__container {
        width: 12vw;
        .delete {
          &:hover {
            color: red;
          }
        }
        .edit {
          font-size: 1.2rem;
          &:hover {
            color: green;
          }
        }
      }
    }
    .done {
      text-decoration: line-through;
      cursor: pointer;
    }
  }
  .deleteAll {
    font-size: 1rem;
    padding: 0.5rem;
    text-transform: capitalize;
    border: 1px solid red;
    border-radius: 10px;
    margin-top: 25px;
    &:hover {
      color: red;
    }
  }
}
</style>
