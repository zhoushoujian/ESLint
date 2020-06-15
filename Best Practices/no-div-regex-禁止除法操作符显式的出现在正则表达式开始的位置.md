## 禁止使用看起来像除法的正则表达式 (no-div-regex)

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

要求正则表达式字面量避开除法操作符。
```js
function bar() { return /=foo/; }
```

### Rule Details
该规则用来消除除法操作符的歧义。

错误 代码示例：
```js
/*eslint no-div-regex: "error"*/

function bar() { return /=foo/; }
```

正确 代码示例：
```js
/*eslint no-div-regex: "error"*/

function bar() { return /[=]foo/; }
```

### Version
该规则在 ESLint 0.1.0 中被引入。
