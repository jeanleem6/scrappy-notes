---
title: js-RegExp
date: 2017-10-05 13:56:18
tags: [javascript,RegExp]
---

## 创建正则

### 字面量形式

``` javascript
var expression = /pattern/flags;
```

- `pattern`: 可以是任何简单或复杂的正则表达式，可以包含字符类、限定符、分组、向前查找以及反向应用；
- `flags`:
    - `g` 全局模式(global)，即应用于所有字符串，而非发现第一个匹配项时立即停止；
    - `i` 不区分大小写(case-insensitive)模式；
    - `m` 多行(multiline)模式，即在到达一行文本末尾时还会继续查找下一行中是否存在与模式匹配的项。

模式(pattern)中使用的**元字符**都必须转义。正则中的元字符包括：

``` javascript
( [ { \ ^ $ | ) ? * + .]}
```

### RegExp 构造函数

``` javascript
var expression = new RegExp('pattern', 'flags');
```

> 注意：传递给 RegExp 构造函数的两个参数都是字符串，所以在某些情况下需要对字符进行双重转义。所有元字符都必须双重转义（例如`\n`，字符 `\` 在字符串中通常被转义为 `\\`，而在正则表达式字符串中就会变成 `\\\\`。）

## RegExp 实例属性

- `global` ：布尔值，表示是否设置了 `g` 标志；
- `ignoreCase` ：布尔值，表示是否设置了 `i` 标志；
- `lastIndex` ：整数，表示开始搜索下一个匹配项的字符位置，从 0 算起；
- `multiline` ：布尔值，表示是否设置了 `m` 标志；
- `source` ：正则的字符串表示，按照字面量形式而非传入构造函数中的字符串模式返回。

``` javascript
var pattern1 = /\[bc\]at/i;

alert(pattern1.global);  //false
alert(pattern1.ignoreCase);  //true
alert(pattern1.multiline);  //false
alert(pattern1.lastIndex);  //0
alert(pattern1.source);  //"\[bc\]at"

var pattern2 = new RegExp("\\[bc\\]at", "i");

alert(pattern2.global);  //false
alert(pattern2.ignoreCase);  //true
alert(pattern2.multiline);  //false
alert(pattern2.lastIndex);  //0
alert(pattern2.source); //"\[bc\]at"
```

## RegExp 实例方法

### 1. exec()

`exec()` 方法用于捕获组，它接收一个参数，即要应用模式的字符串，然后返回包含第一个匹配项的数组；或在没有匹配项的情况下返回 null。

它返回的数组包含两个额外的属性：`index` 和 `input`。

- `index` 表示匹配项在字符串中的位置；
- `input` 表示应用正则表达式的字符串。

``` javascript
var text = "mom and dad and baby";
var pattern = /mom( and dad( and baby)?)?/gi;

var matches = pattern.exec(text);
alert(matches.index); // 0
alert(matches.input); // "mom and dad and baby"
alert(matches[0]); // "mom and dad and baby"
alert(matches[1]); // " and dad and baby"
alert(matches[2]); // " and baby"
```

### 2. test()

`test()` 接收一个字符串参数。在模式与该参数匹配的情况下返回 true；否则，返回 false。

在只想知道目标字符串与某个模式是否匹配，但不需要知道其文本内容的情况下，使用这个方法非常方便。因此，`test()` 方法经常被用在 if 语句中。

``` javascript
var text = "000-00-0000";
var pattern = /\d{3}-\d{2}-\d{4}/;

if (pattern.test(text)){
    alert("The pattern was matched.");
}
```

RegExp 实例继承的 `toLocaleString()` 和 `toString()` 方法都返回正则表达式的字面量，与创建正则的方式无关。而 `valueOf()` 方法返回正则表达式本身。

## RegExp 构造函数属性

| 长属性名 | 短属性名 | 说明 |
|- - - | - - - | - - -|
| input | $_ | 最近一次要匹配的字符串。Opera未实现此属性 |
| lastMatch | $& | 最近一次的匹配项。Opera未实现此属性 |
| lastParen | $+ | 最后一次匹配的捕获组。Opera未实现此属性 |
| leftContext | $\` | input 字符串中 lastMatch 之前的文本 |
| multiline | $* | 布尔值，表示是否所有表达式都使用多行模式。IE和Opera未实现此属性 |
| rightContext | $' | input 字符串中 lastMatch 之后的文本 |

除了上面这几个属性外，还有9个用于存储捕获组的构造函数属性。访问这些属性的语法是：`RegExp.$1`、`RegExp.$2`...`RegExp.$3`，分别用于存储第一、第二...第九个匹配的捕获组。在调用 `exec()` 或 `test()` 方法时，这些属性会被自动填充。

``` javascript
var text = "this has been a short summer";
var pattern = /(..)or(.)/g;

if (pattern.test(text)){
    alert(RegExp.$1); // sh
    alert(RegExp.$2); // t
}
```

