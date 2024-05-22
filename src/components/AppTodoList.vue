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
import { defineComponent } from "vue";
import AppTodoItem from "./AppTodoItem.vue";
import { Todo } from "@/types/Todo"

interface State {
    todoList: Todo[]
}

export default defineComponent({
  name: "AppTodoList",
  components: {
    AppTodoItem
  },
  data(): State {
    return {
        todoList: [
            { id: 0, text: 'First task', complited: true },
            { id: 1, text: 'Second task', complited: false },
            { id: 2, text: 'Lorem fsdf sdf ', complited: true },       
        ]
    }
  },
  methods: {
    toggleTodo(id: number) {
        const targetTodo = this.todoList.find(todo => todo.id === id)

        if (targetTodo) {
            targetTodo.complited = !targetTodo.complited
        }
    },
    deleteTodo(id: number) {
        this.todoList = this.todoList.filter(todo => todo.id !== id)
    }
  }
});
</script>