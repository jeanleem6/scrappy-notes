---
title: Using css counters
date: 2017-09-11 15:41:20
tags: [css]
---

> 今天在 W3C 查阅 [background 标准](https://www.w3.org/TR/css3-background/#the-background)时偶然发现这个属性。

## counters 兼容性

为什么要首先谈它的兼容性？因为这个属性**可以被所有浏览器支持**（<del>IE6/7</del>除外），是不是有了看下去的欲望^o^

## 定义

**CSS counters** 基于在文档中的位置来改变其显示的内容。比如，可以用它对网页中的标题自动计数。

**CSS计数器**本质上是由 CSS 在维护的变量，这些变量可能根据CSS规则增加以跟踪使用次数。

## 使用

首先，必须用 `counter-reset`为计数器设置一个初始值(默认为 0)；
可以在之后赋予 `counter-reset` 一个特定的数值来改变计数器的值。
之后，就可以通过 `counter-increment` 对计数器的值进行递增或递减。
`counter` 的 *name* 属性不能是 none、inherit、initial，否则，这条申明将被忽略。

## 显示 counter

`counter` 的值可以通过赋给 `content` 属性 `counter()` 或 `counters()` 函数来显示。

- `counter()` 函数有两种形式：

``` css
counter(name)
counter(name, style)
```

生成的文本是对给定的伪元素在给定的 *name* 范围内最里层级的计数的值，通过设定的 *style* 值对其格式化 （默认为`decimal` - 10进制）。

- `counters()` 函数同样有两种形式

``` css
counters(name, string)
counters(name, string, style)
```

生成的文本是对给定的伪元素在给定的 *name* 范围内所有计数器的值，从最外层级到最里层级通过设定的 *string* 字符分隔，通过设定的 *style* 值对其格式化 （默认为`decimal` - 10进制）。

## 基本用法举例

本例子将在每个标题的前面添加 *Section [计数器的值]*

``` css
body {
    counter-reset: section;  /*设置名为 section 的计数器，初始值为0*/
}

h3::beforer {
    counter-increment:section; /*将 section 的计数器增加1*/
    content:counter(section);  /*显示 section 计数器的值*/
}
```

``` html
<h3>Introduction</h3>
<h3>Body</h3>
<h3>Conclusion</h3>
```

前台显示结果:

```
1Introduction
2Body
3Conclusion
```

## 嵌套用法举例

css 计数器在有序列表中尤其有用，因为它会自动在子元素上创建计数器。使用 `counters()` 函数，分隔符会自动插入不同层级的嵌套计数中。

``` css
ol {
    counter-reset: section;
    list-style-type: none;
}
li::before {
    counter-increment: section;
    content:counters(section, '.') ' ';  /*用 . 做分隔符*/
}
```

``` html
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item               <!-- 2     -->
    <ol>
      <li>item</li>      <!-- 2.1   -->
      <li>item</li>      <!-- 2.2   -->
      <li>item           <!-- 2.3   -->
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
        </ol>
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
          <li>item</li>  <!-- 2.3.3 -->
        </ol>
      </li>
      <li>item</li>      <!-- 2.4   -->
    </ol>
  </li>
  <li>item</li>          <!-- 3     -->
  <li>item</li>          <!-- 4     -->
</ol>
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item</li>          <!-- 2     -->
</ol>
```

前台显示结果:

```
1 item
2 item
    2.1 item
    2.2 item
    2.3 item
        2.3.1 item
        2.3.2 item
        2.3.1 item
        2.3.2 item
        2.3.3 item
    2.4 item
3 item
4 item
1 item
2 item
```

> 注意在 ** *2.3* 下的两个 ol 列表 **及其前台显示结果（*2.3.1* 和 *2.3.2*）
