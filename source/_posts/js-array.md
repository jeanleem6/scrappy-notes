---
title: Array-JavaScript
date: 2016-09-29 10:35:10
tags: [javascript]
---

在 JavaScript 中 Array 是一个用来构造数组的全局对象，它是一个高阶的类似有序列表的对象。

## 创建一个数组

``` javascript
    var fruits = ["apple", "banana"];

    console.log(fruits.length);
    // 2
```

## 通过索引访问数组元素

``` javascript
    var first = fruits[0];
    // apple

    var last = fruits[fruits.length - 1];
    // banana
```

<!-- more -->

## 遍历数组

``` javascript
    fruits.forEach(function(item, index, array) {
        console.log(item, index, item == array[index]);
    });
    // apple 0 true
    // banana 1 true
```

## 添加元素到数组的末尾

``` javascript
    var newLength = fruits.push("Orange");
    // ["apple", "banana", "Orange"]
```

## 删除数组末尾的元素

``` javascript
    var last = fruits.pop(); // remove Orange from the end
    // ["apple", "banana"]
```

## 删除数组前面的元素

``` javascript
    var first = fruits.shift(); // remove apple from the front
    // ["banana"]
```

## 添加到数组的前面

``` javascript
    var newLength = fruits.unshift("Strawberry"); // add to the front
    // ["Strawberry", "banana"]
```

## 找到某个元素在数组中的索引

``` javascript
    fruits.push("Mango");
    // ["Strawberry", "banana", "Mango"]

    var pos = fruits.indexOf("banana");
    // 1
    // 如果找不到该元素，则返回 -1
```

## 通过索引删除某个元素

``` javascript
    var removeItem = fruits.splice(pos, 1); // this is how to remove an item
    // ["Strawberry", "Mango"]
```

## 复制一个数组

``` javascript
    var shallowCopy = fruits.slice(); // this is how to make a copy
    // ["Strawberry", "Mango"]
```

## 将数组中的所有元素连结为一个字符串

``` javascript
    var str = fruits.join('');
    // StrawberryMango

    fruits.toString();
    // Strawberry,Mango

    var number = 1337;
    var date = new Date();
    var myArr = [number, date, "foo"];
    var str = myArr.toLocaleString();
    console.log(str);
    // 1337,2016/9/29 下午6:07:07,foo
```

## 检测一个变量是否是数组

``` javascript
    Array.isArray(fruits);
    // true

    Array.isArray(Array.prototype);
    // true

    var a = "text";
    Array.isArray(a);
    // false
```

## 颠倒数组元素的排列顺序

``` javascript
    fruits.reverse();
    // ["Mango", "Strawberry"]
```

## 对数组元素进行排序

``` javascript
    var nums = [3, 7, 5, 2];
    nums.sort();
    // [2, 3, 5, 7]
```

## 数组与数组或非数组值组合

``` javascript
    nums.concat(fruits);
    // [2, 3, 5, 7, "Mango", "Strawberry"]

    nums. concat(1, [2, 3]);
    // [2, 3, 5, 7, "Mango", "Strawberry", 1, 2, 3];
```

## 语法

``` javascript
    [element0, element1, ..., elementN]
    new Array(element0, element1[, ...[, elementN]])
    new Array(arrayLength)
```

**元素列 —— elementN**
Array 构造器将会根据给出的元素创建一个 JavaScript 数组，但是当参数仅有一个参数且其为数字时除外，参考下面的 arrayLength。值得注意的是，这种情况仅在使用 Array 构造器时出现，使用带方括号的数组字面量则不会。

**数组长度 —— arrayLength**
向 Array 构造函数传入一个在 0 到 232-1 之间的整数，将返回一个以此为长度的数组对象。通过 length 属性可以访问这个值。如果传入的参数不是有效的数值，则抛出 RangeError 异常。

---

reference:
[Array-JavaScript | MDN][re1]
[JavaScript标准库 | MDN][re2]

[re1]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array
[re2]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects
