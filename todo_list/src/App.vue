<template>
  <div id="app">
    <div class="todo">
      <app-title :title="title"></app-title>
      <add-todo @add-todo="addTodo"></add-todo>
      <todo-list
        :todos="todos"
        @check-todo="checkTodo"
        @delete-todo="deleteTodo"
      ></todo-list>
      <!-- <div v-for="(todo, i) in todos" :key="todo.id">
        <p>
          <span class="todo__id">{{ i + 1 }}</span>
          <span
            class="todo__text"
            :class="{ todo__text_isShow: todo.isCompleted }"
          >
            {{ todo.text }}</span
          >
          <input
            class="todo__check"
            type="checkbox"
            v-model="todo.isCompleted"
            @click="checkСompleted(todo, i)"
          />
          <button class="todo__text_delete-btn" @click="deleteTodo(i)">
            <span class="todo__text_delete-btn-text">Delete</span>
          </button>
        </p>
      </div> -->

      <button
        v-show="completedTodos.length"
        @click="showCompletedTodos = !showCompletedTodos"
      >
        <span v-text="!showCompletedTodos ? 'Show' : 'Unshow'"> </span>
        complited todo
      </button>
      <done-list
        :showCompletedTodos="showCompletedTodos"
        :completedTodos="completedTodos"
        @check-todo-done="unCheck"
        @delete-todo-done="deleteCompletedTodo"
      ></done-list>
      <div class="div"></div>
      <!-- <div
        v-for="(todo, i) in completedTodos"
        :key="todo.id"
        v-show="showCompletedTodos"
      >
        <p>
          <span
            class="todo__text"
            :class="{ todo__text_isShow: todo.isCompleted }"
          >
            {{ todo.text }}</span
          >
          <input
            class="todo__check"
            type="checkbox"
            v-model="todo.isCompleted"
            @click="checkСompleted(todo, i)"
          />
          <button class="todo__text_delete-btn" @click="deleteCompletedTodo(i)">
            <span class="todo__text_delete-btn-text">Delete</span>
          </button>
        </p>
      </div> -->
    </div>
  </div>
</template>

<script>
import AppTitle from "./components/Title";
import AddTodo from "./components/AddTodo";
import TodoList from "./components/TodoList";
import DoneList from "./components/DoneList";

export default {
  components: {
    AppTitle,
    AddTodo,
    TodoList,
    DoneList,
  },

  data() {
    return {
      // uid: 0,
      title: "Todo APP",
      // todoText: "we",
      todo: {},
      todos: [],
      completedTodos: [],
      showCompletedTodos: true,
      anyCompleted: false,
      isDone: false,
      id: 0,
    };
  },
  async mounted() {
    const data = await localStorage.getItem("todos");
    data ? (this.todos = JSON.parse(data)) : null;
    const data2 = await localStorage.getItem("completedTodos");
    data2 ? (this.completedTodos = JSON.parse(data2)) : null;
    this.id = await JSON.parse(localStorage.getItem("idCurrent"));
  },
  methods: {
    addTodo(childTitle) {
      this.todoText = childTitle;

      if (this.todoText != "") {
        this.todos.push({
          id: this.id++,
          text: this.todoText,
          isCompleted: this.isDone,
        });

        localStorage.setItem("todos", JSON.stringify(this.todos));
      }
    },

    deleteTodo(index) {
      this.todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },

    deleteCompletedTodo(index) {
      this.completedTodos.splice(index, 1);
      localStorage.setItem(
        "completedTodos",
        JSON.stringify(this.completedTodos)
      );
    },
    checkTodo(i) {
      let todo = this.todos[i];
      todo.isCompleted = !todo.isCompleted;
      this.completedTodos.push(todo);
      this.todos.splice(i, 1);

      localStorage.setItem("todos", JSON.stringify(this.todos));
      localStorage.setItem(
        "completedTodos",
        JSON.stringify(this.completedTodos)
      );
    },
    unCheck(i) {
      let todo = this.completedTodos[i];
      todo.isCompleted = !todo.isCompleted;
      this.todos.push(todo);
      this.completedTodos.splice(i, 1);

      localStorage.setItem("todos", JSON.stringify(this.todos));
      localStorage.setItem(
        "completedTodos",
        JSON.stringify(this.completedTodos)
      );
    },
  },
};
</script>

<style lang="scss" scoped>
#app {
  // font-family: Avenir, Helvetica, Arial, sans-serif;
  // -webkit-font-smoothing: antialiased;
  // -moz-osx-font-smoothing: grayscale;
  // // text-align: center;
  // color: #2c3e50;
  // margin-top: 60px;
  // width: 400px;
  // min-height: 1000px;
  // background: #289;
}
</style>
