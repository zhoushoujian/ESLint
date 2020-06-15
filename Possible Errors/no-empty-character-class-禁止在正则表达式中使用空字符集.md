## 禁止在正则表达式中出现空字符集 (no-empty-character-class)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

在正则表达式中空字符集不能匹配任何字符，它们可能是打字错误。
```js
var foo = /^abc[]/;
```

### Rule Details
该规则禁止在正则表达式中出现空字符集。

错误 代码示例：
```js
/*eslint no-empty-character-class: "error"*/

/^abc[]/.test("abcdefg"); // false
"abcdefg".match(/^abc[]/); // null
```

正确 代码示例：
```js
/*eslint no-empty-character-class: "error"*/

/^abc/.test("abcdefg"); // true
"abcdefg".match(/^abc/); // ["abc"]

/^abc[a-z]/.test("abcdefg"); // true
"abcdefg".match(/^abc[a-z]/); // ["abcd"]
```
Known Limitations
该规则不会报告 RegExp 构造函数的字符串参数中空字符集的使用情况。

当该规则报告了正确的代码时，漏报的示例：
```js
/*eslint no-empty-character-class: "error"*/

var abcNeverMatches = new RegExp("^abc[]");
```

### Version
该规则在 ESLint 0.22.0 中被引入。
