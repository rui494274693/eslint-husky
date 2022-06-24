<template>
  <div>
    <ul>
     <Item v-for="(li ,index) in list" :todo="li" :key="li.id" :index="index"  :deleteTodo="deleteTodo"></Item>
    </ul>
  </div>
</template>
<script lang="ts">
import Item from "./Item.vue";

import { defineComponent } from "vue";
export default defineComponent({
  name: "List",
  components: {
    Item,
  },
  props: ["list","deleteTodo"],
  setup(props) {
    return {
      
    };
  },
});
</script>

