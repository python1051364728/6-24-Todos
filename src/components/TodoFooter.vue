<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>数量值{{ shengyu }}</strong></span
    >
    <ul class="filters">
      <li v-for="item in lis" :key="item.id">
        <a
          @click="sele(item)"
          href="javascript:;"
          :class="{ selected: item.isSelected }"
          >{{ item.name }}</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="clearWc">清除已完成</button>
  </footer>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  props: ["list"],
  data() {
    return {
      lis: [
        {
          id: uuidv4(),
          name: "全部",
          isSelected: true,
        },
        {
          id: uuidv4(),
          name: "未完成",
          isSelected: false,
        },
        {
          id: uuidv4(),
          name: "已完成",
          isSelected: false,
        },
      ],
    };
  },
  methods: {
    sele(item) {
      this.lis.forEach((i) => (i.isSelected = i === item));
      this.$emit("seleTodo", item.name);
    },
    clearWc() {
      this.$emit("delDone");
    },
  },
  computed: {
    shengyu() {
      return this.list.reduce((pre, curr) => {
        if (curr.isDone === false) {
          pre += 1;
        }
        return pre;
      }, 0);
    },
  },
};
</script>
