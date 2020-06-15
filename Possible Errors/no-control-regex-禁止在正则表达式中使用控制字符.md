## 禁止在正则表达式中使用控制字符（no-control-regex）

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

在 ASCII 中，0-31 范围内的控制字符是特殊的、不可见的字符。这些字符很少被用在 JavaScript 字符串中，所以一个正则表达式如果包含这些字符的，很有可能一个错误。

### Rule Details
该规则禁止在正则表达式中出现控制字符。

错误 代码示例：
```js
/*eslint no-control-regex: "error"*/

var pattern1 = /\x1f/;
var pattern2 = new RegExp("\x1f");
```

正确 代码示例：
```js
/*eslint no-control-regex: "error"*/

var pattern1 = /\x20/;
var pattern2 = new RegExp("\x20");
```

### When Not To Use It
如果你需要使用控制字符进行模式匹配，你应该关闭该规则。

### Version
该规则在 ESLint 0.1.0 中被引入
