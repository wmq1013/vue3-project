<template>
  <div>{{ count }}</div>
</template>

<script lang="ts" setup>
// 在Vue 2中，created和beforeCreate是两个常见的生命周期钩子。然而，在Vue 3中，这些钩子已被替换为新的生命周期钩子，以适应Composition API的逻辑。
// 在Vue 3中，这些概念被整合到了setup函数中。setup函数在实例创建之前并且在模板编译之前运行，可以在这里进行数据初始化和逻辑设置。
import {
  ref,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  onRenderTracked,
  onRenderTriggered,
  onErrorCaptured,
} from 'vue'

// 声明一个响应式数据用于演示更新周期
const count = ref(0)

// 调试钩子，追踪响应式数据变化
onRenderTracked(() => {
  console.log('onRenderTracked: 响应式数据被追踪')
})

// 调试钩子，响应式数据追踪开始
onRenderTriggered(() => {
  console.log('onRenderTriggered: 响应式数据追踪开始')
})

// 错误处理，捕获组件内部及子组件的错误
onErrorCaptured((err, instance, info) => {
  console.error('onErrorCaptured: 发生错误', err, info)
})

// 在挂载之前调用，此时DOM还未渲染
onBeforeMount(() => {
  console.log('onBeforeMount: 组件即将挂载，DOM未渲染')
})

// 在挂载完成后立即调用，DOM已经渲染完成
onMounted(() => {
  console.log('onMounted: 组件已挂载，DOM渲染完成')
})

// 在数据更新之前调用，可以在此处进行数据的清理或预处理
onBeforeUpdate(() => {
  console.log('onBeforeUpdate: 数据即将更新，但DOM尚未重新渲染')
})

// 在数据更新导致的DOM更新之后调用
onUpdated(() => {
  console.log('onUpdated: 数据更新完成，DOM已重新渲染')
})

// 在组件卸载之前调用，可以在此做一些清理工作
onBeforeUnmount(() => {
  console.log('onBeforeUnmount: 组件即将卸载')
})

// 在组件完全卸载后调用，此时组件已从DOM中移除
onUnmounted(() => {
  console.log('onUnmounted: 组件已卸载')
})

// 模拟数据更新以触发更新周期钩子
setTimeout(() => {
  count.value++
}, 2000)
</script>

<style scoped>
/* 此处可以添加样式 */
</style>
