## 禁止使用令人困惑的多行表达式 (no-unexpected-multiline)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

在 JavaScript 中，分号通常是可选的，因为会自动插入分号（ASI)。你可以使用 semi 规则要求或禁止分号。

ASI 的规则是相对简单的：正如 Isaac Schlueter 曾经描述的那样，一个 \n 字符总是一个语句的结尾(像分号一样)，除非下面之一为真：

该语句有一个没有闭合的括号，数组字面量或对象字面量或其他某种方式，不是有效结束一个语句的方式。（比如，以 . 或 , 结尾）
该行是 -- 或 ++（在这种情况下它将减量/增量的下一个标记）
它是个 for()、while()、do、if() 或 else，并且没有 {
下一行以 [、(、+、*、/、-、,、. 或一些其它在单个表达式中两个标记之间的二元操作符。
换行不结束语句，书写错误遗漏了分号，这些异常会导致两个不相干的连续的行被解释为一个表达式。特别是对于一个没有分号的代码风格，读者可能会忽略这些错误。尽管语法上是正确的，代码执行时可能会抛出异常。

### Rule Details
该规则禁止使用令人困惑的多行表达式。

错误 代码示例：
```js
/*eslint no-unexpected-multiline: "error"*/

var foo = bar
(1 || 2).baz();

var hello = 'world'
[1, 2, 3].forEach(addNumber);

let x = function() {}
`hello`

let x = function() {}
x
`hello`

let x = foo
/regex/g.test(bar)
```

正确 代码示例：
```js
/*eslint no-unexpected-multiline: "error"*/

var foo = bar;
(1 || 2).baz();

var foo = bar
;(1 || 2).baz()

var hello = 'world';
[1, 2, 3].forEach(addNumber);

var hello = 'world'
void [1, 2, 3].forEach(addNumber);

let x = function() {};
`hello`

let tag = function() {}
tag `hello`
```

### When Not To Use It
如果你有信心你不会意外地引入这样的代码，你可以关闭此规则。

注意，被认为有问题的模式 不被 semi 规则标记。


### Version
该规则在 ESLint 0.24.0 中被引入。
