## 强制getter/setter成对出现在对象中 (accessor-pairs)

创建一个对象，其某个属性只有 setter 而没有对应的 getter，这在 Javascript 中 是个常犯的错误。没有 getter ，你不能读取这个属性，该属性也就不会被用到。（译者注： Javascript 中不一定非要同时指定 getter 和 setter ，原文将此表述为”错误”并非是指语法上的错误）

例如：
```js
// Bad
var o = {
    set a(value) {
        this.val = value;
    }
};

// Good
var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};
```

如果只定义 setter 而没有定义 getter，该规则会发出警告。设置了 getWithoutSet 选项，如果只有 getter 而没有 setter，该规则同样会发出警告。

### Rule Details
该规则强制一种编码风格：对于每个属性，如果定义了setter，也必须定义相应的 getter。

通过激活 getWithoutSet 选项，强制为每个定义了 getter 的属性提供对应的 setter。

### Options
当 setWithoutGet 设置为true时，如果只定义 setter 而不定义 getter，该规则将发出警告（默认为 true）。
当 getWithoutSet 设置为true时，如果只定义 getter 而不定义 setter，该规则将发出警告（默认为 false）。
setWithoutGet
默认选项{ "setWithoutGet": true }的 错误 代码示例：
```js
/*eslint accessor-pairs: "error"*/

var o = {
    set a(value) {
        this.val = value;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    }
});
```

默认选项{ "setWithoutGet": true }的 正确 代码示例：
```js
/*eslint accessor-pairs: "error"*/

var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    },
    get: function() {
        return this.val;
    }
});
```

getWithoutSet
{ "getWithoutSet": true }选项的 错误 代码示例：
```js
/*eslint accessor-pairs: ["error", { "getWithoutSet": true }]*/

var o = {
    set a(value) {
        this.val = value;
    }
};

var o = {
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    }
});

var o = {d: 1};
Object.defineProperty(o, 'c', {
    get: function() {
        return this.val;
    }
});
```

{ "getWithoutSet": true }选项的 正确 代码示例：
```js
/*eslint accessor-pairs: ["error", { "getWithoutSet": true }]*/
var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    },
    get: function() {
        return this.val;
    }
});
```

### When Not To Use It
如果你不关心对象里同时出现 setter 和 getter，你可以关闭这个规则。

### Version
该规则在 ESLint 0.22.0 中被引入。
