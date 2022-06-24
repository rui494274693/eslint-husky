<template>
  <div>
    <button @click="upDate">添加</button>
    <Header :addToto="addToto"></Header>
    <List :list="todos" :deleteTodo="deleteTodo"></List>
    <Footer
      :list="todos"
      :checkAll="checkAll"
      :clearAllCompletedTodos="clearAllCompletedTodos"
    ></Footer>
  </div>
</template>
<script lang="ts">
import { provide, defineComponent, ref, reactive, toRefs } from "vue";
import Header from "./components/Header.vue";
import List from "./components/List.vue";
import Footer from "./components/Footer.vue";
import { Todo } from "./types/todo.ts";

export default defineComponent({
  name: "App",
  components: {
    Header,
    List,
    Footer,
  },
  setup() {
    const res = reactive({
      arr: [{id:1}],
    });
    const arr2 = reactive( []);
    const upDate = () => {
      // res.arr.push({ id: Math.ceil(Math.random()*1000) });
      // if(res.arr.length>=3){
      //   // res.arr=[]
      //   res.arr.length=0
      // }
      // console.log(res.arr)
      // arr2 = []
    };

    //vue3使用proxy，对于对象和数组都不能直接整个赋值 所以数组外包裹一层对象
    const state = reactive<{ todos: Todo[] }>({
      todos: [
        { id: 1, title: "奔驰", isCheck: false },
        { id: 2, title: "宝马", isCheck: true },
        { id: 3, title: "奥迪", isCheck: false },
      ],
    });
    // 所以 最好不要这样写
    let list = reactive<Todo[]>([
      {
        id: 1,
        title: "宝马",
        isCheck: true,
      },
      {
        id: 2,
        title: "奔驰",
        isCheck: true,
      },
    ]);
    const addToto = (todo: Todo) => {
      state.todos.unshift(todo);
    };
    const deleteTodo = (index: number) => {
      state.todos.splice(index, 1);
    };
    const checkAll = (isCheck: boolean) => {
      state.todos.forEach((li) => {
        li.isCheck = isCheck;
      });
    };

    const clearAllCompletedTodos = () => {
      state.todos = state.todos.filter((item) => !item.isCheck);
    };

    return {
      // res,
      ...toRefs(res),
      upDate,
      list,
      arr2,
      ...toRefs(state),
      addToto,
      deleteTodo,
      checkAll,
      clearAllCompletedTodos,
    };
  },
});
</script>