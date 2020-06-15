## 禁用 debugger (no-debugger)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

debugger 语句用于告诉 JavaScript 执行环境停止执行并在代码的当前位置启动调试器。随着现代调试和开发工具的出现，使用调试器已不是最佳实践。产品代码不应该包含 debugger，因为它会导致浏览器停止执行代码并打开一个适当的调试器。

### Rule Details
该规则禁止 debugger 语句。

错误 代码示例：
```js
/*eslint no-debugger: "error"*/

function isTruthy(x) {
    debugger;
    return Boolean(x);
}
```

正确 代码示例：
```js
/*eslint no-debugger: "error"*/

function isTruthy(x) {
    return Boolean(x); // set a breakpoint at this line
}
```

### When Not To Use It
如果你的代码在很大程度上仍处于开发阶段，不想担心剥离 debugger 语句，那么就关闭此规则。通常在部署测试代码之前，你会想重新开启此规则。

### Version
该规则在 ESLint 0.0.2 中被引入。
