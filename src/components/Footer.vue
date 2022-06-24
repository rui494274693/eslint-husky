<template>
  <div>
    <input type="checkbox" v-model="isCheckAll" />
    已选中{{ count }}个，共有{{ list.length }}个
    <button @click="clearAllCompletedTodos">删除已选中</button>
  </div>
</template>
<script lang="ts">
import { Todo } from "../types/todo";
import { computed, defineComponent } from "vue";
export default defineComponent({
  name: "Footer",
  props: {
    list: {
      type: Array as () => Todo[],
      required: true,
    },
    checkAll: {
      type: Function,
      required: true,
    },
    clearAllCompletedTodos: {
      type: Function,
      required: true,
    },
  },
  setup(props) {
    const count = computed(() => {
      return props.list.reduce(
        (pre, todo, index) => pre + (todo.isCheck ? 1 : 0),
        0
      );
    });
    const isCheckAll = computed({
      get() {
        return count.value > 0 && props.list.length === count.value;
      },
      set(val) {
        props.checkAll(val);
      },
    });
    const clearAllCompletedTodos = ()=>{
      props.clearAllCompletedTodos()
    }
    return {
      count,
      isCheckAll,
      clearAllCompletedTodos
    };
  },
});
</script>

