## 强制在点号之前或之后换行 (dot-location)

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

JavaScript 允许你在成员表达式中的点操作符之前或之后放置一个换行符。

点操作符前后一致得放置换行符，可以能大大提供代码可读性。
```js
var a = universe.
        galaxy;

var b = universe
       .galaxy;
```

### Rule Details
该规则旨在强制成员表达式中强制换行的一致性。防止既在点号操作之前也在之后使用换行符。

### Options
该规则有个字符串选项：

如果它的值是 "object" (默认)，表达式中的点号操作符应该和对象部分在同一行。

如果它的值是 "property"，表达式中的点号操作符应该和属性在同一行。

```object```
默认选项 "object" 要求点操作符和对象部分放在同一行。

默认选项 "object" 的 错误 代码示例：
```js
/*eslint dot-location: ["error", "object"]*/

var foo = object
.property;
```

默认选项 "object" 的 正确 代码示例：
```js
/*eslint dot-location: ["error", "object"]*/

var foo = object.
property;
var bar = object.property;
```

```property```
选项 "property" 要求点操作符和属性放在同一行。

选项 "property" 的 错误 代码示例：
```js
/*eslint dot-location: ["error", "property"]*/

var foo = object.
property;
```

选项 "property" 的 正确 代码示例：
```js
/*eslint dot-location: ["error", "property"]*/

var foo = object
.property;
var bar = object.property;
```

### When Not To Use It
如果你不关心成员表达式中点操作符前后的换行符的一致性，可以关掉此规则。

### Version
该规则在 ESLint 0.21.0 中被引入
