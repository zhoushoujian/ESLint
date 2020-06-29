## 要求遵循大括号约定 (curly)

命令行中的 --fix 选项可以自动修复一些该规则报告的问题。

当代码块只有一条语句时，JavaScript 允许省略大括号。然而，很多人认为，在块区域前后时刻保留大括号是一种最佳实践，即使他们是可有可无的，因为省略大括号会导致错误，并且降低代码的清晰度。所以以下模式：
```js
if (foo) foo++;
```
能被重写为：
```js
if (foo) {
    foo++;
}
```
然而，依然有人更乐意在有多条执行语句时才使用大括号。

### Rule Details
此规则目的在于，通过确保代码块使用了大括号包裹以避免bug的发生，并且增加代码的清晰度

### Options
all
默认选项 "all" 的 错误 代码示例：
```js
/*eslint curly: "error"*/

if (foo) foo++;

while (bar)
    baz();

if (foo) {
    baz();
} else qux();
```

默认选项 "all" 的 正确 代码示例：
```js
/*eslint curly: "error"*/

if (foo) {
    foo++;
}

while (bar) {
    baz();
}

if (foo) {
    baz();
} else {
    qux();
}
```

multi
默认情况下当 if、else、for、while 或 do 不使用大括号包裹代码时，会给出警告。然而，你可以指定当块中有多条语句时才使用大括号，而当代码块中只有一条语句时只会给出警告。

选项 "multi" 的 错误 代码示例：
```js
/*eslint curly: ["error", "multi"]*/

if (foo) {
    foo++;
}

if (foo) bar();
else {
    foo++;
}

while (true) {
    doSomething();
}

for (var i=0; i < items.length; i++) {
    doSomething();
}
```

选项 "multi" 的 正确 代码示例：
```js
/*eslint curly: ["error", "multi"]*/

if (foo) foo++;

else foo();

while (true) {
    doSomething();
    doSomethingElse();
}
```

multi-line
另外，你可以放宽规则，允许在单行中省略大括号，而if、else if、else、for、while 和 do，在其他使用中依然会强制使用大括号。实现如上定制，配置规则如下：

"multi-line"选项的 错误 代码示例：
```js
/*eslint curly: ["error", "multi-line"]*/

if (foo)
  doSomething();
else
  doSomethingElse();

if (foo) foo(
  bar,
  baz);
  ```
选项 "multi-line" 的 正确 代码示例：
```js
/*eslint curly: ["error", "multi-line"]*/

if (foo) foo++; else doSomething();

if (foo) foo++;
else if (bar) baz()
else doSomething();

do something();
while (foo);

while (foo
  && bar) baz();

if (foo) {
    foo++;
}

if (foo) { foo++; }

while (true) {
    doSomething();
    doSomethingElse();
}
```

multi-or-nest
如果 if、else if、else、for、while 和 do 的代码主体中只包含一条语句，你可以使用另外一个配置来强制省略大括号。同时在其他的情况下，强制使用大括号。

选项 "multi-or-nest" 的 错误 代码示例：
```js
/*eslint curly: ["error", "multi-or-nest"]*/

if (!foo)
    foo = {
        bar: baz,
        qux: foo
    };

while (true)
  if(foo)
      doSomething();
  else
      doSomethingElse();

if (foo) {
    foo++;
}

while (true) {
    doSomething();
}

for (var i = 0; foo; i++) {
    doSomething();
}

if (foo)
    // some comment
    bar();
```

选项 "multi-or-nest" 的 正确 代码示例：
```js
/*eslint curly: ["error", "multi-or-nest"]*/

if (!foo) {
    foo = {
        bar: baz,
        qux: foo
    };
}

while (true) {
  if(foo)
      doSomething();
  else
      doSomethingElse();
}

if (foo)
    foo++;

while (true)
    doSomething();

for (var i = 0; foo; i++)
    doSomething();

if (foo) {
    // some comment
    bar();
}
```

consistent
当在使用任何 multi* 选项时，你可以添加一个参数来强制 if、else if 和 else 中所有的代码块使用或者不使用大括号。

选项 "multi", "consistent" 的 错误 代码示例：
```js
/*eslint curly: ["error", "multi", "consistent"]*/

if (foo) {
    bar();
    baz();
} else
    buz();

if (foo)
    bar();
else if (faa)
    bor();
else {
    other();
    things();
}

if (true)
    foo();
else {
    baz();
}

if (foo) {
    foo++;
}
```
选项 "multi", "consistent" 的 正确 代码示例：
```js
/*eslint curly: ["error", "multi", "consistent"]*/

if (foo) {
    bar();
    baz();
} else {
    buz();
}

if (foo) {
    bar();
} else if (faa) {
    bor();
} else {
    other();
    things();
}

if (true)
    foo();
else
    baz();

if (foo)
    foo++;
```

### When Not To Use It
如果你没有严格约定何时是否使用块语句，你可以放心的禁用此规则。

### Version
该规则在 ESLint 0.0.2 中被引入。
