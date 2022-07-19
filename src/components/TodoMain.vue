<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li
      :class="{ completed: item.isDone }"
      v-for="(item, index) in showList"
      :key="item.id"
    >
      <div class="view">
        <input class="toggle" type="checkbox" v-model="item.isDone" />
        <label>{{ item.name }}</label>
        <button @click="delTodo(index)" class="destroy"></button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: ["list", "sele"],
  methods: {
    delTodo(index) {
      this.$emit("del-todo", index);
    },
  },
  computed: {
    showList() {
      switch (this.sele) {
        case "全部":
          return this.list;
        case "未完成":
          return this.list.filter((item) => !item.isDone);
        case "已完成":
          return this.list.filter((item) => item.isDone);
        default:
          return [];
      }
    },
  },
};
</script>
