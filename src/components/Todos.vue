<template>
  <section class="wrapper">
    <h1>Todos component</h1>
    <input
      type="text"
      class="todo-input"
      placeholder="what needs to be done"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
    <article>
      <div v-for="(todo, index) in todos" :key="index + 1" class="todo-item">
        <p :class="{ done: todo.completed }">
          {{ todo.title }}
        </p>
        <button class="delete__btn" @click="deleteTodo(todo.id)">x</button>
      </div>
    </article>
  </section>
</template>

<script>
export default {
  name: "todos",
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
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: Math.floor(Math.random * 10000),
        title: this.newTodo,
        completed: false,
      });
      this.newTodo = "";
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
  },
  completed: {
    makeId() {
      return Math.floor(Math.random * 10000);
    },
  },
};
</script>

<style lang="scss" scope>
.wrapper {
  margin-top: 5rem;
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
  article {
    margin-top: 15px;
    display: flex;
    gap: 15px;
    flex-direction: column;
    font-size: 1.2rem;
    .todo-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      .done {
        text-decoration: line-through;
      }
      .delete__btn {
        border: none;
        padding: 12px;
        background: transparent;
        font-size: 1.4rem;
        cursor: pointer;
        transition: all 0.3s ease;
        &:hover {
          color: red;
        }
      }
    }
  }
}
</style>
