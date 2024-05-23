<template>
  <section class="add-todo">
    <button v-if='!isFormVisible' @click='showForm' class="add-todo__show-form-button">
      <i class="bi bi-plus-lg"></i>
    </button>
    <form v-if='isFormVisible' class="add-todo__form" @submit.prevent="addTodo">
      <button @click='closeForm' class="close-button" type="button">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model='todoText' class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { Todo } from "@/types/Todo"

interface State {
  isFormVisible: boolean
  todoText: string
}

export default defineComponent({
    name: 'AppAddTodo',
    data(): State {
      return {
        isFormVisible: false,
        todoText: '',
      }
    },
    methods: {
      showForm() {
        this.isFormVisible = true
      },
      closeForm() {
        this.isFormVisible = false
      },
      addTodo() {
        this.$emit('addTodo', {
          id: Date.now(),
          text: this.todoText,
          complited: false
        })
        this.todoText = ''
      }
    },
    emits: {
      addTodo: (todo: Todo) => todo
    }
})
</script>

