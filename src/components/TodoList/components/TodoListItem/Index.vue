<template>
  <transition appear name="todo-list__item-transition" mode="out-in">
    <div class="todo-list__item">
      <div class="todo-list__item-name">
        <input
          type="checkbox"
          :id="item.id"
          @input="toggleIsDone"
          :value="isDone"
        />
        <label :for="item.id" :class="{ 'todo-list__item--is-done': isDone }">
          {{ item.label }}
        </label>
      </div>
      <button class="todo-list__item-remove" @click="onRemove">
        <i class="fas fa-trash"></i>
      </button>
    </div>
  </transition>
</template>
<script>
export default {
  name: "TodoListItem",
  props: {
    items: {
      default: () => [],
    },
    index: {
      default: 0,
    },
  },
  methods: {
    /**
     * Toggle is_done status of item
     */
    toggleIsDone(e) {
      this.item.is_done = e.target.checked;
    },
    onRemove() {
      if (window.confirm("Do you really want to remove item?")) {
        this.items.splice(this.index, 1);
      }
    },
  },
  computed: {
    /**
     * Item itself from items array
     * @return object
     */
    item() {
      return this.items[this.index];
    },
    /**
     * Check list item is done
     * @return bool
     */
    isDone() {
      return this.item.is_done ? true : false;
    },
  },
};
</script>
