---
title: JavaScript变量命名规则
date: 2016-12-14 10:55:58
description:
tags: [javascript]
---

以下是JavaScript变量的命名规则：

1. **变量名不能以数字开头**

   ```javascript
   var 3x, 2goats, 76trombones // 非法变量名
   var up2me, go4it // 合法变量名
   ```

2. **变量名不能包含数学或逻辑运算符**

   ```javascript
   var 2*something, this+that // 非法的，因为 * 和 + 都是算数运算符，也同样适用于 ^, /, \, ! 等符号。
   ```

3. **变量名不能包含任何形式的标点符号，除了下划线 `_`**

   ```javascript
   var some:thing, big#, do'to // 非法
   var _pounds, some_thing, gallons_ // 合法
   ```

4. **任何时候，变量名都不能含有空格**

5. **变量名不能为JavaScript的保留字**

   ```javascript
   var window, open, location, string // 非法
   var thatWindow, someString, theLocation // 合法 (将保留字作为变量名的一部分是合法的)
   ```

6. **变量名对大小写敏感**

   ```javascript
   var gasbag, Gasbag, GasBag, gasBag // 它们是完全不同的变量名
   ```

如果不能确定，你可以[点击这里](https://mothereff.in/js-variables)查看你的变量名是否合法。
