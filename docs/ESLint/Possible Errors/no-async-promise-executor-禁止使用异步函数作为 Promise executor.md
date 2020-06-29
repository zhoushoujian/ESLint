## 禁止使用异步函数作为 Promise executor (no-async-promise-executor)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

new Promise 构造函数接收一个 executor 函数作为参数，该函数具有 resolve 和 reject 两个参数，可用于控制创建的 Promise 的状态。例如:

```js
const result = new Promise(function executor(resolve, reject) {
  readFile('foo.txt', function(err, result) {
    if (err) {
      reject(err);
    } else {
      resolve(result);
    }
  });
});
```

executor 函数也可以是 async function。然而，这通常是一个错误，原因如下:

如果异步 executor 函数抛出一个错误，这个错误将会丢失，并且不会导致新构造的 Promise 被拒绝。这可能使会调试和处理一些错误变得困难。
如果一个 Promise executor 函数使用了 await，这通常表示实际上没有必要使用 new Promise 构造函数，或者可以减少 new Promise 构造函数的范围。

### Rule Details
此规则旨在禁止使用异步的 Promise executor 函数。

错误 代码示例
```js
const foo = new Promise(async (resolve, reject) => {
  readFile('foo.txt', function(err, result) {
    if (err) {
      reject(err);
    } else {
      resolve(result);
    }
  });
});

const result = new Promise(async (resolve, reject) => {
  resolve(await foo);
});
```

正确 代码示例：
```js
const foo = new Promise((resolve, reject) => {
  readFile('foo.txt', function(err, result) {
    if (err) {
      reject(err);
    } else {
      resolve(result);
    }
  });
});

const result = Promise.resolve(foo);
```

### When Not To Use It
如果你的代码库不支持异步函数语法，则不需要启用此规则。

### Version
该规则在 ESLint 5.3.0 中被引入。
