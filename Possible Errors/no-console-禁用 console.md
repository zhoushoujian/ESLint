## 禁用 console (no-console)
在 JavaScript，虽然console 被设计为在浏览器中执行的，但避免使用 console 的方法被认为是一种最佳实践。这样的消息被认为是用于调试的，因此不适合输出到客户端。通常，在发布到产品之前应该剔除 console 的调用。

```js
console.log("Made it here.");
console.error("That shouldn't have happened.");
```

### Rule Details
该规则禁止调用 console 对象的方法。

错误 代码示例：
```js
/*eslint no-console: "error"*/

console.log("Log a debug level message.");
console.warn("Log a warn level message.");
console.error("Log an error level message.");
```

正确 代码示例：
```js
/*eslint no-console: "error"*/

// custom console
Console.log("Hello world!");
```

### Options
该规则有例外情况，是个对象：

"allow" 是个字符串数组，包含允许使用的console 对象的方法
选项 { "allow": ["warn", "error"] } 的 正确 代码示例：
```js
/*eslint no-console: ["error", { allow: ["warn", "error"] }] */

console.warn("Log a warn level message.");
console.error("Log an error level message.");
```

### When Not To Use It
如果你在使用 Node.js，然后，console 主要用来向用户输出信息，所以不是严格用于调试目的。如果你正在做 Node.js 开发，那么你很可能不想启用此规则。

另一个可能不使用此规则的情况是，如果你想执行控制台调用，而不是控制台重写。例如:

```js
/*eslint no-console: ["error", { allow: ["warn"] }] */
console.error = function (message) {
  throw new Error(message);
};
```

在上面使用 no-console 规则的示例中，ESLint 将报告一个错误。对于上面的例子，你可以禁用该规则:
```js
// eslint-disable-next-line no-console
console.error = function (message) {
  throw new Error(message);
};

// or

console.error = function (message) {  // eslint-disable-line no-console
  throw new Error(message);
};
```

然而，你可能不希望手动添加 eslint-disable-next-line 或 eslint-disable-line。你可以使用 no-restricted-syntax 规则来实现控制台调用仅接收错误的效果:
```js
{
    "rules": {
        "no-console": "off",
        "no-restricted-syntax": [
            "error",
            {
                "selector": "CallExpression[callee.object.name='console'][callee.property.name!=/^(log|warn|error|info|trace)$/]",
                "message": "Unexpected property on console object was called"
            }
        ]
    }
}
```

### Version
该规则在 ESLint 0.0.2 中被引入。
