<template>
  <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
    <el-tab-pane
      v-for="(item, index) in tabList"
      :label="item.label"
      :key="index"
      :name="item.name">
      <component :is="item.component" />
    </el-tab-pane>
  </el-tabs>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import type { TabsPaneContext } from 'element-plus'
import HelloWorld from './components/HelloWorld.vue'
import Vue3 from './components/Vue3.vue'
import BasicGrammar from './components/BasicGrammar.vue'
const activeName = ref('vue3')
const tabList = [
  { label: 'Vue3 新特性', name: 'vue3', component: Vue3 },
  { label: '基础语法与模板', name: 'basicGrammar', component: BasicGrammar },
  { label: 'Composition API', name: 'composition', component: HelloWorld },
  { label: '组件化开发', name: 'template', component: HelloWorld },
]
const handleClick = (tab: TabsPaneContext, event: Event) => {
  console.log(tab, event)
}
</script>

<style>
.demo-tabs > .el-tabs__content {
  padding: 32px;
  color: #6b778c;
  font-size: 32px;
  font-weight: 600;
}
</style>
