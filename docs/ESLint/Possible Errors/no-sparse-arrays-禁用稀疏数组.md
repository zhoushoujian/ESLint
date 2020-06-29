## 禁用稀疏数组 (no-sparse-arrays)

`配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。`

稀疏数组包括很多空位置，经常是由于在数组字面量中使用多个逗号造成的，例如：

```js
var items = [, ,];
```

在这个例子中，item 数组的 length 为 2，实际上，items[0] 或 items[1]并没有值。数组中只有逗号是有效的，再加上 length 被设置，没有实际的值被设置，这些情况让很多开发者对稀疏数组感到困惑。考虑下面的情况：

```js
var colors = ['red', , 'blue'];
```

在这个例子中，colors 数值的 length 是 3。但是否是开发者想让数组中间出现一个空元素？或者只是一个书写错误？

稀疏数组的定义方式造成了很大的困惑，建议避免使用它们，除非你确定它们在你的代码中很有用。

### Rule Details

该规则禁止使用稀疏数组，也就是逗号之前没有任何元素的数组。该规则不适用于紧随最后一个元素的拖尾逗号的情况。

错误 代码示例：

```js
/*eslint no-sparse-arrays: "error"*/

var items = [,];
var colors = ['red', , 'blue'];
```

正确 代码示例：

```js
/*eslint no-sparse-arrays: "error"*/

var items = [];
var items = new Array(23);

// trailing comma (after the last element) is not a problem
var colors = ['red', 'blue'];
```

### When Not To Use It

如果你想使用稀疏数组，可以关闭此规则。

### Version

该规则在 ESLint 0.4.0 中被引入。
