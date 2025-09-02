

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

const isObject = (item) => {
  return (item && typeof item === 'object' && !Array.isArray(item));
}

const areObjectsEqual = (obj1, obj2) => {
  const keys1 = Object.keys(obj1);
  const keys2 = Object.keys(obj2);
  if (keys1.length !== keys2.length) {
    return false;
  }
  for (let key of keys1) {
    const val1 = obj1[key];
    const val2 = obj2[key];
    const areObjects = isObject(val1) && isObject(val2);
    if (
      areObjects && !areObjectsEqual(val1, val2) ||
      !areObjects && val1 !== val2
    ) {
      return false;
    }
  }
  return true;
}
```