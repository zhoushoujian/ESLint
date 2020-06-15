## 禁止不规则的空白 (no-irregular-whitespace)

```配置文件中的 "extends": "eslint:recommended" 属性启用了此规则。```

无效的或不规则的空白会导致 ECMAScript 5 解析问题，也会使代码难以调试（类似于混合 tab 和空格的情况）。

各种空白字符可能是由程序员误输入的，比如拷贝或键盘快捷键。例如，在 macOS 按下 Alt + Space，增加了一个不间断空格。

Known issues these spaces cause:

零宽空格
不被认为是分隔符，经常被解析为 Unexpected token ILLEGAL
不在现代浏览器中显示，期待使用代码存储软件解决其可视化问题
行分隔符
在 JSON 中不是一个有效的字符，会引起解析错误

### Rule Details
This rule is aimed at catching invalid whitespace that is not a normal tab and space. Some of these characters may cause issues in modern browsers and others will be a debugging issue to spot.

This rule disallows the following characters except where the options allow:

\u000B - Line Tabulation (\v) - <VT>
\u000C - Form Feed (\f) - <FF>
\u00A0 - No-Break Space - <NBSP>
\u0085 - Next Line
\u1680 - Ogham Space Mark
\u180E - Mongolian Vowel Separator - <MVS>
\ufeff - Zero Width No-Break Space - <BOM>
\u2000 - En Quad
\u2001 - Em Quad
\u2002 - En Space - <ENSP>
\u2003 - Em Space - <EMSP>
\u2004 - Tree-Per-Em
\u2005 - Four-Per-Em
\u2006 - Six-Per-Em
\u2007 - Figure Space
\u2008 - Punctuation Space - <PUNCSP>
\u2009 - Thin Space
\u200A - Hair Space
\u200B - Zero Width Space - <ZWSP>
\u2028 - Line Separator
\u2029 - Paragraph Separator
\u202F - Narrow No-Break Space
\u205f - Medium Mathematical Space
\u3000 - Ideographic Space
Options
This rule has an object option for exceptions:

"skipStrings": true (默认) 允许在字符串字面量中出现任何空白字符
"skipComments": true 允许在注释中出现任何空白字符
"skipRegExps": true 允许在正则表达式中出现任何空白字符
"skipTemplates": true 允许在模板字面量中出现任何空白字符

### skipStrings
Examples of incorrect code for this rule with the default { "skipStrings": true } option:
```js
/*eslint no-irregular-whitespace: "error"*/

function thing() /*<NBSP>*/{
    return 'test';
}

function thing( /*<NBSP>*/){
    return 'test';
}

function thing /*<NBSP>*/(){
    return 'test';
}

function thing᠎/*<MVS>*/(){
    return 'test';
}

function thing() {
    return 'test'; /*<ENSP>*/
}

function thing() {
    return 'test'; /*<NBSP>*/
}

function thing() {
    // Description <NBSP>: some descriptive text
}

/*
Description <NBSP>: some descriptive text
*/

function thing() {
    return / <NBSP>regexp/;
}

/*eslint-env es6*/
function thing() {
    return `template <NBSP>string`;
}
```

Examples of correct code for this rule with the default { "skipStrings": true } option:
```js
/*eslint no-irregular-whitespace: "error"*/

function thing() {
    return ' <NBSP>thing';
}

function thing() {
    return '​<ZWSP>thing';
}

function thing() {
    return 'th <NBSP>ing';
}
```

skipComments
Examples of additional correct code for this rule with the { "skipComments": true } option:
```js
/*eslint no-irregular-whitespace: ["error", { "skipComments": true }]*/

function thing() {
    // Description <NBSP>: some descriptive text
}

/*
Description <NBSP>: some descriptive text
*/
```

skipRegExps
Examples of additional correct code for this rule with the { "skipRegExps": true } option:
```js
/*eslint no-irregular-whitespace: ["error", { "skipRegExps": true }]*/

function thing() {
    return / <NBSP>regexp/;
}
```

skipTemplates
Examples of additional correct code for this rule with the { "skipTemplates": true } option:
```js
/*eslint no-irregular-whitespace: ["error", { "skipTemplates": true }]*/
/*eslint-env es6*/

function thing() {
    return `template <NBSP>string`;
}
```

### When Not To Use It
If you decide that you wish to use whitespace other than tabs and spaces outside of strings in your application.
