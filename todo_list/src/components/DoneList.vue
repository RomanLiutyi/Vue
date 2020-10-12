<template>
  <div>
    <div
      class="wrapp"
      v-for="(todo, id) in completedTodos"
      :key="todo.id"
      v-show="showCompletedTodos"
    >
      <div>
        <span
          class="todo__text"
          :class="{ todo__text_isShow: todo.isCompleted }"
        >
          {{ todo.text }}</span
        >
        <input
          class="todo__check"
          type="checkbox"
          @click="unCheckСompleted(id)"
        />
        <button class="todo__text_delete-btn" @click="deleteCompletedTodo(id)">
          <span class="todo__text_delete-btn-text">Delete</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    completedTodos: {
      type: Array,
      required: true,
    },
    todo: {
      type: String,
    },
    showCompletedTodos: {
      type: Boolean,
    },
  },
  methods: {
    unCheckСompleted(id) {
      this.$emit("check-todo-done", id);
    },
    deleteCompletedTodo(id) {
      this.$emit("delete-todo-done", id);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
