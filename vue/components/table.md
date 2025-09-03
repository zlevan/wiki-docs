# table 组件

> 基于 `element-plus` 二次封装组件



# 属性

| 属性名            | 说明                                  | 类型     | 默认值                                     |
| ----------------- | ------------------------------------- | -------- | ------------------------------------------ |
| columns           | 表头                                  | Column[] | -                                          |
| filters           | 过滤条件                              | object   | `{}`                                       |
| forms             | 表单                                  | object   | -                                          |
| props             | 查询字段名称配置                      | object   | `{ pageNo:'pageNo', pageSize: 'pageSize'}` |
| notPage           | 是否不分页                            | boolean  | `false`                                    |
| pagination        | 分页配置                              | object   | `{}`                                       |
| showResetButton   | 显示重置按钮（新增/编辑弹窗按钮）     | boolean  | -                                          |
| showSustainButton | 显示继续添加按钮（新增/编辑弹窗按钮） | boolean  | -                                          |
| queryFn           | 查询数据函数                          | Function | -                                          |
| delFn             | 删除列函数                            | Function | -                                          |
| delsFn            | 删除多列函数                          | Function | -                                          |
| addFn             | 新增列函数                            | Function | -                                          |
| editFn            | 编辑列函数                            | Function | -                                          |
| beforeSubmit      | 提交数据前                            | Function | -                                          |
| beforeDelete      | 删除数据前                            | Function | -                                          |
| i18n              | 多语言                                | boolean  | -                                          |
| columnsI18nPrefix | 表格列多语言前缀                      | string   | -                                          |
| formsI18nPrefix   | 表单多语言前缀                        | string   | -                                          |
| formsItemWidth    | 表单单个宽度                          | string   | number                                     | - |
| formsLabelWidth   | 表单 label 宽度                       | string   | -                                          |
| formsInline       | 表单是否为行内样式                    | boolean  | -                                          |
| dialogWidth       | 表单弹窗宽度                          | string   | `3.5rem`                                   |

{ .dense }

# 事件

| 事件名 | 说明 | 类型 |
| ------ | ---- | ---- |
| -      | -    | -    |

{ .dense }

# 插槽

| 插槽名 | 说明 |
| ------ | ---- |
| -      | -    |

{ .dense }

# 暴露方法

| 方法名 | 说明                                   | 类型     |
| ------ | -------------------------------------- | -------- |
| add    | 打开新增弹窗                           | Function |
| edit   | 打开编辑弹窗，参数为当前的列数据 scope | Function |
| del    | 删除 参数为 当前列 id                  | Function |
| dels   | 批量删除                               | Function |
| query  | 表格数据查询                           | Function |


{ .dense }
