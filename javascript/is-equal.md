
# 使用 JSON.stringify()
```js
const areObjectsEqual = (obj1, obj2) => {
  return JSON.stringify(obj1) === JSON.stringify(obj2)
}
```

# 使用 lodash 的 isEqual 函数
```js
import isEqual from 'lodash/isEqual'
 
const areObjectsEqual = (obj1, obj2) => {
  return isEqual(obj1, obj2)
}
```

# 递归比较
```js

const isEqual = (a: any, b: any) => {
  // 处理基本类型和相同引用
  if (a === b) return true

  // 处理NaN
  if (Number.isNaN(a) && Number.isNaN(b)) return true

  // 处理null和undefined
  if (a == null || b == null) return a === b

  // 检查类型是否一致
  if (typeof a !== typeof b) return false

  // 处理日期对象
  if (a instanceof Date && b instanceof Date) {
    return a.getTime() === b.getTime()
  }

  // 处理正则表达式
  if (a instanceof RegExp && b instanceof RegExp) {
    return a.toString() === b.toString()
  }

  // 处理函数
  if (typeof a === 'function' && typeof b === 'function') {
    return a.toString() === b.toString()
  }

  // 处理数组和对象
  if (typeof a === 'object' && typeof b === 'object') {
    const keysA = Object.keys(a)
    const keysB = Object.keys(b)

    if (keysA.length !== keysB.length) return false

    for (let key of keysA) {
      if (!keysB.includes(key)) return false
      if (!isEqual(a[key], b[key])) return false
    }
    return true
  }

  // 其他情况
  return false
}
```