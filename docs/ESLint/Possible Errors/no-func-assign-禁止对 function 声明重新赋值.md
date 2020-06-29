## 禁止对 function 声明重新赋值 (no-func-assign)
```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

JavaScript 函数有两种形式：函数声明 function foo() { ... } 或者函数表达式 var foo = function() { ... } 。虽然 JavaScript 解释器可以容忍对函数声明进行覆盖或重新赋值，但通常这是个错误或会导致问题出现。
```js
function foo() {}
foo = bar;
```

### Rule Details
该规则禁止对 function 声明重新赋值。

错误 代码示例：
```js
/*eslint no-func-assign: "error"*/

function foo() {}
foo = bar;

function foo() {
    foo = bar;
}
```

与 JSHint 中对应的规则不同，该规则的 错误 代码示例：
```js
/*eslint no-func-assign: "error"*/

foo = bar;
function foo() {}
```

正确 代码示例：
```js
/*eslint no-func-assign: "error"*/

var foo = function () {}
foo = bar;

function foo(foo) { // `foo` is shadowed.
    foo = bar;
}

function foo() {
    var foo = bar;  // `foo` is shadowed.
}
```

### Version
该规则在 ESLint 0.0.9 中被引入。
