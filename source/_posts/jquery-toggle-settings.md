---
title: jquery toggle()及相关动画设置
date: 2017-06-14 08:37:58
description: 💬聊一聊 jquery 的 <code>toggle()</code> 方法及动画设置💬
tags: [jQuery]
---

## toggle()

`toggle() 方法切换元素的可见状态。`
如果被选元素可见，则隐藏这些元素，如果被选元素隐藏，则显示这些元素。

``` javascript
$(selector).toggle(speed,callback,switch) //水平显隐动画

// 栗子
$(".btn1").click(function(){
    $("p").toggle(200);
    $("p").toggle(true);  //显示所有 p 元素
    $("p").toggle(false);  //隐藏所有 p 元素
});
```

*[参数]说明：*

- **speed:** 可选。规定元素从可见到隐藏的速度（或者相反）。默认为 "0"。
    在设置速度的情况下，元素从可见到隐藏的过程中，会逐渐地改变其高度、宽度、外边距、内边距和透明度。*如果设置此参数，则无法使用 switch 参数。*
    **可能的值：**毫秒 （比如 1500）、slow、normal、fast
- **callback**: 可选。toggle 函数执行完之后，要执行的函数。*除非设置了 speed 参数，否则不能设置该参数。*
- **switch**: 可选。布尔值。规定 toggle 是否*隐藏(false)*或*显示(true)*所有被选元素。*如果设置此参数，则无法使用 speed 和 callback 参数。*

## slideToggle()

`slideToggle() 方法通过使用滑动效果（高度变化）来切换元素的可见状态。`
如果被选元素是可见的，则隐藏这些元素，如果被选元素是隐藏的，则显示这些元素。

``` javascript
$(selector).slideToggle(speed,callback) //垂直显隐动画

// 栗子
$(".btn1").click(function(){
    $("p").slideToggle(200);
});
```

*[参数]说明：*

- **speed:** 可选。规定元素从可见到隐藏的速度（或者相反）。默认为 "normal"。在设置速度的情况下，元素在切换的过程中，会逐渐地改变其高度（这样会创造滑动效果）。 **可能的值：**毫秒 （比如 1500）、slow、normal、fast
- **callback**: 可选。toggle 函数执行完之后，要执行的函数。*除非设置了 speed 参数，否则不能设置该参数。*

## Fading——淡入淡出

通过 jQuery，您可以实现元素的**淡入淡出**效果。

jQuery 拥有下面四种 fade 方法：

``` javascript
fadeIn()
fadeOut()
fadeToggle()
fadeTo()
```

### fadeIn()

`fadeIn() 用于淡入已隐藏的元素。`

``` javascript
$(selector).fadeIn(speed,callback);

// 栗子
$("button").click(function(){
    $("#div1").fadeIn();
    $("#div2").fadeIn("slow");
    $("#div3").fadeIn(3000);
});
```

*[参数]说明：*

- **speed**：可选，参数规定效果的时长。它可以取以下值：slow、fast 或毫秒。
- **callback**：可选，参数是 fading 完成后所执行的函数名称。

### fadeOut()

`fadeOut() 用于淡出可见元素。`

``` javascript
$(selector).fadeOut(speed,callback);

// 栗子
$("button").click(function(){
    $("#div1").fadeOut();
    $("#div2").fadeOut("slow");
    $("#div3").fadeOut(3000);
});
```

*[参数]说明：*

- **speed**：可选，参数规定效果的时长。它可以取以下值：slow、fast 或毫秒。
- **callback**：可选，参数是 fading 完成后所执行的函数名称。

### fadeToggle()

`fadeToggle() 方法可以在 fadeIn() 与 fadeOut() 方法之间进行切换。`
如果元素已淡出，则 fadeToggle() 会向元素添加淡入效果。
如果元素已淡入，则 fadeToggle() 会向元素添加淡出效果。

``` javascript
$(selector).fadeToggle(speed,callback);

// 栗子
$("button").click(function(){
    $("#div1").fadeToggle();
    $("#div2").fadeToggle("slow");
    $("#div3").fadeToggle(3000);
});
```

*[参数]说明：*

- **speed**：可选，参数规定效果的时长。它可以取以下值：slow、fast 或毫秒。
- **callback**：可选，参数是 fading 完成后所执行的函数名称。

### fadeTo()

`fadeTo() 方法允许渐变为给定的不透明度（值介于 0 与 1 之间）。`

``` javascript
$(selector).fadeTo(speed,opacity,callback);

// 栗子
$("button").click(function(){
    $("#div1").fadeTo("slow",0.15);
    $("#div2").fadeTo("slow",0.4);
    $("#div3").fadeTo("slow",0.7);
});
```

*[参数]说明：*

- **speed**：必须，参数规定效果的时长。它可以取以下值：slow、fast 或毫秒。
- **opacity**：必须，参数将淡入淡出效果设置为给定的不透明度（值介于 0 与 1 之间）。
- **callback**：可选，参数是 fading 完成后所执行的函数名称。

## 引深

同样的道理，jquery的show()和hide（）方向怎么设置呢？同样也可以用slideDown()和slideUp()来解决。达到你想要的效果！

## jQuery之相关动画效果操作

> 哈哈哈，加入你对上面的案例，在我说了之后不熟练，不熟悉的话，可以复习一下jquery的动画效果了！下面我列举一下！

### 1、show()显示效果

语法：show(speed,callback)　　Number/String,Function　speend为动画执行时间，单位为毫秒。也可以为slow","normal","fast"　callback可选,为当动画完成时执行的函数。

``` javascript
show(speed,[easing],callback)　　Number/String　　easing默认是swing,可选linear;

$("#div1").show(3000,function(){ alert("动画显示完成!"); });
```

### 2、hide()隐藏效果

语法:hide(speed,callback)　　Number/String,Function

``` javascript
hide(speed,easing,callback)　　Number/String

$("#div1").hide(3000,function(){ alert("动画隐藏完成") });
```

### 3、toggle()隐藏显示自动切换，当目前为显示则隐藏，当目前为隐藏则显示

语法：toggle(speed,callback)　　Number/String,Function

``` javascript
toggle(speed,callback)　　Number/String,String,Function

$("#div1").toggle(3000,function(){ alert("动画效果切换完成") });
```

### 4、slideDown()向下显示，slow()是水平与垂直方向同时展开，而slideDown是仅仅在垂直方向向下展开

语法:slideDown(speed,callback)　　Number/String,Function

``` javascript
slideDown(speed,[easing],callback)　　Number/String,Function

$("#div1").slideDown(3000,function(){ alert("向下展开显示成功!"); });
```

### 5、slideUp()向上隐藏,　　hide()是水平与垂直两个方向的，而slideUp()仅仅是垂直方向向上收起隐藏

语法:slideUp(speed,callback)　　Number/String,Function

``` javascript
slideUp(speed,[easing],callback)　　Number/String,String,Function

$("#div1").slideUp(3000,function(){ alert("向上收起隐藏成功!"); })
```

### 6、slideToggle垂直方向上切换,toggle是水平与垂直两个方向上的，而slideToggle是仅仅垂直方向的。

语法:slideToggle(speed,callback)　　Number/String,Function

``` javascript
slideToggle(speed,[easing],callback)　　Number/String,String,Function

$("#div1").slideToggle(3000,function(){ alert("水平方向上切换成功"); });
```

### 7、fadeIn() 以改变透明度来显示

语法：fadeIn(speed,callback)　　　　Number/String,Function

``` javascript
fadeIn(speed,[easing],callback)　　Number/String,Function

$("#div1").FadeIn(3000,function(){ alert("淡入显示成功!"); });
```

### 8、fadeOut() 以改变透明度来隐藏

语法：fadeOut(speed,callback)　　 Number/String,Function

``` javascript
fadeOut(speed,[easing],callcack)　　   Number/String,String,Function

$("#div1").fadeOut(3000,function(){ alert("淡出隐藏成功!"); });
```

### 9、fadeToggle() 以改变透明度来切换显示隐藏状态

语法: fadeToggle(speed,callback)　　Number/String,Function

``` javascript
fadeToggle(speed,[easing],callback)　　　　Number/String,Function

$("#div1").fadeToggle(3000,function(){ alert("淡入淡出切换成功!"); });
```

### 10、fadeTo() 由指定的时间将透明度改变到指定的透明度

语法：fadeTo(speed,callback)　　　　Number/String,Function

``` javascript
fadeTo([speed],opacity,[easing],[fn])　　Number/String,Float,String,Function

$("#div1").fadeTo(3000,0.22,function(){ alert("透明度改变成功!"); });
```

### 11、animate() 自定义动画，一般来说数字变动都可以用于动画。

语法：animate(params,speed,easing,callback);　　样式参数，时间，可选择，函数

``` javascript
$("#div1").animate({ width:300px,height,300px },3000);

// 其中params要用中括号括起来，可以使用的css样式参数。
// 注意要采用骆驼法则，如font-size要写成fontSize。颜色渐变不支持。

backgroundPosition
borderWidth
borderBottomWidth
borderLeftWidth
borderRightWidth
borderTopWidth
borderSpacing
margin
marginBottom
marginLeft
marginRight
marginTop
outlineWidth
padding
paddingBottom
paddingLeft
paddingRight
paddingTop
height
width
maxHeight
maxWidth
minHeight
maxWidth
font
fontSize
bottom
left
right
top
letterSpacing
wordSpacing
lineHeight
textIndent
```

### 12、`stop()` 停止正在执行动画

`stop([clearQueue],[gotoEnd])`;　　两个参数均为布尔值，第一个表示，是否停止动画执行、第二个表示，如果停止，是否立即变为执行完成的状态，如果设置为否，则停留在执行一半的状态。

``` javascript
$("#div1").hide(5000)　　//此动画正在执行

$("#div1").stop();　　　　//上一行代码指定的动画停止在一半状态

$("#div1").stop(true,true);　　//停止当前动画，同时动画切换到完成执行状态。
```

### 13、`delay()` 延迟执行动画：当一个动画stop()了之后还能够用delay()来延迟执行。从停止位置继续执行。当然用原来的方法继续执行也不可，不过没有延时效果。

``` javascript
delay(duration,[queueName])　　//设置一个延迟值来执行动画　　Integer,String

$("#div1").delay(3000).hide(3000);　　//表示在3000毫秒后执行hide(3000);
```

### 14、`jQuery.fx.off` 该属性只是是否关闭当前页面上的动画,关闭动画之后，没有动画效果，所有设置了执行时间的动画会瞬间完成。注意此属性出现的位置。出现的位置不同影响的范围也不同。

``` javascript
$(function(){

    jQuery.fx.off = true;　　//属性在事件外面，对页面加载后执行的所有动画有效

    $("#div1").click(function(){　　//属性如果写在这里，仅仅对当前点击事件无效，不影响其他事件的动画

        $("#div1").hide(3000);　　//注意由于jQuery.fx.off设置为了true,因此3000毫秒失效，相当于hide();

    });

});
```

### 15、jQuery.fx.interval　　//该属性设置动画的帧速，单位是毫秒，如果设置的时间越小，就越平滑。，属性出现的位置同样有影响范围

``` javascript
$(function(){

    jQuery.fx.interval = 1000;

    $("#div1").click(function(){　　

        $("#div1").hide(3000);　　　//jQuery.fx.interval设置为1000，也就是1秒钟，改变一次效果。　

    });

});
```

<!-- source: http://www.haorooms.com/post/jquery_toggle_dr -->
