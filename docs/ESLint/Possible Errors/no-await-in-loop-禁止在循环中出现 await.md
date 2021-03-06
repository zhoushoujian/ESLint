## 禁止在循环中 出现 await (no-await-in-loop)

在迭代器的每个元素上执行运算是个常见的任务。然而，每次运算都执行 await，意味着该程序并没有充分利用 async/await 并行的好处。

通常，代码应该重构为立即创建所有 promise，然后通过 Promise.all() 访问结果。否则，每个后续的操作将不会执行，直到前一个操作执行完毕。

具体来说，以下函数需要重构为：
```js
async function foo(things) {
  const results = [];
  for (const thing of things) {
    // Bad: each loop iteration is delayed until the entire asynchronous operation completes
    results.push(await bar(thing));
  }
  return baz(results);
}
async function foo(things) {
  const results = [];
  for (const thing of things) {
    // Good: all asynchronous operations are immediately started.
    results.push(bar(thing));
  }
  // Now that all the asynchronous operations are running, here we wait until they all complete.
  return baz(await Promise.all(results));
}
```

### Rule Details
该规则禁止在循环体中使用 await。

### Examples
正确 代码示例：
```js
async function foo(things) {
  const results = [];
  for (const thing of things) {
    // Good: all asynchronous operations are immediately started.
    results.push(bar(thing));
  }
  // Now that all the asynchronous operations are running, here we wait until they all complete.
  return baz(await Promise.all(results));
}
```

错误 代码示例：
```js
async function foo(things) {
  const results = [];
  for (const thing of things) {
    // Bad: each loop iteration is delayed until the entire asynchronous operation completes
    results.push(await bar(thing));
  }
  return baz(results);
}
```

### When Not To Use It
在许多情况下，一个循环的迭代实际上并不是相互独立的。例如，一次迭代的输出可能是另一次迭代的输入。或者，循环可以重试不成功的异步操作。或者，循环可用来防止代码发送并行处理过多的请求。在这种情况下，在循环中使用 await 是有意义的，并建议使用标准的 ESLint 禁用注释来禁用规则。

### Version
该规则在 ESLint 3.12.0 中被引入。
