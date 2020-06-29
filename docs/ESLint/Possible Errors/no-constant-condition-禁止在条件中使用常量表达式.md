## 禁止在条件中使用常量表达式 (no-constant-condition)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

将一个常量表达式（比如，一个字面值）作为一个测试条件可能是个书写错误或者为了触发某个特定的行为。例如，下面的代码看起来像是没有准备好发布的。
```js
if (false) {
    doSomethingUnfinished();
}
```

### Rule Details
该规则禁止在以下语句的条件中出现常量表达式：

if、for、while 或 do...while 语句
?: 三元表达式
错误 代码示例：
```js
/*eslint no-constant-condition: "error"*/

if (false) {
    doSomethingUnfinished();
}

if (void x) {
    doSomethingUnfinished();
}

for (;-2;) {
    doSomethingForever();
}

while (typeof x) {
    doSomethingForever();
}

do {
    doSomethingForever();
} while (x = -1);

var result = 0 ? a : b;
```

正确 代码示例：
```js
/*eslint no-constant-condition: "error"*/

if (x === 0) {
    doSomething();
}

for (;;) {
    doSomethingForever();
}

while (typeof x === "undefined") {
    doSomething();
}

do {
    doSomething();
} while (x);

var result = x !== 0 ? a : b;
```

### Options
```checkLoops```
默认为 true。设置该选项为 false 允许在循环中使用常量表达式。

当 checkLoops 为 false 时的 正确 代码示例：
```js
/*eslint no-constant-condition: ["error", { "checkLoops": false }]*/

while (true) {
    doSomething();
    if (condition()) {
        break;
    }
};

for (;true;) {
    doSomething();
    if (condition()) {
        break;
    }
};

do {
    doSomething();
    if (condition()) {
        break;
    }
} while (true)
```

### Version
该规则在 ESLint 0.4.1 中被引入。
