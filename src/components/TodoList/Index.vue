<template>
  <div class="todo-list">
    <!-- ToDo List Header -->
    <div class="todo-list__header">
      <h5 class="todo-list__header-title">Vue To-Do List</h5>
    </div>
    <!-- ./ToDo List Header -->

    <!-- Create Button -->
    <CreateItem @create="onCreate" />
    <!-- ./Create Button -->

    <!-- ToDo List Items -->
    <div class="todo-list__items" v-if="listItems && listItems.length">
      <TodoListItem
        v-for="(item, itemIndex) in listItems"
        :key="item.id"
        :items="listItems"
        :index="itemIndex"
      />
    </div>
    <!-- ./ToDo List Items -->

    <!-- ToDo List Footer -->
    <div class="todo-list__footer" v-if="listItems && listItems.length">
      <b>Items Checked:</b> {{ getCheckedItemsLength }} / {{ getItemsLength }}
    </div>
    <!-- ./ToDo List Footer -->
  </div>
</template>
<script>
// Dynamic Import
const TodoListItem = () => import("./components/TodoListItem/Index.vue");

// Static Import
import CreateItem from "./components/CreateItem/Index.vue";

export default {
  name: "TodoList",
  components: {
    CreateItem,
    TodoListItem,
  },
  data() {
    return {
      listItems: [
        {
          id: 1,
          label: "Vue ToDo List by makaraman",
          is_done: false,
        },
      ],
    };
  },
  methods: {
    onCreate(label) {
      const newItem = {
        id: this.listItems.length + 1,
        label: label,
        is_done: false,
      };
      this.listItems.push(newItem);
    },
  },
  computed: {
    getItemsLength() {
      return this.listItems.length;
    },
    getCheckedItemsLength() {
      return this.listItems.filter((item) => item.is_done).length;
    },
  },
};
</script>
<style lang="scss">
.todo-list {
  background-color: #ffffff;
  width: 100%;
  height: auto;
  border-radius: 0.875rem;
  box-shadow: 0px 3px 9px rgba(0, 0, 0, 0.2);
  &__items {
    border-bottom-left-radius: 0.875rem;
    border-bottom-right-radius: 0.875rem;
    max-height: 450px;
    overflow: auto;
  }
  &__item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    cursor: default;
    padding: 1.2rem;
    transition: 400ms all;
    &:not(:last-child) {
      margin-bottom: 5px;
    }
    &:hover {
      box-shadow: -3px 3px 6px rgba(0, 0, 0, 0.2);
    }
    &--is-done {
      text-decoration: line-through;
    }
    &-transition {
      &-enter,
      &-leave-to {
        transform: scale(0.9);
        opacity: 0;
      }
      &-enter-active,
      &-leave-active {
        transition: transform 300ms ease-in-out, opacity 550ms ease-in-out;
      }
    }
    &-remove {
      display: flex;
      align-items: center;
      cursor: pointer;
      outline: none;
      border-style: unset;
      padding: 0.7rem 1rem;
      border-radius: 0.375rem;
      transition: 400ms all;
      color: #b02727;
      border: 1px solid #b02727;
      background-color: #fff;
      &:hover {
        box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        background-color: #b02727;
        color: #ffffff;
      }
    }
  }
  &__header {
    padding: 1.5rem;
    border-top-right-radius: 0.875rem;
    border-top-left-radius: 0.875rem;
    text-align: center;
    background-color: #fbc02d;
    &-title {
      margin: 0;
      font-weight: bold;
      font-size: 1.4rem;
      color: #000;
    }
  }
  &__create {
    padding: 1.5rem;
    display: flex;
    justify-content: space-between;
    gap: 25px;
    &-input {
      width: 100%;
      border-radius: 0.375rem;
      padding: 10px 15px;
      font-size: 16px;
      border: 1px solid rgb(206, 206, 206);
      outline: none;
      &:focus {
        border-color: #9c27b0;
      }
    }
    &-button {
      display: flex;
      align-items: center;
      cursor: pointer;
      outline: none;
      border-style: unset;
      padding: 0.9rem 2rem;
      border-radius: 0.375rem;
      transition: 400ms all;
      color: #ffffff;
      border-color: #9c27b0;
      background-color: #9e3baf;
      font-weight: bold;
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      font-size: 14px;
      & > i {
        margin-right: 10px;
      }
      &:hover {
        box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        background-color: #9c27b0;
        border-color: #9e3baf;
      }
    }
  }
  &__footer {
    padding: 1.5rem;
    background-color: rgb(228, 228, 228);
    border-bottom-left-radius: 0.875rem;
    border-bottom-right-radius: 0.875rem;
  }
}
</style>
