<template>
  <div>
    <input type="text" v-model="inputRef" placeholder="输入值1" />

    <input type="text" v-model="inputReactive.name" placeholder="输入值2" />

    <p>计算属性: {{ computedValue }}</p>

    <p>监听器触发的结果: {{ watchedValues }}</p>
  </div>
</template>
<script lang="ts" setup>
import { ref, reactive, computed, watch, watchEffect } from 'vue'
const inputRef = ref('')

const inputReactive = reactive({
  name: '',
})

// 计算属性
const computedValue = computed(() => {
  return `${inputRef.value} - ${inputReactive.name}`.toUpperCase()
})

// 监听单个ref
watch(inputRef, (newVal, oldVal) => {
  console.log('inputRef改变:', newVal, oldVal)
})

// 监听多个属性（包括ref和reactive）
watch(
  () => [inputRef, inputReactive],
  ([newRefVal, newReactiveVal], [oldRefVal, oldReactiveVal]) => {
    console.log('多个属性改变:', newRefVal, newReactiveVal)
  },
  { deep: true } // 深度监听
)

// 使用watchEffect监听所有相关数据的变化
let watchedValues = ''
watchEffect(() => {
  watchedValues = `监听器触发的结果: ${computedValue.value}`
})
</script>
