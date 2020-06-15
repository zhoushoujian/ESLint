## 禁止对 catch 子句中的异常重新赋值 (no-ex-assign)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

在 try 语句中的 catch 子句中，如果意外地（或故意地）给异常参数赋值，是不可能引用那个位置的错误的。由于没有 arguments 对象提供额外的方式访问这个异常，对它进行赋值绝对是毁灭性的。

### Rule Details
该规则禁止对 catch 子句中的异常重新赋值。

错误 代码示例：
```js
/*eslint no-ex-assign: "error"*/

try {
    // code
} catch (e) {
    e = 10;
}
```

正确 代码示例：
```js
/*eslint no-ex-assign: "error"*/

try {
    // code
} catch (e) {
    var foo = 10;
}
```

### Version
该规则在 ESLint 0.0.9 中被引入。
