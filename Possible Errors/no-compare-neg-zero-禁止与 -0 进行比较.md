## 禁止与 -0 进行比较 (no-compare-neg-zero)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

### Rule Details
该规则对试图与 -0 进行比较的代码发出警告，因为并不会达到预期。也就是说像 x === -0 的代码对于 +0 和 -0 都有效。作者可能想要用 Object.is(x, -0)。

错误 代码示例：
```js
if (x === -0) {
    // doSomething()...
}
```

正确的 代码示例：
```js
if (x === 0) {
    // doSomething()...
}

if (Object.is(x, -0)) {
    // doSomething()...
}
```

### Version
该规则在 ESLint 3.17.0 中被引入。
