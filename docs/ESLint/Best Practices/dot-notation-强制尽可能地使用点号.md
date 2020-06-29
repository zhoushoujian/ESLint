## 强制尽可能地使用点号 (dot-notation)

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

在 JavaScript 中，你可以使用点号 (foo.bar) 或者方括号 (foo["bar"])来访问属性。然而，点号通常是首选，因为它更加易读，简洁，也更适于 JavaScript 压缩。
```js
foo["bar"];
```

### Rule Details
该规则旨在维护代码的一致性，通过鼓励使用点号操作符来提高代码可读性。因此，当遇到不必要的方括号时，该规则将发出警告。

错误 代码示例：
```js
/*eslint dot-notation: "error"*/

var x = foo["bar"];
```

正确 代码示例：
```js
/*eslint dot-notation: "error"*/

var x = foo.bar;

var x = foo[bar];    // Property name is a variable, square-bracket notation required
```

### Options
该规则接受单个选项参数：

为了兼容 ECMAScript 3，设置 allowKeywords 为 false（默认为true），避免对是保留字的属性使用点号。
将 allowPattern设置为一个正则表达式字符串允许匹配这个模式的属性名使用括号。（默认情况下,没有匹配模式）。
```allowKeywords```
选项 { "allowKeywords": false } 的 正确 代码示例：
```js
/*eslint dot-notation: ["error", { "allowKeywords": false }]*/

var foo = { "class": "CS 101" }
var x = foo["class"]; // Property name is a reserved word, square-bracket notation required
```

```allowPattern```
例如，当把准备好的数据发送到外部接口时，经常要求使用包括下划线的属性名。如果启用了 camelcase 规则，这些 snake case 属性将不被允许使用。通过给 dot-notation 规则提供 allowPattern 选项，这些属性就可以使用括号来访问了。

选项 { "allowPattern": "^[a-z]+(_[a-z]+)+$" } 的 正确 代码示例：
```js
/*eslint camelcase: "error"*/
/*eslint dot-notation: ["error", { "allowPattern": "^[a-z]+(_[a-z]+)+$" }]*/

var data = {};
data.foo_bar = 42;

var data = {};
data["fooBar"] = 42;

var data = {};
data["foo_bar"] = 42; // no warning
```

### Version
该规则在 ESLint 0.0.7 中被引入
