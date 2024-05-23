<template>
  <AppHeader />
  <AppFilters />

  <main class="app-main">
    <AppTodoList :todo-list="todoList" @toggle-todo="toggleTodo" @delete-todo="deleteTodo" />
    <AppAddTodo @add-todo="addTodo" />
  </main>
  <AppFooter />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppAddTodo from "./components/AppAddTodo.vue";
import AppFilters from "./components/AppFilters.vue";
import AppFooter from "./components/AppFooter.vue";
import AppHeader from "./components/AppHeader.vue";
import AppTodoList from "./components/AppTodoList.vue";
import { Todo } from "./types/Todo";

interface State {
    todoList: Todo[]
}

export default defineComponent({
  name: "App",
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter,
  },
  data(): State {
    return {
      todoList: [
        { id: 0, text: "First task", complited: true },
        { id: 1, text: "Second task", complited: false },
        { id: 2, text: "Lorem fsdf sdf ", complited: true },
      ],
    };
  },
  methods: {
    addTodo(todo: Todo) {
      this.todoList.push(todo)
    },
    toggleTodo(id: number) {
      const targetTodo = this.todoList.find((todo) => todo.id === id);

      if (targetTodo) {
        targetTodo.complited = !targetTodo.complited;
      }
    },
    deleteTodo(id: number) {
      this.todoList = this.todoList.filter((todo) => todo.id !== id);
    },
  },
});
</script>

<style></style>
