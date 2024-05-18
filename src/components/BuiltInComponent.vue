<template>
  <!-- Suspense -->
  <Suspense>
    <template #default>
      <AsyncComponent />
    </template>
    <template #fallback>
      <div>Loading...</div>
    </template>
  </Suspense>

  <!-- Teleport -->
  <!-- 切换Teleport -->
  <button @click="teleportDisabled = !teleportDisabled">
    是否“传送”{{ !teleportDisabled }}
  </button>
  <br />
  <br />
  <button @click="open = true">Open Modal</button>
  <Teleport to="#app" :disabled="teleportDisabled">
    <div v-if="open" class="modal">
      <p>Hello from the modal!</p>
      <button @click="open = false">Close</button>
    </div>
  </Teleport>
</template>

<script lang="ts" setup>
import { ref, defineAsyncComponent, h } from 'vue'

// 定义一个异步组件，模拟加载延迟
const AsyncComponent = defineAsyncComponent(() => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve({
        render() {
          return h('h1', 'Async Component')
        },
      })
    }, 2000) // 模拟2秒延迟
  })
})
const open = ref(false)
const teleportDisabled = ref(false)
</script>

<style scoped>
.modal {
  position: fixed;
  z-index: 999;
  top: 10%;
  left: 50%;
  width: 300px;
  margin-left: -150px;
  background: aqua;
}
</style>
