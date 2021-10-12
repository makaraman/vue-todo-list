<template>
  <div id="app" class="app-container">
    <TodoList />
  </div>
</template>

<script>
import TodoList from "./components/TodoList/Index.vue";
export default {
  name: "App",
  components: {
    TodoList,
  },
};
</script>
<style lang="scss">
html,
body {
  margin: 0;
  background-color: #f5f6fb;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.app-container {
  max-width: 40%;
  margin: auto;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
