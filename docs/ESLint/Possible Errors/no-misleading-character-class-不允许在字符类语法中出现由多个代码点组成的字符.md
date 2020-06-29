## 不允许在字符类语法中出现由多个代码点组成的字符 (no-misleading-character-class)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

Unicode 包括由多个代码点组成的字符。RegExp 字符类语法 (/[abc]/) 不能处理由多个代码点组成的字符；这些字符将被分解到每个代码点。例如，❇️ 是由 ❇ (U+2747) 和 VARIATION SELECTOR-16 (U+FE0F)。如果这是正则表达式字符类，它将匹配 ❇ (U+2747) 或 VARIATION SELECTOR-16 (U+FE0F)而不是 ❇️。

此规则报告在字符类语法中包含多个代码点字符的正则表达式。此规则将以下字符视为多个代码点字符。

### 组合字符的字符：

组合字符属于 Mc、Me 和 Mn Unicode 通用类别 之一。
```js
/^[Á]$/u.test("Á") //→ false
/^[❇️]$/u.test("❇️") //→ false
```

带有表情符号修饰符的字符：
```js
/^[👶🏻]$/u.test("👶🏻") //→ false
/^[👶🏽]$/u.test("👶🏽") //→ false
```

一组区域指标符号：
```js
/^[🇯🇵]$/u.test("🇯🇵") //→ false
```

ZWJ（Zero Width Joiner）连接的字符：
```js
/^[👨‍👩‍👦]$/u.test("👨‍👩‍👦") //→ false
```

没有 Unicode 标志的 Surrogate pair：
```js
/^[👍]$/.test("👍") //→ false

// Surrogate pair is OK if with u flag.
/^[👍]$/u.test("👍") //→ true
```

### Rule Details
此规则报告在字符类语法中包含多个代码点字符的正则表达式。

错误 代码示例：
```js
/*eslint no-misleading-character-class: error */

/^[Á]$/u
/^[❇️]$/u
/^[👶🏻]$/u
/^[🇯🇵]$/u
/^[👨‍👩‍👦]$/u
/^[👍]$/
```

正确 代码示例：
```js
/*eslint no-misleading-character-class: error */

/^[abc]$/
/^[👍]$/u
```

### When Not To Use It
如果不想检查多个代码点字符的 RegExp 字符类语法，可以关闭此规则。

### Version
该规则在 ESLint 5.3.0 被引入。
