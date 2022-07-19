<template>
  <!-- <section class="todoapp"> -->
  <div>
    <TodoHeader :list="list"></TodoHeader>
    <TodoMain :sele="sele" :list="list" @del-todo="delTodo"></TodoMain>
    <TodoFooter
      :list="list"
      @delDone="clearWC"
      @seleTodo="sele = $event"
    ></TodoFooter>
  </div>
  <!-- </section> -->
</template>

<script>
import TodoHeader from "@/components/TodoHeader";
import TodoMain from "@/components/TodoMain";
import TodoFooter from "@/components/TodoFooter";
export default {
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      sele: "全部",
      list: JSON.parse(localStorage.getItem("TodoList")) || [],
      // list: [
      //   { id: 100, name: "吃饭", isDone: true },
      //   { id: 201, name: "睡觉", isDone: false },
      //   { id: 103, name: "打豆豆", isDone: true },
      // ],
    };
  },
  methods: {
    delTodo(index) {
      this.list.splice(index, 1);
    },
    clearWC() {
      this.list = this.list.filter((item) => !item.isDone);
    },
  },
  watch: {
    list: {
      deep: true,
      immediate: true,
      handler(newList) {
        localStorage.setItem("TodoList", JSON.stringify(newList));
      },
    },
  },
};
</script>
