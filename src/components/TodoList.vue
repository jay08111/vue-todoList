<template>
  <article>
    <div>
      <div>
        <span>{{ index + 1 }} ) </span>
        <p :class="done" @click="toggleClass(todo)">
          {{ todo.title }}
        </p>
      </div>
      <div class="btn__container">
        <button @click="deleteTodo(todo.id)">x</button>
        <button @click="editTodo(todo.id, todo.title)">edit</button>
      </div>
    </div>
  </article>
</template>

<script lang="ts">
import Vue, { PropType } from "vue";
import { Todo } from "../types";
export default Vue.extend({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true,
    },
    index: {
      type: Number as PropType<number>,
    },
  },
  methods: {
    deleteTodo(id: number) {
      this.$emit("deleteTodo", id);
    },
    editTodo(id: number, title: string) {
      this.$emit("editTodo", id, title);
    },
    toggleClass(todo: Todo) {
      this.$emit("toggleClass", todo);
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
});
</script>

<style lang="scss" scoped>
article {
  margin-top: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 20px;
  div {
    display: flex;
    justify-content: space-between;
    align-items: center;
    div {
      display: flex;
      align-items: center;
      .done {
        text-decoration: line-through;
      }
      p,
      span {
        font-size: 1.7rem;
      }
      p {
        cursor: pointer;
      }
      span {
        margin-right: 10px;
      }
    }
    .btn__container {
      display: flex;
      gap: 15px;
      button {
        border: none;
        background: transparent;
        padding: 10px;
        cursor: pointer;
        font-size: 1.2rem;
        transition: all 0.2s linear;
        &:nth-child(1) {
          font-size: 1.3rem;
          &:hover {
            color: red;
          }
        }
        &:nth-child(2) {
          font-size: 1rem;
          &:hover {
            color: green;
          }
        }
      }
    }
  }
}
</style>
