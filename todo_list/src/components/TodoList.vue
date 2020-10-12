<template>
  <div>
    <div v-for="(todo, id) in todos" :key="todo.id">
      <div class="wrapp">
        <div class="list">
          <span class="todo__id">{{ id + 1 }}</span>
          <span
            class="todo__text"
            :class="{ todo__text_isShow: todo.isCompleted }"
          >
            {{ todo.text }}</span
          >
        </div>
        <div class="control">
          <input type="checkbox" class="todo__check" @click="checkTodo(id)" />
          <button class="todo__text_delete-btn" @click="deleteTodo(id)">
            <span class="todo__text_delete-btn-text">Delete</span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true,
    },
    todo: {
      type: String,
    },
  },
  methods: {
    checkTodo(id) {
      this.$emit("check-todo", id);
    },
    deleteTodo(id) {
      this.$emit("delete-todo", id);
    },
  },
};
</script>
<style lang="scss">
.wrapp {
  display: flex;
  justify-content: space-between;
}
.todo {
  width: 300px;
  min-height: 500px;
  background: #0c6;
  padding: 30px;
  outline: 1px solid #59f;

  &__id {
    font-size: 25px;
    color: red;
    font-weight: bold;
  }
  &__text {
    font-size: 20px;
    color: #f70;

    &_isShow {
      color: #ccc;
      text-decoration: line-through;
    }
  }
  &__check {
    display: inline-block;
    margin-left: 10px;
  }
}
</style>