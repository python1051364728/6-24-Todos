<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
    <label for="toggle-all"></label>
    <input
      v-model="inTodo"
      @keydown.enter="addTodo"
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
    />
  </header>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  props: ["list"],
  data() {
    return {
      inTodo: "",
    };
  },
  methods: {
    addTodo() {
      if (this.inTodo.trim() === "") {
        alert("请输入正确的任务名");
        this.inTodo = "";
        return;
      }
      const todo = {
        id: uuidv4(),
        name: this.inTodo,
        isDone: false,
      };
      this.list.push(todo);
      this.inTodo = "";
    },
  },
  computed: {
    isAll: {
      get() {
        return this.list.every((item) => item.isDone);
      },
      set(newSelected) {
        return this.list.forEach((item) => (item.isDone = newSelected));
      },
    },
  },
};
</script>
