<template>
  <div class="todo-list__create">
    <input
      class="todo-list__create-input"
      type="text"
      placeholder="Type Something"
      v-model="value"
      @keyup.enter="onCreate"
    />
    <button class="todo-list__create-button" @click="onCreate">
      <i class="fas fa-plus"></i> Add
    </button>
  </div>
</template>
<script>
export default {
  name: "CreateItem",
  data() {
    return {
      value: null,
    };
  },
  methods: {
    onCreate() {
      if (this.value) {
        this.$emit("create", this.value.trim());
        this.value = null;
      } else {
        alert("Type something to add item to list");
      }
    },
  },
};
</script>
