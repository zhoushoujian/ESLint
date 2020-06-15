## 禁止在 return、throw、continue 和 break 语句后出现不可达代码 (no-unreachable)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

因为 return、throw、continue 和 break 语句无条件地退出代码块，其之后的任何语句都不会被执行。不可达语句通常是个错误。
```js
function fn() {
    x = 1;
    return x;
    x = 3; // this will never execute
}
```

### Rule Details
该规则禁止在 return、throw、continue 和 break 语句后出现不可达代码。

错误 代码示例：
```js
/*eslint no-unreachable: "error"*/

function foo() {
    return true;
    console.log("done");
}

function bar() {
    throw new Error("Oops!");
    console.log("done");
}

while(value) {
    break;
    console.log("done");
}

throw new Error("Oops!");
console.log("done");

function baz() {
    if (Math.random() < 0.5) {
        return;
    } else {
        throw new Error();
    }
    console.log("done");
}

for (;;) {}
console.log("done");
```

正确 代码示例，因为 JavaScript 函数和变量提升：
```js
/*eslint no-unreachable: "error"*/

function foo() {
    return bar();
    function bar() {
        return 1;
    }
}

function bar() {
    return x;
    var x;
}

switch (foo) {
    case 1:
        break;
        var x;
}
```

### Version
该规则在 ESLint 0.0.6 中被引入。
