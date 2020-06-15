### 禁用 Alert (no-alert)

JavaScript 的 alert、confirm 和 prompt 被广泛认为是突兀的 UI 元素，应该被一个更合适的自定义的 UI 界面代替。此外, alert 经常被用于调试代码，部署到生产环境之前应该删除。

alert("here!");

### Rule Details
该规则旨在捕获本应移除的调试代码和应该被替换为不那么突兀的 UI 元素。因此，当遇到 alert、prompt 和 confirm 时，该规则将发出警告。

错误 代码示例：
```js
/*eslint no-alert: "error"*/

alert("here!");

confirm("Are you sure?");

prompt("What's your name?", "John Doe");
```

正确 代码示例：
```js
/*eslint no-alert: "error"*/

customAlert("Something happened!");

customConfirm("Are you sure?");

customPrompt("Who are you?");

function foo() {
    var alert = myCustomLib.customAlert;
    alert();
}
```

### Version
该规则在 ESLint 0.0.5 中被引入。
