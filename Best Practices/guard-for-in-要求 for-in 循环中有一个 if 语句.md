## 需要约束 for-in (guard-for-in)

在使用 for in 遍历对象时，会把从原型链继承来的属性也包括进来。这样会导致意想不到的项出现。
```js
for (key in foo) {
    doSomething(key);
}
```

注意，在某些情况下，对 foo.hasOwnProperty(key) 做简单的检测可能会导致错误出现；查看no-prototype-builtins。

### Rule Details
此规则目的在于，阻止在 for in 遍历过程中，由于不对结果进行筛选而导致意想不到的行为发生。因此，当 for in 循环没有使用 if 语句对结果进行筛选时，该规则将会发出警告。

错误 代码示例：
```js
/*eslint guard-for-in: "error"*/

for (key in foo) {
    doSomething(key);
}
```

正确 代码示例：
```js
/*eslint guard-for-in: "error"*/

for (key in foo) {
    if (Object.prototype.hasOwnProperty.call(foo, key)) {
        doSomething(key);
    }
}

for (key in foo) {
    if ({}.hasOwnProperty.call(foo, key)) {
        doSomething(key);
    }
}
```

### Version
该规则在 ESLint 0.0.6 中被引入。
