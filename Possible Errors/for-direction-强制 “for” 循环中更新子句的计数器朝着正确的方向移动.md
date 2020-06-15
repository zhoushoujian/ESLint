## 强制 “for” 循环中更新子句的计数器朝着正确的方向移动 (for-direction)

```(推荐) 配置文件中的 "extends": "eslint:recommended" 属性启用此规则。```

### Rule Details
如果一个 for 循环的停止条件永远无法到达，比如，计数器在错误的方向上移动，将陷入无限循环。当存在这样的无限循环时，惯例是改用 while 循环。更典型的是，无限循环是个 bug。

错误 代码示例：
```js
/*eslint for-direction: "error"*/
for (var i = 0; i < 10; i--) {
}

for (var i = 10; i >= 0; i++) {
}
```

正确 代码示例：
```js
/*eslint for-direction: "error"*/
for (var i = 0; i < 10; i++) {
}
```

### Version
该规则在 ESLint 4.0.0-beta.0 中被引入。
