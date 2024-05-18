<template>
  <h3>我是子组件</h3>
  <p>内部计数: {{ count }}</p>
</template>
<script lang="ts" setup>
import { ref, defineExpose } from 'vue'
const count = ref(0)
// 定义一个增加计数的方法
const increment = () => {
  count.value++
}
// 暴露方法和属性给父组件
defineExpose({
  increment,
  count,
})
</script>
