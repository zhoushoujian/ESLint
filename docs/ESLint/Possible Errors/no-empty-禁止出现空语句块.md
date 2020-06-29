## 禁止空块语句 (no-empty)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

空语句块，如果不是技术上的错误，通常是由于不完整的重构造成的。这会造成代码阅读上的困惑。

## Rule Details
该规则禁止空语句块出现。该规则忽略包含一个注释的语句块（例如，在 try 语句中，一个空的 catch 或 finally 语句块意味着程序应该继续执行，无论是否出现错误）。

错误 代码示例：
```js
/*eslint no-empty: "error"*/

if (foo) {
}

while (foo) {
}

switch(foo) {
}

try {
    doSomething();
} catch(ex) {

} finally {

}
```

正确 代码示例：
```js
/*eslint no-empty: "error"*/

if (foo) {
    // empty
}

while (foo) {
    /* empty */
}

try {
    doSomething();
} catch (ex) {
    // continue regardless of error
}

try {
    doSomething();
} finally {
    /* continue regardless of error */
}
```

Options
该规则有例外情况，是个对象：

"allowEmptyCatch": true 允许出现空的 catch 子句 (也就是说，不包含注释)
allowEmptyCatch
选项 { "allowEmptyCatch": true } 的 正确 代码示例：

```js
/* eslint no-empty: ["error", { "allowEmptyCatch": true }] */
try {
    doSomething();
} catch (ex) {}

try {
    doSomething();
}
catch (ex) {}
finally {
    /* continue regardless of error */
}
```

### When Not To Use It
如果你打算使用空语句块，那么你可以禁用此规则。

### Version
该规则在 ESLint 0.0.2 中被引入。
