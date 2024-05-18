<template>
  <div>
    <p>count: {{ count }}</p>
    <p>message: {{ message }}</p>
    <p>userInfo: {{ userInfo }}</p>
    <p>messageDemo: {{ messageDemo }}</p>
    <button @click="count++">count增加</button>
    <h1>通过属性透传获取的fruit数组：{{ fruit }}</h1>
    <h1>通过属性透传获取的color数据：{{ color }}</h1>
    <button @click="getFruit">获取第一个fruit</button>
    <el-divider>孙组件</el-divider>
  </div>
</template>
<script lang="ts" setup>
import { ref, inject } from 'vue'

const count = inject('count')
// 如果没有祖先组件提供 "message"
// `value` 会是 "这是默认值"
const message = inject('messageDemo', '这是默认值')

// 定义一个函数来注入多个属性
function injectMultiple(defaults) {
  return Object.fromEntries(
    Object.entries(defaults).map(([key, defaultValue]) => [
      key,
      inject(key, defaultValue),
    ])
  )
}
// 一次注入 "userInfo" 和 "messageDemo"
const { userInfo, messageDemo } = injectMultiple({
  userInfo: 0,
  messageDemo: '这是默认值',
})

const props = defineProps({
  fruit: {
    type: Array,
    default: [],
  },
  color: {
    type: String,
    default: 'red',
  },
})
const emit = defineEmits(['getFirstFruit'])
const firstFruit = ref<any>('')
const getFruit = () => {
  emit('getFirstFruit')
}
</script>
