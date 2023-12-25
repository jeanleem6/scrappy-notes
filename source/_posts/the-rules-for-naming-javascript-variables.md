---
title: JavaScript变量命名规则
date: 2016-12-14 10:55:58
tags: [javascript]
---

以下是JavaScript变量的命名规则：

1. **变量名不能以数字开头**
    例如：`3x`、`2goats`或者`76trombones`都是*非法的*变量名；
    当然，你可以在变量名中使用数字。
    例如：`up2me`或者`go4it`都是*合法的*变量名。

2. **变量名不能包含数学或逻辑运算符**
    例如：`2*something`或者`this+that`都是非法的，因为 * 和 + 都是算数运算符，也同样适用于`^, /, \, !`等符号。

3. **变量名不能包含任何形式的标点符号，除了下划线`_`**
    例如：`some:thing`、`big#`或者`do'to`都是非法的。
    下划线是一个例外，它可以用在变量名的开头、中间、末尾。
    例如：`_pounds`、`some_thing`或者`gallons_`都是合法的。

    <!-- more -->

4. **任何时候，变量名都不能含有空格**

5. **变量名不能为JavaScript的保留字**
    例如：`window`、`open`、`location`、`string`等都是非法的变量名。
    当然，你可以将保留字作为变量名的一部分。
    例如：`thatWindow`、`someString`、`theLocation`都是合法的。

6. **变量名对大小写敏感**
    例如，在JavaScript中以下都是完全不同的变量名：
    `gasbag`、`Gasbag`、`GasBag`、`gasBag`

如果不能确定，你可以[点击这里] [link-01]查看你的变量名是否合法。

[link-01]: https://mothereff.in/js-variables

