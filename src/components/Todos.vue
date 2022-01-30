<template>
  <section>
    <h1>To do list</h1>
    <form @submit.prevent="addTodo">
      <div class="input__field">
        <input type="text" placeholder="add to do" v-model="title" />
        <button>{{ isEditing ? "Edit" : "Add" }}</button>
      </div>
    </form>
    <div v-for="todo in todos" :key="todo.id" class="todo__list">
      <TodoList
        :todo="todo"
        @deleteTodo="deleteTodo"
        @toggleTodo="toggleTodo(todo)"
        @editTodo="editTodo"
      />
    </div>
    <div class="btn__container">
      <button @click="todos = []" v-if="todos.length > 0">clear all</button>
      <button @click="completed" v-if="todos.length > 0">
        completed clear
      </button>
    </div>
    <h1 v-if="todos.length === 0">there is nothing...</h1>
  </section>
</template>

<script>
import TodoList from "./TodoList.vue";
export default {
  name: "Todos",
  components: {
    TodoList,
  },
  data() {
    return {
      todos: [
        { id: 1, title: "Talk with Daysha", completed: false },
        { id: 2, title: "Wait Daysha", completed: true },
        { id: 3, title: "eat dinner with Daysha", completed: false },
        { id: 4, title: "have fun with Daysha", completed: true },
      ],
      title: "",
      isEditing: false,
      editId: null,
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
    addTodo() {
      if (!this.title) {
        return;
      } else if (this.isEditing && this.title) {
        this.todos = this.todos.map((item) =>
          item.id === this.editId
            ? { id: this.editId, title: this.title, completed: false }
            : item
        );
        this.isEditing = false;
        this.title = "";
        this.editId = null;
      } else {
        const newTodo = {
          id: Math.floor(Math.random() * 10000),
          title: this.title,
          completed: false,
        };
        this.todos = [...this.todos, newTodo];
        this.title = "";
      }
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    editTodo(id, title) {
      this.isEditing = true;
      this.editId = id;
      this.title = title;
    },
    completed() {
      this.todos = this.todos.filter((item) => item.completed === false);
    },
  },
};
</script>

<style lang="scss" scoped>
section {
  h1 {
    margin-top: 2rem;
    font-size: 2rem;
  }
  .input__field {
    display: flex;
    flex-direction: row;
    gap: 10px;
    margin-top: 1.2rem;
    margin-bottom: 1.2rem;
    input {
      width: 100%;
      padding: 10px;
      outline: none;
      &::placeholder {
        font-size: 1.2rem;
      }
    }
    button {
      border: 1px solid red;
      background: transparent;
      padding: 10px;
      cursor: pointer;
    }
  }
  .todo__list {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
  .btn__container {
    display: flex;
    justify-content: center;
    margin-top: 2.5rem;
    gap: 20px;
    button {
      border: none;
      background: transparent;
      font-size: 1.4rem;
      padding: 15px 10px;
      cursor: pointer;
      border: 1px solid red;
    }
  }
}
</style>
