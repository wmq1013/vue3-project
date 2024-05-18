<template>
  <div>
    <h3>使用ref的响应式变量</h3>
    <p>{{ count }}</p>
    <button @click="incrementCount">点击增加计数器</button>

    <el-divider />
    <h3>使用reactive的响应式对象</h3>
    <p>{{ user.age }}</p>
    <button @click="changeUserName">点击更改age</button>
    <button @click="coverUserName">覆盖响应式对象</button>

    <h3>使用shallowRef的浅响应式对象</h3>
    <p>{{ shallowUser }}</p>
    <button @click="changeShallowUserName">尝试更改name</button>

    <el-divider />
    <h3>使用readonly的只读响应式对象</h3>
    <p>原对象：{{ originalUser.age }}</p>
    <p>只读对象：{{ readonlyUser.age }}</p>
    <button @click="changeReadonlyAge">更改只读对象</button>
    <button @click="changeOriginalUser">更改原对象</button>

    <el-divider />
    <h3>使用toRefs将复杂用户对象的属性转换为ref</h3>
    <p>name：{{ name }}</p>
    <p>age：{{ age }}</p>
    <p>address：{{ address }}</p>
    <button @click="changeComplexUser">更改toRefs后的值</button>
  </div>
</template>

<script lang="ts" setup>
import { ref, reactive, shallowRef, readonly, toRefs } from 'vue'

// 使用ref创建一个响应式的基本类型变量
const count = ref(0)
function incrementCount() {
  count.value++
}

// 使用reactive创建一个响应式的对象
let user = reactive({ age: 18 })
function changeUserName() {
  user.age = count.value
  console.log(user)
}
// 覆盖
const coverUserName = () => {
  user = { age: 24 }
  console.log(user)
}

// 创建浅响应式的对象，仅最外层属性响应式
const shallowUser = shallowRef({ name: '浅响应式用户', age: 18 })
function changeShallowUserName() {
  shallowUser.value.name = '新名称' // 这里不会更新视图
  shallowUser.value = { name: '另一个名称', age: 20 } // 这里会更新视图，因为替换整个对象
}

// 创建只读的响应式对象，对象本身不可修改
const originalUser = reactive({ age: 25 })
const readonlyUser = readonly(originalUser)
function changeReadonlyAge() {
  readonlyUser.age = 30 // 这里不会更新视图，因为对象是只读的
}
function changeOriginalUser() {
  originalUser.age = 30 // 这里会更新视图，因为对象是响应式的，且只读对象的值也会变化
}
// 假设有更复杂的用户对象
let complexUser = reactive({
  name: '复杂用户',
  age: 35,
  address: {
    street: '456 Elm St',
    city: 'Othertown',
  },
})

// 使用toRefs将复杂用户对象的属性转换为ref，以便独立操作
const { name, age, address } = toRefs(complexUser)
function changeComplexUser() {
  name.value = '新名称' + age.value
  age.value++
  address.value.city = 'NewCity' + age.value
}
</script>
