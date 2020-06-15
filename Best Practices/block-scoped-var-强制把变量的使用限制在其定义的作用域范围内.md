## 强制把变量的使用限制在其定义的作用域范围内 (block-scoped-var)

当变量在其被定义的范围之外被使用时，该规则会发出警告。这种解析方式模拟了 C 语言中的块级作用域。

### Rule Details
此规则借鉴其他语言的块级作用域概念，旨在用来减少变量跨作用域使用情况的发生。此规则可帮助语言初学者避免因变量声明提升而产生的 bug。

错误 代码示例：
```js
/*eslint block-scoped-var: "error"*/

function doIf() {
    if (true) {
        var build = true;
    }

    console.log(build);
}

function doIfElse() {
    if (true) {
        var build = true;
    } else {
        var build = false;
    }
}

function doTryCatch() {
    try {
        var build = 1;
    } catch (e) {
        var f = build;
    }
}
```

正确 代码示例：
```js
/*eslint block-scoped-var: "error"*/

function doIf() {
    var build;

    if (true) {
        build = true;
    }

    console.log(build);
}

function doIfElse() {
    var build;

    if (true) {
        build = true;
    } else {
        build = false;
    }
}

function doTryCatch() {
    var build;
    var f;

    try {
        build = 1;
    } catch (e) {
        f = build;
    }
}
```

### Version
该规则在 ESLint 0.1.0 中被引入。

