# Node.js代码风格指南

这是一篇关于如何写出统一和优雅的Node.js代码的指南. 激发的灵感是社区中流行的代码, 和受人喜爱的一些个人观点.

这份指南是由[Felix Geisendörfer](http://felixge.de/)建立的. 版权协议是[CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/). 鼓励大家fork这个repository, 并根据自己的偏好做出调整.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## 4格缩进

用4个空格作为缩进, 发誓不要混淆Tab和空格, 在你的代码中. 不然的话, 另一个地狱说不定在等待你.

## 结尾没有空格

就和你每次吃饭后刷牙一样, 你清除所有的结尾空格, 在你提交JS文件之前. 否则不小心造成的疏忽所产生的腐烂味道, 会最终赶走所有的贡献者和同事.

## 使用分号

根据[科学研究][hnsemicolons], 使用分号是我们(JavaScript)社区的核心价值. 考虑到这点[the opposition][], 但是请按照传统的方法使用分号, 当它成为滥用错误纠正机制, 为了廉价的语法快乐.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

## 每行80字

约束你每行的字数最大到80字. 是的, 这几年显示器变的越来越大, 但是你的大脑却没有. 使用额外的功能去分屏. 你的编辑器支持这个功能, 对吗?

## 使用单引号

使用单引号, 除非你在写JSON.

*正确:*

```js
var foo = 'bar';
```

*错误:*

```js
var foo = "bar";
```

## 不换行使用大括号

大括号在语句之后紧跟, 不需要换行.

*正确:*

```js
if (true) {
  console.log('winning');
}
```

*错误:*

```js
if (true)
{
  console.log('losing');
}
```

同样, 请注意在条件语句的前后, 使用空格.

## 每行声明一个变量

每行申明一个变量, 这个会让我们容易重新安排行数. 在这里忽略[Crockford][crockfordconvention]的方式, 尽可能的显式申明.

*正确:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (items.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*错误:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (items.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

## 变量, 属性, 方法名使用小骆驼拼写法

变量, 属性和方法名应该使用`小骆驼拼写法`. 他们应该同样是描述性的. 单个字符的变量和不常见的缩写通常应该是避免的.

*正确:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*错误:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

## 类名使用大骆驼拼写法

类名应该使用`大骆驼拼写法`.

*正确:*

```js
function BankAccount() {
}
```

*错误:*

```js
function bank_Account() {
}
```

## 常量大写

常量应该被声明成常规变量, 或者静态类属性, 使用所有的大写字母.

Node.js / V8 虽然支持Mozilla的[const][const]扩展, 但是不幸的是, 这个不能适用于类的成员变量, 同样也不是ECMA的标准.

*正确:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*错误:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
``` 

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## 对象 / 数组建立

使用后面的逗号, 并且使用短声明在每1行上. 只在key上放引号, 当你的解释器抱怨的时候.

*正确:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*错误:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## 使用===符号

编程不是关于记住那些[愚蠢的规则][comparisonoperators]. 使用3个恒等于, 因为它会像预期的那样工作.

*正确:*

```js
var a = 0;
if (a === '') {
  console.log('winning');
}

```

*错误:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

## 三元判断符多行使用

三元操作符不应该单行使用. 把它分到多行使用.

*正确:*

```js
var foo = (a === b)
  ? 1
  : 2;
```

*错误:*

```js
var foo = (a === b) ? 1 : 2;
```

## 不要扩展内建原型

不要扩展原生JavaScript对象的原型. 你以后的self会永远感恩.

*正确:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*错误:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```

## 使用描述性的语言

任何非平凡的条件应该被赋予一个描述性的参数:

*正确:*

```js
var isAuthorized = (user.isAdmin() || user.isModerator());
if (isAuthorized) {
  console.log('winning');
}
```
*错误:*

```js
if (user.isAdmin() || user.isModerator()) {
  console.log('losing');
}
```

## 写精简的方法

保持你的方法很精简. 如果一个函数写的好, 那么它能在演讲上使用, 而且大教室里的最后几排的人都可以清楚的看懂. 所以不要计算它们有完美的世界, 并且限制你自己每个函数只写15行.

## 快速返回值

为了避免if语句的深层嵌套, 请尽快返回一个函数的结果.

*正确:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*错误:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

或者为了这个特别的例子, 可能缩短一点更好:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

## 给你的闭包命名

随便给你的闭包取个名字. 这意味着你关心他们, 并且能更好的追踪栈, 堆, 和CPU性能问题.

*正确:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*错误:*

```js
req.on('end', function() {
  console.log('losing');
});
```

## 没有嵌套闭包


