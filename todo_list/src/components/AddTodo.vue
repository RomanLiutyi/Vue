<template>
  <div>
    <form @submit.prevent="onAddTodo()" class="form">
      <input type="text" placeholder="Add Todo..." v-model="title" />
      <input  type="submit" class="btn" />
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return { title: "" };
  },
  methods: {
    onAddTodo() {
      // console.log(e);
      this.$emit("add-todo", this.title);
      this.title = "";
    },
  },
};
</script>

<style scoped>
.form {
  display: flex;
  justify-content: space-between;
}

</style>