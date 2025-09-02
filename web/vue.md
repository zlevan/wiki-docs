
- [VUE *版本差异* ](/web/vue-version)
{.links-list}
---
> vue3.0

# 日常开发问题
1. 组件 `props` 传递的另一个组件需要用 `markRaw`[^1] 函数处理,否则会异常；
1. 当遇到需要`监听数组`中某个属性变化时而又不想监听整个数组的变化，可使用 `watch` 和 `computed` 的组合使用，或者使用 `watchEfect`，[示例地址](/web/vue-watch-array) ；


  
[^1]: 用于标记一个对象或组件，使其不被 `Vue` 的响应式系统处理。换句话说，被 `markRaw` 标记的对象或组件不会被 Vue 转换为响应式对象，也不会被追踪其属性的变化
 