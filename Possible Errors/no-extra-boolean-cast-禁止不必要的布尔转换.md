## 禁止不必要的布尔类型转换（no-extra-boolean-cast）
```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

在上下文中比如 if 语句的测试表达式的结果已经被强制转化成了一个布尔值，再通过双重否定（!!）或 Boolean 转化是不必要的。例如，这些 if 语句是等价的：
```js
if (!!foo) {
    // ...
}

if (Boolean(foo)) {
    // ...
}

if (foo) {
    // ...
}
```

### Rule Details
该规则禁止不必要的布尔类型转换。

错误 代码示例：
```js
/*eslint no-extra-boolean-cast: "error"*/

var foo = !!!bar;

var foo = !!bar ? baz : bat;

var foo = Boolean(!!bar);

var foo = new Boolean(!!bar);

if (!!foo) {
    // ...
}

if (Boolean(foo)) {
    // ...
}

while (!!foo) {
    // ...
}

do {
    // ...
} while (Boolean(foo));

for (; !!foo; ) {
    // ...
}
```
正确 代码示例：
```js
/*eslint no-extra-boolean-cast: "error"*/

var foo = !!bar;
var foo = Boolean(bar);

function foo() {
    return !!bar;
}

var foo = bar ? !!baz : !!bat;
```

### Version
该规则在 ESLint 0.4.0 中被引入。

