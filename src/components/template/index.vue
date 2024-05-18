<template>
  <Child :message="parentMessage" @custom-event="handleCustomEvent" />
  <el-divider>传参与使用</el-divider>

  <ref-template ref="refChild" />
  <button @click="callIncrement">通过ref调用子组件方法</button>
  <el-divider>父组件通过ref控制子组件</el-divider>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import Child from './components/Child.vue'
import RefTemplate from './components/RefTemplate.vue'
const parentMessage = ref<string>('现在是父组件数据')
function handleCustomEvent(data: any) {
  parentMessage.value = data
  console.log('子组件调用函数', data)
}
const refChild = ref<InstanceType<typeof RefTemplate>>()
const childCount = ref<number>(0)
// 定义一个方法来调用子组件暴露的方法
const callIncrement = () => {
  if (refChild.value) {
    refChild.value.increment()
    childCount.value = refChild.value.count
  } else {
    console.warn('子组件尚未挂载')
  }
}
</script>
