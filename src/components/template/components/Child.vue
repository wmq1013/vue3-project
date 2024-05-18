<template>
  <p>来自父组件的message： {{ message }}</p>
  <button @click="sendCustomEvent">调用父组件函数</button>
</template>
<script lang="ts" setup>
const emit = defineEmits(['custom-event'])
const props: any = defineProps({
  message: {
    type: String,
    required: true,
    default: () => {},
  },
})
function sendCustomEvent() {
  console.log(props.message)
  emit('custom-event', '这是来自子组件的数据')
}
</script>
