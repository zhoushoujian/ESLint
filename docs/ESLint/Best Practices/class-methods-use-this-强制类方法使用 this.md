## 强制类方法使用 this (class-methods-use-this)

如果一个类方法不使用 this，可以安全的做为静态函数出现。

可以有一个不使用 this 的类方法，比如：
```js
class A {
    constructor() {
        this.a = "hi";
    }

    print() {
        console.log(this.a);
    }

    sayHi() {
        console.log("hi");
    }
}

let a = new A();
a.sayHi(); // => "hi"
```

在上面的例子中，sayHi 方法没有使用 this，因此我们可以把它改造成静态方法：
```js
class A {
    constructor() {
        this.a = "hi";
    }

    print() {
        console.log(this.a);
    }

    static sayHi() {
        console.log("hi");
    }
}

A.sayHi(); // => "hi"
```

还要注意，在上面的例子中，在类实例上调用函数 (let a = new A(); a.sayHi();) 改为在类自身上调用 (A.sayHi();)。

### Rule Details
该规则只在标记没有使用 this 的类方法。

错误 代码示例：
```js
/*eslint class-methods-use-this: "error"*/
/*eslint-env es6*/

class A {
    foo() {
        console.log("Hello World");     /*error Expected 'this' to be used by class method 'foo'.*/
    }
}
```

正确 代码示例：
```js
/*eslint class-methods-use-this: "error"*/
/*eslint-env es6*/
class A {
    foo() {
        this.bar = "Hello World"; // OK, this is used
    }
}

class A {
    constructor() {
        // OK. constructor is exempt
    }
}

class A {
    static foo() {
        // OK. static methods aren't expected to use this.
    }
}
```

### Options
Exceptions
"class-methods-use-this": [<enabled>, { "exceptMethods": [<...exceptions>] }]
exceptMethods 选项允许你传递一个你想要忽略警告的方法名的数组。例如，你可能有一个来自外部库的规范，它要求你将方法作为常规函数(而不是静态方法)重写，并且在函数体中不使用 this 。在本例中，可以将该方法添加到警告中来忽略。

当使用 exceptMethods 时的 错误 代码示例：
```js
/*eslint class-methods-use-this: "error"*/

class A {
    foo() {
    }
}
```

当使用 exceptMethods 时的 正确 代码示例：
```js
/*eslint class-methods-use-this: ["error", { "exceptMethods": ["foo"] }] */

class A {
    foo() {
    }
}
```

### Version
该规则在 ESLint 3.4.0 中被引入。
