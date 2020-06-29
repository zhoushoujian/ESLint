## 禁止在 function 定义中出现重复的参数 (no-dupe-args)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

如果在一个函数定义中出现多个同名的参数，后面出现的会覆盖前面出现的参数。重复的名称可能是一个打字错误。

### Rule Details
该规则禁止在函数定义或表达中出现重名参数。该规则并不适用于箭头函数或类方法，因为解析器会报告这样的错误。

如果 ESLint 在严格模式下解析代码，解析器（不是该规则）将报告这样的错误。

错误 代码示例：
```js
/*eslint no-dupe-args: "error"*/

function foo(a, b, a) {
    console.log("value of the second a:", a);
}

var bar = function (a, b, a) {
    console.log("value of the second a:", a);
};
```

正确 代码示例：
```js
/*eslint no-dupe-args: "error"*/

function foo(a, b, c) {
    console.log(a, b, c);
}

var bar = function (a, b, c) {
    console.log(a, b, c);
};
```

### Version
该规则在 ESLint 0.16.0 中被引入。
