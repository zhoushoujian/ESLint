## 要求使用 === 和 !== (eqeqeq)

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

使用类型安全的 === 和 !== 操作符代替 == 和 != 操作符是一个很好的实践。

这样做的原因是，== 和 != 遵循 Abstract Equality Comparison Algorithm 作强制转型。例如，以下语句被认为是 true。

```js
[] == false
[] == ![]
3 == "03"
```

如果它们中的任何一个出现在一个看上去无害的语句中，比如 a == b ，那么实际的问题是很难被发现的。

### Rule Details
该规则旨在消除非类型安全的相等操作符。

错误 代码示例：
```js
/*eslint eqeqeq: "error"*/

if (x == 42) { }

if ("" == text) { }

if (obj.getStuff() != undefined) { }
```

命令行中的 --fix 选项可以自动修复该规则报告的一些问题。该规则唯一问题是只修复操作数之一是 typeof 表达式的或操作数是相同类型的字面量。

### Options
always
选项 "always"（默认）强制在任何情况下都使用 === 和 !== （除非你选择对 null 有更具体的处理[见下文]）。

选项 "always" 的 错误 代码示例：

/*eslint eqeqeq: ["error", "always"]*/
```js
a == b
foo == true
bananas != 1
value == undefined
typeof foo == 'undefined'
'hello' != 'world'
0 == 0
true == true
foo == null
```

选项 "always" 的 正确 代码示例：
```js
/*eslint eqeqeq: ["error", "always"]*/

a === b
foo === true
bananas !== 1
value === undefined
typeof foo === 'undefined'
'hello' !== 'world'
0 === 0
true === true
foo === null
```

该规则可以有第二个参数，是个对象，支持以下属性：

"null": 自定义如何对待 null 字面量。可能的值：
always (默认) - 总是使用 === 或 !==.
never - 从不和 null 一起使用 === 或 !==。
ignore - 不要对 null 应用此规则。
smart
选项 "smart" 除了以下这些情况外，强制使用 === 和 !==：

## 要求使用 === 和 !==
比较 typeof 的值
与 null 进行比较
选项 "always" 的 错误 代码示例：

/*eslint eqeqeq: ["error", "smart"]*/
```js
// comparing two variables requires ===
a == b

// only one side is a literal
foo == true
bananas != 1

// comparing to undefined requires ===
value == undefined
```

选项 "smart" 的 正确 代码示例：
```js
/*eslint eqeqeq: ["error", "smart"]*/

typeof foo == 'undefined'
'hello' != 'world'
0 == 0
true == true
foo == null
allow-null
```
弃用： 使用 “always”，然后传一个 “null” 选项，属性值为 “ignore” 代替。这将告诉 ESLint 除了与 null 字面量进行比较时，总是强制使用绝对相等。

["error", "always", {"null": "ignore"}]

When Not To Use It
如果你不想强制使用相等操作符，可以禁用此规则。

Version
该规则在 ESLint 0.0.2 中被引入。
