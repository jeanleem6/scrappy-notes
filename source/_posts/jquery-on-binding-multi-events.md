---
title: jquery on()方法绑定多个选择器，多个事件
date: 2017-06-14 08:17:32
tags: [jQuery]
---

这样一个需求，如果用`live()`方法实现的话 非常简单，容易理解。
``` javascript
$('nav li, #sb-nav li, #help li').live('click', function () {
    // code...
});
```

jquery在1.7版本后，建议大家用on方法代替之前的bind、live、delegate方法。
那上面一句如果用on的话，怎么写呢？

其实查看live源码就知道，live实际是委托doucment进行事件委派的。
按照这个思路，可以将on方法绑定到document即可。

``` javascript
$(document).on('click', '#header .fixed-feedback-bn, #sb-sec .feedback-bn', function () {
     // code...
});
```

还有一种情况，`on()`方法绑定**多个事件**，可以这样写：
``` javascript
$("table.planning_grid").on({
    mouseenter: function() {
        // Handle mouseenter...
    },
    mouseleave: function() {
        // Handle mouseleave...
    },
    click: function() {
        // Handle click...
    }
}, "td");
```

最后，用`on()`方法绑定**多个选择器**，多个事件则可以这样写：
``` javascript
$(document).on({
    mouseenter: function() {
        // Handle mouseenter...
    },
    mouseleave: function() {
        // Handle mouseleave...
    },
    click: function() {
        // Handle click...
    }
}, '#header .fixed-feedback-bn, #sb-sec .feedback-bn');
```

<!-- source: http://www.ghugo.com/jquery-on-method-multiple-event-selectors/ -->
