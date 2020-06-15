## 禁用 caller 或 callee (no-caller)

arguments.caller 和 arguments.callee 的使用使一些代码优化变得不可能。在 JavaScript 的新版本中它们已被弃用，同时在 ECMAScript 5 的严格模式下，它们也是被禁用的。

```js
function foo() {
    var callee = arguments.callee;
}
```

### Rule Details
这个规则的目的是通过禁止使用 arguments.caller 和 arguments.callee来阻止使用不推荐的和次优化的代码。因此，当 arguments.caller 和 arguments.callee 被使用时，该规则将会发出警告。

错误 代码示例：
```js
/*eslint no-caller: "error"*/

function foo(n) {
    if (n <= 0) {
        return;
    }

    arguments.callee(n - 1);
}

[1,2,3,4,5].map(function(n) {
    return !(n > 1) ? 1 : arguments.callee(n - 1) * n;
});
```

正确 代码示例：
```js
/*eslint no-caller: "error"*/

function foo(n) {
    if (n <= 0) {
        return;
    }

    foo(n - 1);
}

[1,2,3,4,5].map(function factorial(n) {
    return !(n > 1) ? 1 : factorial(n - 1) * n;
});
```

### Version
该规则在 ESLint 0.0.6 中被引入。

