> 数组属性变化监听

# 使用 watch 和 computed
```js

const items = ref([
  { id: 1, name: 'Item 1' }, 
  { id: 2, name: 'Item 2' }
])
 
// 使用 computed 来创建一个响应式的属性，该属性依赖于数组中的特定属性
const nameComputed = computed(() => {
  return items.value.map(item => item.name)
})
 
// 使用 watch 来监听这个计算属性
watch(nameComputed, (newNames, oldNames) => {
  console.log('Names changed:', newNames, oldNames)
}, { deep: true })

// 模拟更新某个项的name属性
const updateName = (id, newName) => {
  items.value = items.value.map(item => item.id === id ? { ...item, name: newName } : item);
}
```

# 使用 watchEffect
```js

const items = ref([
  { id: 1, name: 'Item 1' }, 
  { id: 2, name: 'Item 2' }
])
 
watchEffect(() => {
  const names = items.value.map(item => item.name)
  console.log('Names:', names)
})
```


# 使用 watch 直接监听数组属性变化
> 不推荐直接监听
{ .is-warning }

```js

const items = ref([
  { id: 1, name: 'Item 1' }, 
  { id: 2, name: 'Item 2' }
])

// 直接监听数组的变化（不推荐这样做，除非你知道自己在做什么）
watch(items, (newItems, oldItems) => {
  console.log('Items changed:', newItems, oldItems);
}, { 
	// 使用 deep: true 来深入监听对象内部的变化
  deep: true 
}) 
```



