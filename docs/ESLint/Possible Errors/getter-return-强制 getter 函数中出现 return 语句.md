## 强制在 getter 属性中出现一个 return 语句 (getter-return)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

get 语法将对象属性绑定到一个函数，该函数在查找该属性时将被调用。这是首次在 ECMAScript 5 中引入：
```js
    var p = {
        get name(){
            return "nicholas";
        }
    };

    Object.defineProperty(p, "age", {
        get: function (){
            return 17;
        }
    });
```
注意，每个 getter 都期望有返回值。

### Rule Details
该规则前置在属性 getter 中出现 return 语句。

错误 代码示例：
```js
/*eslint getter-return: "error"*/

p = {
    get name(){
        // no returns.
    }
};

Object.defineProperty(p, "age", {
    get: function (){
        // no returns.
    }
});

class P{
    get name(){
        // no returns.
    }
}
```

正确 代码示例：
```js
/*eslint getter-return: "error"*/

p = {
    get name(){
        return "nicholas";
    }
};

Object.defineProperty(p, "age", {
    get: function (){
        return 18;
    }
});

class P{
    get name(){
        return "nicholas";
    }
}
```

### Options
该规则有一个对象选项：

"allowImplicit": false (默认) 禁止在 return 语句中隐式地返回 undefined。
选项 { "allowImplicit": true } 的 正确 代码示例：
```js
/*eslint getter-return: ["error", { allowImplicit: true }]*/
p = {
    get name(){
        return; // return undefined implicitly.
    }
};
```

### When Not To Use It
如果你的项目不使用 ES5 属性 getter，你不需要使用此规则。

### Version
该规则在 ESLint 4.2.0 中被引入。

