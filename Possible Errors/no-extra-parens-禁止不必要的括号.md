## 禁止不必要的括号（no-extra-parens）

```命令行中的 --fix 选项可以自动修复一些该规则报告的问题。```

该规则对圆括号的使用做了限制，只有在必要的地方才能使用。

### Rule Details
该规则总是忽略以下情况的额外的圆括号：

RegExp 字面量比如 (/abc/).test(var) 避免与 wrap-regex 规则产生冲突
立即执行函数 (也就是 IIFE) 比如 var x = (function () {})(); 和 ((function foo() {return 1;})()) 避免与 wrap-iife 规则产生冲突
箭头函数参数避免与 arrow-parens 规则产生冲突

### Options
该规则有一个字符串选项：

```"all" (默认)``` 禁止在 任何 表达式周围出现不必要的圆括号
"functions" 只在 函数表达式周围禁止不必要的圆括号
该规则对于 "all" 选项有例外情况，是个对象：

```"conditionalAssign": false ```允许在条件语句的测试表达式中的赋值语句周围出现额外的圆括号
```"returnAssign": false``` 允许在 return 语句中的赋值语句周围出现额外的圆括号
```"nestedBinaryExpressions": false``` 允许在嵌套的二元表达式中出现额外的圆括号
```"ignoreJSX": "none|all|multi-line|single-line```" 允许在 no/所有/多行/单行的JSX 组件周围出现额外的圆括号。 默认为 none。
```"enforceForArrowConditionals": false``` 允许在箭头函数体中的三元表达式周围出现额外的圆括号
all
默认选项 "all" 的 错误 代码示例：
```js
/* eslint no-extra-parens: "error" */

a = (b * c);

(a * b) + c;

for (a in (b, c));

for (a in (b));

for (a of (b));

typeof (a);

(function(){} ? a() : b());
默认选项 "all" 的 正确 代码示例：

/* eslint no-extra-parens: "error" */

(0).toString();

(Object.prototype.toString.call());

({}.toString.call());

(function(){}) ? a() : b();

(/^a$/).test(x);

for (a of (b, c));

for (a of b);

for (a in b, c);

for (a in b);
```

conditionalAssign
选项 "all" 和 { "conditionalAssign": false } 的 正确 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { "conditionalAssign": false }] */

while ((foo = bar())) {}

if ((foo = bar())) {}

do; while ((foo = bar()))

for (;(a = b););
```

returnAssign
选项 "all" 和 { "returnAssign": false } 的 正确 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { "returnAssign": false }] */

function a(b) {
  return (b = 1);
}

function a(b) {
  return b ? (c = d) : (c = e);
}

b => (b = 1);

b => b ? (c = d) : (c = e);
```

nestedBinaryExpressions
选项 "all" 和 { "nestedBinaryExpressions": false } 的 正确 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { "nestedBinaryExpressions": false }] */

x = a || (b && c);
x = a + (b * c);
x = (a * b) / c;
```

ignoreJSX
选项 all 和 { "ignoreJSX": "all" } 正确 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "all" }] */
const Component = (<div />)
const Component = (
    <div
        prop={true}
    />
)
```

选项 all 和 { "ignoreJSX": "multi-line" } 的 错误 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "multi-line" }] */
const Component = (<div />)
const Component = (<div><p /></div>)
```

选项 all 和 { "ignoreJSX": "multi-line" } 的 正确 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "multi-line" }] */
const Component = (
    <div>
        <p />
    </div>
)
const Component = (
    <div
        prop={true}
    />
)
```

选项 all 和 { "ignoreJSX": "single-line" } 的 错误 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "single-line" }] */
const Component = (
    <div>
        <p />
    </div>
)
const Component = (
    <div
        prop={true}
    />
)
```

选项 all 和 { "ignoreJSX": "single-line" } 的 正确 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "single-line" }] */
const Component = (<div />)
const Component = (<div><p /></div>)
```

enforceForArrowConditionals
选项 "all" and { "enforceForArrowConditionals": false } 的 正确 代码示例：
```js
/* eslint no-extra-parens: ["error", "all", { "enforceForArrowConditionals": false }] */

const b = a => 1 ? 2 : 3;
const d = c => (1 ? 2 : 3);
```

functions
选项 "functions" 的 错误 代码示例：
```js
/* eslint no-extra-parens: ["error", "functions"] */

((function foo() {}))();

var y = (function () {return 1;});
```

选项 "functions" 的 正确 代码示例：
```js
/* eslint no-extra-parens: ["error", "functions"] */

(0).toString();

(Object.prototype.toString.call());

({}.toString.call());

(function(){} ? a() : b());

(/^a$/).test(x);

a = (b * c);

(a * b) + c;

typeof (a);
```
### Version
该规则在 ESLint 0.1.4 中被引入。
