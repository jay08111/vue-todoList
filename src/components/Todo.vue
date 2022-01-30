<template>
  <section>
    <h1>Todo List</h1>
    <form @submit.prevent="addTodo">
      <div>
        <input type="text" v-model="title" />
        <button>{{ isEditing ? "edit" : "add" }}</button>
      </div>
    </form>
    <article v-for="(todo, index) in todos" :key="todo.id">
      <TodoList
        :todo="todo"
        @deleteTodo="deleteTodo"
        @editTodo="editTodo"
        @toggleClass="toggleClass"
        :index="index"
        v-if="todos.length !== 0"
      />
      <h2 v-else>there is nothing to do...</h2>
    </article>
    <div class="btn__container" v-if="todos.length > 0">
      <button @click="todos = []">all clear</button>
      <button @click="clearTodo">clear complete todo</button>
    </div>
  </section>
</template>

<script lang="ts">
import Vue from "vue";
import TodoList from "./TodoList.vue";
import { Todo } from "../types";
export default Vue.extend({
  components: {
    TodoList,
  },
  data() {
    return {
      title: "" as string,
      todos: [
        { id: 1, title: "Study about vue", completed: false },
        { id: 2, title: "Study Typescript", completed: true },
        { id: 3, title: "Study Vuex", completed: false },
      ] as Todo[],
      isEditing: false as boolean,
      setEditId: null as null | number,
    };
  },
  methods: {
    addTodo() {
      if (!this.title) {
        return;
      } else if (this.title && this.isEditing) {
        this.todos = this.todos.map((item) =>
          item.id === this.setEditId
            ? { id: this.setEditId, title: this.title, completed: false }
            : item
        );
        this.title = "";
        this.isEditing = false;
        this.setEditId = null;
      } else {
        const newTodo: Todo = {
          id: Math.floor(Math.random() * 1000),
          title: this.title,
          completed: false,
        };
        this.todos = [...this.todos, newTodo];

        this.title = "";
      }
    },
    deleteTodo(id: number) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
    editTodo(id: number, title: string) {
      this.setEditId = id;
      this.isEditing = true;
      this.title = title;
    },
    toggleClass(todo: Todo) {
      todo.completed = !todo.completed;
    },
    clearTodo() {
      this.todos = this.todos.filter((item) => item.completed === false);
    },
  },
});
</script>

<style lang="scss" scoped>
section {
  margin-top: 4rem;
  h1 {
    font-size: 2rem;
  }
  div {
    display: flex;
    margin-top: 1.2rem;
    gap: 10px;
    input {
      width: 100%;
      padding: 9px;
      outline: 0;
    }
    button {
      border: 1px solid red;
      background: transparent;
      font-size: 1.2rem;
      padding: 0 10px;
      cursor: pointer;
    }
  }
  .btn__container {
    justify-content: center;
    margin-top: 2rem;
    gap: 20px;
  }
}
</style>
