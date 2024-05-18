<template>
  <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
    <el-tab-pane
      v-for="(item, index) in tabList"
      :label="item.label"
      :key="index"
      :name="item.name">
      <component :is="item.component" v-if="item.name === activeName" />
    </el-tab-pane>
  </el-tabs>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import type { TabsPaneContext } from 'element-plus'
import Vue3 from './components/Vue3.vue'
import BuiltInComponent from './components/BuiltInComponent.vue'
import BasicGrammar from './components/BasicGrammar.vue'
import ComputedWatch from './components/ComputedWatch.vue'
import LifecycleHooks from './components/LifecycleHooks.vue'
import ProvideInject from './components/provideInject/index.vue'
import Template from './components/template/index.vue'
const activeName = ref('vue3')
const tabList = [
  { label: 'Vue3 新特性', name: 'vue3', component: Vue3 },
  {
    label: '新内置组件',
    name: 'BuiltInComponent',
    component: BuiltInComponent,
  },
  { label: '基础语法与模板', name: 'basicGrammar', component: BasicGrammar },
  {
    label: '计算属性、监听',
    name: 'computedWatch',
    component: ComputedWatch,
  },
  { label: '生命周期', name: 'lifecycleHooks', component: LifecycleHooks },
  { label: '依赖注入', name: 'provideInject', component: ProvideInject },
  { label: '组件化开发', name: 'template', component: Template },
]
const handleClick = (tab: TabsPaneContext, event: Event) => {}
</script>

<style>
.demo-tabs > .el-tabs__content {
  padding: 16px;
  color: #6b778c;
  font-size: 16px;
  font-weight: 600;
}
</style>
