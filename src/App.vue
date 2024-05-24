<template>
  <AppHeader />
  <AppFilters :active-filter="activeFilter" @set-filter="setFilter"/>

  <main class="app-main">
    <AppTodoList :todo-list="filteredTodos" @toggle-todo="toggleTodo" @delete-todo="deleteTodo" />
    <AppAddTodo @add-todo="addTodo" />
  </main>
  <AppFooter :stats="stats" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppAddTodo from "./components/AppAddTodo.vue";
import AppFilters from "./components/AppFilters.vue";
import AppFooter, { Stats } from "./components/AppFooter.vue";
import AppHeader from "./components/AppHeader.vue";
import AppTodoList from "./components/AppTodoList.vue";
import { Todo } from "./types/Todo";
import { Filter } from "@/types/Filter";

interface State {
    todoList: Todo[]
    activeFilter: Filter
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
      activeFilter: 'All'
    };
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.activeTodos
        case 'Done':
          return this.complitedTodos
        case 'All':
        default:
          return this.todoList

      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.complitedTodos.length
      }
    },
    activeTodos(): Todo[] {
      return this.todoList.filter(todo => !todo.complited)
    },
    complitedTodos(): Todo[] {
      return this.todoList.filter(todo => todo.complited)
    }
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
    setFilter(filter: Filter) {
      this.activeFilter = filter
    }
  },
});
</script>

<style></style>
