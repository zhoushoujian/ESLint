## 强制 typeof 表达式与有效的字符串进行比较 (valid-typeof)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

对于绝大多数用例而言，typeof 操作符的结果是以下字符串字面量中的一个："undefined"、"object"、"boolean"、"number"、"string"、"function"、"symbol" 和 "bigint"。把 typeof 操作符的结果与其它字符串进行比较，通常是个书写错误。

### Rule Details
该规则强制 typeof 表达式与有效的字符串进行比较。

### Options
该规则有一个对象选项：

"requireStringLiterals": true 要求 typeof 表达式只与字符串字面量或其它 typeof 表达式 进行比较，禁止与其它值进行比较。
错误 代码示例：
```js
/*eslint valid-typeof: "error"*/

typeof foo === "strnig"
typeof foo == "undefimed"
typeof bar != "nunber"
typeof bar !== "fucntion"
```

正确 代码示例：
```js
/*eslint valid-typeof: "error"*/

typeof foo === "string"
typeof bar == "undefined"
typeof foo === baz
typeof bar === typeof qux
```

选项 { "requireStringLiterals": true } 的 错误 代码示例：
```js
typeof foo === undefined
typeof bar == Object
typeof baz === "strnig"
typeof qux === "some invalid type"
typeof baz === anotherVariable
typeof foo == 5
```

选项 { "requireStringLiterals": true } 的 正确 代码示例：
```js
typeof foo === "undefined"
typeof bar == "object"
typeof baz === "string"
typeof bar === typeof qux
```

### When Not To Use It
如果你将在宿主对象上使用 typeof 操作符，你可以关闭此规则。

### Version
该规则在 ESLint 0.5.0 中被引入。
