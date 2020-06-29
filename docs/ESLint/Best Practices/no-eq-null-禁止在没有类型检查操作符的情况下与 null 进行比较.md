## 禁止与 null 进行比较 (no-eq-null)

与 null 进行比较时不使用类型检测操作符（== 或 !=），可能得意想不到的的结果，因为 null 其本身以及 null 与 undefined 比较结果都为 true。
```js
if (foo == null) {
  bar();
}
```

### Rule Details
该规则旨在通过确保与 null 比较时只等于 null，而不同时等于 undefined， 来减少潜在的 bug 和 意外行为。因此，它也将标记使用 == 和 != 与 null比较的情况。

错误 代码示例：
```js
/*eslint no-eq-null: "error"*/

if (foo == null) {
  bar();
}

while (qux != null) {
  baz();
}
```

正确 代码示例：
```
/*eslint no-eq-null: "error"*/

if (foo === null) {
  bar();
}

while (qux !== null) {
  baz();
}
```

### Version
该规则在 ESLint 0.0.9 中被引入。

