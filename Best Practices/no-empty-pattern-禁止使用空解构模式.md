## 禁止使用空解构模式 (no-empty-pattern)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

当使用解构赋值时，可能创建了一个不起作用的模式。把空的花括号放在嵌入的对象的解构模式右边时，就会产生这种情况，例如：
```js
// doesn't create any variables
var {a: {}} = foo;
```

在以上代码中，没有创建新的变量，因为 a 只是一个辅助位置，而 {} 将包含创建的变量，例如：
```js
// creates variable b
var {a: { b }} = foo;
```

在许多情况下，作者本来打算使用一个默认值，却错写成空对象，例如：
```js
// creates variable a
var {a = {}} = foo;
```

这两种模式直接的区别是微妙的，因为空模式看起来像是一个对象字面量。

### Rule Details
此规则目的在于标记出在解构对象和数组中的任何的空模式，每当遇到一个这样的空模式，该规则就会报告一个问题。

错误 代码示例：
```js
/*eslint no-empty-pattern: "error"*/

var {} = foo;
var [] = foo;
var {a: {}} = foo;
var {a: []} = foo;
function foo({}) {}
function foo([]) {}
function foo({a: {}}) {}
function foo({a: []}) {}
```

正确 代码示例：
```js
/*eslint no-empty-pattern: "error"*/

var {a = {}} = foo;
var {a = []} = foo;
function foo({a = {}}) {}
function foo({a = []}) {}
```

### Version
该规则在 ESLint 1.7.0 中被引入。
