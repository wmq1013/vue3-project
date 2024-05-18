<template>
  <button @click="increment">增加</button>
  <p>count：{{ count }}</p>
  <p>computed：{{ doubleCount }}</p>
</template>

<script lang="ts" setup>
import { ref, computed, onMounted } from 'vue'

// 在setup中直接定义响应式变量和计算属性
const count = ref(0)
const doubleCount = computed(() => count.value * 4)

// 直接定义函数
const increment = () => {
  count.value++
}

// 使用onMounted代替mounted钩子
onMounted(() => {
  console.log('mounted', count.value)
})
</script>