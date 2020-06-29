## 禁用不必要的分号 (no-extra-semi)

`配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。`

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

书写错误和对哪里需要使用分号的误解，会导致出现不必要的分号。虽然在技术上不是个错误，但阅读代码时会引起困惑。

### Rule Details

该规则禁用不必要的分号。

错误 代码示例：

```js
/*eslint no-extra-semi: "error"*/

var x = 5;;

function foo() {
  // code
}
```

正确 代码示例：

```js
/*eslint no-extra-semi: "error"*/

var x = 5;

var foo = function () {
  // code
};
```

### When Not To Use It

如果你有意使用额外的分号，那么你可以禁用此规则。

### Version

该规则在 ESLint 0.0.9 中被引入。
