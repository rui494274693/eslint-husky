<template>
  <li
    class="li"
    :style="{ backgroundColor: bgColor }"
    @mouseenter="mouseHandler(true)"
    @mouseleave="mouseHandler(false)"
  >
    <input type="checkbox" v-model="todo.isCheck" />
    <label class="label" for="">{{ todo.title }}</label>
    <button v-show="isShow" @click="deleteHanlde" class="right">删除</button>
  </li>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";
import { Todo } from "../types/todo";
export default defineComponent({
  name: "Item",
  props: {
    todo: {
      type: Object as () => Todo,
      required: true,
    },
    index:{
      type:Number,
       required: true,
    },
    deleteTodo:{
      type:Function,
      required: true,

    }
  },
  setup(props) {
    const isShow = ref(false);
    const bgColor = ref("white");
    const mouseHandler = (e) => {
      isShow.value = e;
      if (e) {
        bgColor.value = "pink";
      } else {
        bgColor.value = "white";
      }
    };
    const deleteHanlde = ()=>{
      console.log(props.index)
      props.deleteTodo(props.index)
    }
    return {
      mouseHandler,
      isShow,
      bgColor,
      deleteHanlde
    };
  },
});
</script>
<style>
.li {
  display: block;
  width: 300px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  padding: 10px;
}
.label {
  margin-left: 10px;
}
.right {
  float: right;
}
</style> 

