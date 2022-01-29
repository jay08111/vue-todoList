<template>
  <section>
    <h1>Todo List</h1>
    <input
      type="text"
      placeholder="Add new Task"
      v-model="title"
      @keyup.enter="addTodo"
      autocomplete="off"
    />
    <TodoList
      v-if="todos.length"
      :title="title"
      :todos="todos"
      :isEditing="isEditing"
      @delete-todo="deleteTodo"
      @toggle-todo="toggleTodo"
      @delete-all="deleteAll"
      @edit-todo="editTodo"
    />
    <h2 v-else>There is nothing ...</h2>
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
      title: "",
      todos: [
        { id: 1, title: "Talk with Daysha", completed: true },
        { id: 2, title: "Wait Daysha", completed: false },
        { id: 3, title: "eat dinner with Daysha", completed: false },
        { id: 4, title: "have fun with Daysha", completed: true },
      ],
      setTodoId: null,
      isEditing: false,
    };
  },
  methods: {
    addTodo() {
      if (this.title) {
        const newTodo = {
          id: Math.floor(Math.random() * 1000),
          title: this.title,
          completed: false,
        };
        this.todos = [...this.todos, newTodo];
        this.title = "";
        this.setTodoId = newTodo.id;
        console.log(this.setTodoId);
      }
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
    toggleTodo() {
      this.completed = !this.completed;
      console.log(this.completed);
    },
    deleteAll() {
      this.todos = [];
    },
    editTodo(id) {
      this.setTodoId = id;
      this.isEditing = true;
    },
  },
};
</script>

<style lang="scss">
section {
  h1 {
    margin-top: 3rem;
    font-size: 2rem;
  }
  input {
    width: 100%;
    margin-top: 2rem;
    padding: 10px;
    outline: none;
    &::placeholder {
      font-size: 1.1rem;
    }
  }
  h2 {
    margin-top: 5rem;
    text-align: center;
  }
}
</style>
