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
    <article>
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
    </article>
    <button class="btn deleteAll" @click="deleteAll">delete all</button>
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
      isEditing: false,
      editId: null,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo) {
        const newTodo = {
          id: Math.floor(Math.random() * 10000),
          title: this.newTodo,
          completed: false,
        };
        this.todos = [...this.todos, newTodo];
        this.newTodo = "";
      }
      if (this.isEditing) {
        this.todos = this.todos.map((item) =>
          item.id === this.editId
            ? {
                id: Math.floor(Math.random() * 10000),
                title: this.newTodo,
                completed: false,
              }
            : item
        );
        this.isEditing = false;
        this.newTodo = "";
        this.editId = null;
      }
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
    toggleTodo() {
      this.todos.completed = !this.todos.completed;
      console.log(this.todos.completed);
    },
    deleteAll() {
      this.todos = [];
    },
    editTodo($event, id) {
      this.isEditing = true;
      this.editId = id;
      this.newTodo = $event.target.value;
      console.log(this.isEditing, this.editId, this.newTodo);
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
      .done {
        text-decoration: line-through;
      }
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
