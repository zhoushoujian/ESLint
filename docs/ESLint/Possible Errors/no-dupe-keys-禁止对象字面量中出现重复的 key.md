## 禁止在对象字面量中出现重复的键 (no-dupe-keys)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

在你的应用程序中，如果对象字面量中出现多个属性有同样的键可能会到导致意想不到的情况出现。
```js
var foo = {
    bar: "baz",
    bar: "qux"
};
```

### Rule Details
该规则禁止在对象字面量中出现重复的键。

错误 代码示例：
```js
/*eslint no-dupe-keys: "error"*/

var foo = {
    bar: "baz",
    bar: "qux"
};

var foo = {
    "bar": "baz",
    bar: "qux"
};

var foo = {
    0x1: "baz",
    1: "qux"
};
```

正确 代码示例：
```js
/*eslint no-dupe-keys: "error"*/

var foo = {
    bar: "baz",
    quxx: "qux"
};
```

### Version
该规则在 ESLint 0.0.9 中被引入。

