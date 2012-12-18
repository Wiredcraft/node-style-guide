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



