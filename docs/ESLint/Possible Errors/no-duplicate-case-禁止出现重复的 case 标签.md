## 禁止重复 case 标签（no-duplicate-case）
```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

如果一个 switch 语句中的 case 子句中出现重复的测试表达式，那么很有可能是某个程序员拷贝了一个 case 子句但忘记了修改测试表达式。

### Rule Details
该规则禁止在 switch 语句中的 case 子句中出现重复的测试表达式。

错误 代码示例：
```js
/*eslint no-duplicate-case: "error"*/

var a = 1,
    one = 1;

switch (a) {
    case 1:
        break;
    case 2:
        break;
    case 1:         // duplicate test expression
        break;
    default:
        break;
}

switch (a) {
    case one:
        break;
    case 2:
        break;
    case one:         // duplicate test expression
        break;
    default:
        break;
}

switch (a) {
    case "1":
        break;
    case "2":
        break;
    case "1":         // duplicate test expression
        break;
    default:
        break;
}
```

正确 代码示例：
```js
/*eslint no-duplicate-case: "error"*/

var a = 1,
    one = 1;

switch (a) {
    case 1:
        break;
    case 2:
        break;
    case 3:
        break;
    default:
        break;
}

switch (a) {
    case one:
        break;
    case 2:
        break;
    case 3:
        break;
    default:
        break;
}

switch (a) {
    case "1":
        break;
    case "2":
        break;
    case "3":
        break;
    default:
        break;
}
```

### Version
该规则在 ESLint 0.17.0 中被引入。
