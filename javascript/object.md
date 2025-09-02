

# 排序键
```js
const sortObjKey = (obj) => {
  return Object.keys(obj)
    .sort()
    .reduce((acc, key) => {
      acc[key] = obj[key]
      return acc
    }, {})
}

const unsorted = {
  b: "foo",
  c: "bar",
  a: "baz",
}

sortObjKey(unsorted) // {a: 'baz', b: 'foo', c: 'bar'}
```