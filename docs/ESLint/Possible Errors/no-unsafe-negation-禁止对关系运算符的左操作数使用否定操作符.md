## 禁止对关系运算符的左操作数使用否定操作符 (no-unsafe-negation)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

开发人员可能会把 -(a + b) 写错成 -a + b 来表示一个负数，也可能会把 !(key in object) 错写成 !key in object 来测试一个键是否在对象中。类似的情况也有 !obj instanceof Ctor。

### Rule Details
该规则禁止对关系运算符的左操作数使用否定操作符。

### 关系运算符有：

in 运算符.
instanceof 运算符.
错误 代码示例：
```js
/*eslint no-unsafe-negation: "error"*/

if (!key in object) {
    // operator precedence makes it equivalent to (!key) in object
    // and type conversion makes it equivalent to (key ? "false" : "true") in object
}

if (!obj instanceof Ctor) {
    // operator precedence makes it equivalent to (!obj) instanceof Ctor
    // and it equivalent to always false since boolean values are not objects.
}
```

正确 代码示例：
```js
/*eslint no-unsafe-negation: "error"*/

if (!(key in object)) {
    // key is not in object
}

if (!(obj instanceof Ctor)) {
    // obj is not an instance of Ctor
}

if(("" + !key) in object) {
    // make operator precedence and type conversion explicit
    // in a rare situation when that is the intended meaning
}
```

### When Not To Use It
如果你不想收到不安全的逻辑否，可以不使用此规则。

### Version
该规则在 ESLint 3.3.0 中被引入。
