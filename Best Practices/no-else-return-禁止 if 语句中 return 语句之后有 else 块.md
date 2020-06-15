## 禁止 if 语句中 return 语句之后有 else 块 (no-else-return)

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

如果 if 块中包含了一个 return 语句，else 块就成了多余的了。可以将其内容移至块外。
```js
function foo() {
    if (x) {
        return y;
    } else {
        return z;
    }
}
```

### Rule Details
该规则旨在突出含有 return 语句的 if 语句后的不必要的代码。因此，当else 语句出现在含有 return 语句的 if 语句之后，该规则将发出警告。

### Options
该规则有一个对象选项：

allowElseIf: true (默认) 允许在 return 之后有 else if 块
allowElseIf: false 禁止在 return 之后有 else if 块

`allowElseIf: true`
错误 代码示例：
```js
/*eslint no-else-return: "error"*/

function foo() {
    if (x) {
        return y;
    } else {
        return z;
    }
}

function foo() {
    if (x) {
        return y;
    } else if (z) {
        return w;
    } else {
        return t;
    }
}

function foo() {
    if (x) {
        return y;
    } else {
        var t = "foo";
    }

    return t;
}

function foo() {
    if (error) {
        return 'It failed';
    } else {
        if (loading) {
            return "It's still loading";
        }
    }
}

// Two warnings for nested occurrences
function foo() {
    if (x) {
        if (y) {
            return y;
        } else {
            return x;
        }
    } else {
        return z;
    }
}
```

正确 代码示例：
```js
/*eslint no-else-return: "error"*/

function foo() {
    if (x) {
        return y;
    }

    return z;
}

function foo() {
    if (x) {
        return y;
    } else if (z) {
        var t = "foo";
    } else {
        return w;
    }
}

function foo() {
    if (x) {
        if (z) {
            return y;
        }
    } else {
        return z;
    }
}

function foo() {
    if (error) {
        return 'It failed';
    } else if (loading) {
        return "It's still loading";
    }
}
```

`allowElseIf: false`
错误 代码示例：
```js
/*eslint no-else-return: ["error", {allowElseIf: false}]*/

function foo() {
    if (error) {
        return 'It failed';
    } else if (loading) {
        return "It's still loading";
    }
}
```

正确 代码示例：
```js
/*eslint no-else-return: ["error", {allowElseIf: false}]*/

function foo() {
    if (error) {
        return 'It failed';
    }

    if (loading) {
        return "It's still loading";
    }
}
```

### Version
该规则在 ESLint 0.0.9 中被引入。

