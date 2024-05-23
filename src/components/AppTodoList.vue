<template>
  <ul class="todo-list">
    <AppTodoItem
        v-for="todo in todoList"
        :key="todo.id"
        :todo="todo"
        @toggleTodo="toggleTodo"
        @deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import AppTodoItem from "./AppTodoItem.vue";
import { Todo } from "@/types/Todo";

export default defineComponent({
  name: "AppTodoList",
  components: {
    AppTodoItem
  },
  props: {
    todoList: {
      type: Array as PropType<Todo[]>
    }
  },
  methods: {
    toggleTodo(id: number) {
      this.$emit('toggleTodo', id)
    },
    deleteTodo(id: number) {
      this.$emit('deleteTodo', id)
    }
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    deleteTodo: (id: number) => Number.isInteger(id)
  }
});
</script>