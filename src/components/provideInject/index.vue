<template>
  count：{{ count }}
  <el-divider>父组件</el-divider>
  <Child :fruit="fruit" :color="color" @getFirstFruit="getFirstFruit" />
</template>
<script lang="ts" setup>
import { ref, provide } from 'vue'
import Child from './components/Child.vue'
provide(/* 注入名 */ 'message', /* 值 */ 'hello!')
const count = ref(0)
provide('count', count)
const userInfo = {
  name: '张三',
  age: 18,
}
provide('userInfo', userInfo)

// 属性透传
const fruit = ref(['apple', 'banana', 'orange'])
const color = ref('red')
// 获取第一个水果
const getFirstFruit = () => {
  console.log(fruit.value[0]);
}
</script>
