<template>
  <div>
    输入：<input type="text" v-model="title" />
    <button @click="add">添加</button>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "Header",
  props:{
    addToto:{
      type:Function,
      require:true,
    }
  },
  setup(props) {
    const title = ref("");
    const add = () => {
      let tit:string = title.value;
      if (!tit.trim()) return;
      const addTodo = {
        id:Date.now(),
        title:tit,
        isCheck:false
      }
      props.addToto(addTodo)
      title.value=""
    };
    return {
      title,
      add,
    };
  },
});
</script>