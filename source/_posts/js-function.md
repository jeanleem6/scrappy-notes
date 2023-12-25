---
title: js-function
date: 2017-10-06 08:42:46
tags: [javascript]
---

## 概览

说起来 ECMAScript 中什么最有意思，我想莫过于函数了——而有意思的根源，则在于函数实际上是对象。

- 函数是对象，函数名是指针；
- 每个函数都是 Function 的实例，而且都与其它引用类型一样具有属性和方法；
- 由于函数是对象，因此函数名实际上也是一个指向函数对象的指针，不会与某个函数绑定。

## 函数声明

``` javascript
function sum(num1, num2) {
    return num1 + num2;
}
```

``` javascript
// 使用 Function 构造函数
var sum = function(num1, num2) {
    return num1 + num2;
};
```

**Function 构造函数可以接收任意数量的参数，但最后一个参数始终都被看成是函数体，而前面的参数则枚举出了新函数的参数。**来看一个例子：

``` javascript
var sum = new Function('num1', 'num2', 'return num1 + num2'); // 不推荐
```

我们不推荐使用这种方法定义函数，因为这种语法会导致解析两次代码（第一次解析常规 ECMAScript 代码，第二次是解析传入构造函数中的字符串），从而影响性能。不过，这种语法对于理解**“函数是对象，函数名是指针”**的概念倒是非常直观的。

## 函数名是指针

由于函数名仅仅是指向函数的指针，因此函数名与包含对象指针的其他变量没有什么不同。换句话说，**一个函数可能会有多个名字**，来看如下的例子：

``` javascript
var sum = function(sum1, sum2) {
    return sum1 + sum2;
}
console.log(sum(10, 20)); // 30

var anothersum = sum;
console.log(anothersum(10, 20)); // 30

sum = null;
console.log(anothersum(10, 20)); // 30
```

> 注意：**使用不带圆括号的函数是访问函数指针，而非调用函数。**

在上面的例子中，anothersum 和 sum 都指向了同一个函数，因此 `anothersum()` 也可以被调用并返回结果。即使 sum 设置为 null，让它与函数“断绝关系”，但仍然可以正常调用 `anothersum()`。

## 函数没有重载

如果定义了两个同名的函数，则后一个函数会覆盖前一个函数。将函数名想象为指针，有助于理解为什么 ECMAScript 中没有函数重载的概念。来看一个例子：

``` javascript
function addSomeNumber(num) {
    return num + 100;
}

function addSomeNumber(num) {
    return num + 200;
}

var result = addSomeNumber(100); // 300
```

再看下面这个例子：

``` javascript
var addSomeNumber = function(num) {
    return num + 100;
}

addSomeNumber = function(num) {
    return num + 200;
}

var result = addSomeNumber(100); // 300
```

通过观察从写之后的代码，很容易看清楚到底是怎么回事儿——在创建第二个函数时，实际上覆盖了引用第一个函数的变量 addSomeNumber。

## 函数声明与函数表达式

解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。

- 解析器会率先读取函数声明（函数声明提升——function declaration hoisting），并使其在执行任何代码之前可用（可以访问）；
- 至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解析执行。

来看两个例子：

``` javascript
console.log(sum(10,10)); // 20
function sum(num1,num2) {
    return num1 + num2;
}

console.log(sum(10,10)); // error (unexpected identifier)
var sum = function(num1,num2) {
    return num1 + num2;
}
```

## 作为值的函数

因为 ECMAScript 中的函数名本身就是变量，所以函数也可以作为值来使用。来看一个例子：

``` javascript
function callSomeFunction(someFunction, someArgument) {
    return someFunction(someArgument);
}
```

这个函数接收两个参数。第一个参数应该是一个函数，第二参数应该是要传递给该函数的一个值。然后，就可以像下面的例子一样传递函数了：

``` javascript
function add10(num) {
    return num + 10;
}

var result1 = callSomeFunction(add10,10);
console.log(result1); // 20

function getGreeting(name) {
    return "Hello, " + name;
}

var result2 = callSomeFunction(getGreeting, 'Jeanleem6');
console.log(result2); // "Hello, Jeanleem6"
```

> 注意：`callSomeFunction(someFunction, someArgument)`这里的第一个参数是要访问函数的指针而不执行函数，所以要去掉后面的那对圆括号。所以，这里传递的是 add10 和 getGreeting，而不是执行它们之后的结果。

下面再看一个例子：从一个函数中返回另一个函数，根据某个对象属性对数组进行排序。

``` javascript
function createComparisonFunction(propertyName) {
    return function(object1,object2) {
        var value1 = object1[propertyName];
        var value2 = object2[propertyName];

        if(value1 < value2) {
            return -1;
        } else if(value1 > value2) {
            return 1;
        } else {
            return 0;
        }
    };
}

var data = [{name:'Zachary',age:27},{name:'Jeanleem6',age:32}];

data.sort(createComparisonFunction('name'));
console.log(data[0].name); // "Jeanleem6"

data.sort(createComparisonFunction('age'));
console.log(data[0].name); // "Zachary"
```

在默认情况下，`sort()` 方法会调用每个对象的 `toString()` 方法以确定它们的次序；但得到的结果往往并不符合人类的思维习惯。因此，我们调用 `createComparisonFunction('name')` 方法创建了一个比较函数，以遍按照每个对象的 name 属性值进行排序。

## 函数内部属性

- `arguments`
- `this`

### arguments

虽然 arguments 主要用途是保存函数参数，但这个对象还有一个名叫 `callee` 的属性，该属性是一个指针，指向拥有这个 arguments 对象的函数。来看一个非常经典的阶乘函数：

``` javascript
function factorial(num) {
    if(num <= 1) {
        return 1;
    } else {
        return num * factorial(num - 1);
    }
}
```

在函数名不会变的情况下这样定义没有问题；但问题是这个函数的执行与函数名 factorial 紧紧耦合在了一起，为了消除这种耦合现象，可以像下面这样使用 `arguments.callee`：

``` javascript
function factorial(num) {
    if(num <= 1) {
        return 1;
    } else {
        return num * arguments.callee(num - 1);
    }
}

var trueFactorial = factorial;

factorial = function() {
    return 0;
}

console.log(trueFactorial(5)); // 120
console.log(factorial(5)); // 0
```

### this

`this` 引用的是函数据以执行的环境对象——或者也可以说是 this 值（当在网页的全局作用域中调用函数时，this 对象引用的就是 window）。来看一个例子：

``` javascript
window.color = 'red';
var o = {color:'blue'};

function sayColor() {
    console.log(this.color);
}

sayColor(); // "red"

o.sayColor = sayColor;
o.sayColor(); // "blue"
```

> 一定要牢记，函数的名字仅仅是一个包含指针的变量而已。因此，即使是在不同的环境中执行，全局的 sayColor() 函数与 o.sayColor() 指向的仍然是同一个函数。

## 函数属性和方法

ECMAScript 中的函数是对象，因此函数也有属性和方法。

### 属性

每个函数都包含两个属性：

- `length` 表示函数希望接收的命名参数的个数
- `prototype` 对于 ECMAScript 中的引用类型而言，prototype 是保存它们所有实例方法的真正所在。换句话说，诸如 `toString()` 和 `toValue()` 等方法实际上都保存在 prototype 名下，只不过是通过各自对象的实例访问罢了。

### 方法

每个函数都包含两个非继承而来的方法：

- `apply()`
- `call()`

这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内 this 对象的值。

`apply()` 方法接收两个参数：一个是在函数中运行的作用域，另一个是参数数组。其中，第二个参数可以是 Array 的实例，也可以是 arguments 对象。来看一个例子：

``` javascript
function sum(num1,num2) {
    return num1 + num2;
}

function callSum1(num1,num2) {
    return sum.apply(this,arguments);
}

function callSum2(num1,num2) {
    return sum.apply(this,[num1,num2]);
}

console.log(callSum1(10,20)); // 30
console.log(callSum2(10,20)); // 30
```

`call()` 方法与 `apply()` 方法的作用相同，它们的区别仅在于接收参数的方式不同。`call()` 方法的第一个参数同样是 this；变化的是其余参数都直接传递给函数（参数必须逐个列举出来）。看一个例子：

``` javascript
function sum(num1,num2) {
    return num1 + num2;
}

function callSum(num1,num2) {
    return sum.call(this,num1,num2);
}

console.log(callSum(10,20)); // 30
```

事实上，传递参数并非 `apply()` 和 `call()` 真正的用武之地；它们真正强大的地方是能够扩充函数赖以运行的作用域。来看一个例子：

``` javascript
window.color = 'red';
var o = {color:'blue'};

function sayColor() {
    console.log(this.color);
}

sayColor(); // "red"

sayColor.call(this); // "red"
sayColor.call(window); // "red"
sayColor.call(o); // "blue"
```

当运行 `sayColor.call(o)` 时，函数的执行环境就不一样了，因为此时函数体内的 this 对象指向了 o，于是结果显示的是 "blue"。

使用 `call()`(或 `apply()`)来扩充作用域的最大好处，就是对象不需要与方法有任何耦合关系。


- `bind()` ECMAScript 5 定义的一个方法。这个方法会创建一个函数的实例，其 this 值会被绑定到传给 `bind()` 函数的值。

``` javascript
window.color = 'red';
var o = {color:'blue'};

function sayColor() {
    console.log(this.color);
}
var objectSayColor = sayColor.bind(o);
objectSayColor(); // "blue"
```

- `toLocaleString()`
- `toString()`
- `valueOf()`

这三个方法始终都返回函数的代码，但不同浏览器返回的格式可能不同；因此我们无法根据它们返回的结果来实现任何重要的功能；不过这些返回的信息在调试代码时倒是很有用。
