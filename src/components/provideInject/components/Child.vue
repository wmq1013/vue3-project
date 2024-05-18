<template>
  <h1>通过属性透传获取的color:{{ color }}</h1>
  <el-divider>子组件</el-divider>
  <Grandson v-bind="$attrs" />
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import Grandson from './Grandson.vue';
const props = defineProps({
  color: {
    type: String,
    default: ''
  }
})
</script>