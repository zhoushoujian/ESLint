## 禁止由于 await 或 yield的使用而可能导致出现竞态条件的赋值。(require-atomic-updates)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则```。

在编写异步代码时，可能会产生细微的竞争条件错误。考虑下面的例子：
```js
let totalLength = 0;

async function addLengthOfSinglePage(pageNum) {
  totalLength += await getPageLength(pageNum);
}

Promise.all([addLengthOfSinglePage(1), addLengthOfSinglePage(2)]).then(() => {
  console.log('The combined length of both pages is', totalLength);
});
```

这段代码看起来将对调用 getPageLength(1) 和 getPageLength(2) 的结果进行求和，但实际上，totalLength的最终值仅为两个页面中的一个页面的长度。错误在语句 totalLength += await getPageLength(pageNum); 中。该语句首先读取 totalLength 的初始值，然后调用 getPageLength(pageNum) ，并等待该 Promise 完成。最后，它将 totalLength 的值设置为 waiting getPageLength(pageNum) 和 totalLength 的 初始 值的和。如果在 getPageLength(pageNum) Promise 处于 pending 状态期间，在单独的函数调用中更新了 totalLength 变量，那么更新将会丢失，因为新值被覆盖而不被读取。

解决这个问题的一种方法是确保 totalLength 在更新的同时被读取，如下所示:
```js
async function addLengthOfSinglePage(pageNum) {
  const lengthOfThisPage = await getPageLength(pageNum);
  totalLength += lengthOfThisPage;
}
```

另一个解决方案是完全避免使用可变变量引用：
```js
Promise.all([getPageLength(1), getPageLength(2)]).then(pageLengths => {
  const totalLength = pageLengths.reduce((accumulator, length) => accumulator + length, 0);

  console.log('The combined length of both pages is', totalLength);
});
```

### Rule Details
这条规则的目的是报告满足下列所有条件的给变量或属性赋值的情况：

变量或属性根据其旧值重新分配到新值。
yield 或 await 表达式在读取旧值和设置新值之前中断赋值。
规则不能很容易地验证赋值是否安全（例如，如果赋值的变量是本地的，并且在函数暂停时不能从其他任何地方读取）。
错误 代码示例：
```js
/* eslint require-atomic-updates: error */

let result;
async function foo() {
  result += await somethingElse;

  result = result + await somethingElse;

  result = result + doSomething(await somethingElse);
}

function* bar() {
  result += yield;

  result = result + (yield somethingElse);

  result = result + doSomething(yield somethingElse);
}
```

正确 代码示例：
```js
/* eslint require-atomic-updates: error */

let result;
async function foo() {
  result = await somethingElse + result;

  let tmp = await somethingElse;
  result += tmp;

  let localVariable = 0;
  localVariable += await somethingElse;
}

function* bar() {
  result += yield;

  result = (yield somethingElse) + result;

  result = doSomething(yield somethingElse, result);
}
```

### When Not To Use It
如果你不使用异步或生成器函数，则不需要启用此规则。

### Version
该规则在 ESLint 5.3.0 中被引入。
