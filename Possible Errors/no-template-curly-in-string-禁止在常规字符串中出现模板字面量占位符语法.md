## 禁止在常规字符串中出现模板字面量占位符语法 (no-template-curly-in-string)

ECMAScript 6 允许程序员使用模板字面量创建包含变量或表达式的字符串，在两个反引号之间书写表达式比如 ${variable}，而不是使用字符串拼接。在使用模板字面量过程中很容易写错引号，写错成 "${variable}" 而不是在字符串中包含注入的表达式的值。

### Rule Details
该规则旨在对常规字符串中包含看起来像是模板字面量占位符的情况发出警告。当发现一个字符串中包含模板语法占位符(${something}) 使用了 " 或 '，该规则将发出警告。

### Examples
错误 代码示例：
```js
/*eslint no-template-curly-in-string: "error"*/
"Hello ${name}!";
'Hello ${name}!';
"Time: ${12 * 60 * 60 * 1000}";
```

正确 代码示例：
```js
/*eslint no-template-curly-in-string: "error"*/
`Hello ${name}!`;
`Time: ${12 * 60 * 60 * 1000}`;

templateFunction`Hello ${name}`;
```

### When Not To Use It
该规则不应在 ES3/5 环境下使用。

### Version
该规则在 ESLint 3.3.0 中被引入。
