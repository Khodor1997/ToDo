<template>
  <AppHeader/>
  <AppFilters/>

  <main class="app-main">
    <AppTodoList/>  
    <AppAddTodo/>
  </main>
  <AppFooter/>

</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppAddTodo from "./components/AppAddTodo.vue";
import AppFilters from "./components/AppFilters.vue";
import AppFooter from "./components/AppFooter.vue";
import AppHeader from "./components/AppHeader.vue";
import AppTodoList from "./components/AppTodoList.vue"

export default defineComponent({
  name: "App",
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
  },
});
</script>

<style></style>
