---
title: Get Sizes
date: 2016-09-14 08:53:32
tags: [javascript]
---

## Window Size
How can I get `windowWidth`, `windowHeight`, `pageWidth`, `pageHeight`, `screenWidth`, `screenHeight`, `pageX`, `pageY`, `screenX`, `screenY` which will work in all major browsers?

![getSize](about-js-get-size.jpg)

## Element Size

每个HTML元素都有下列属性：

|  |  |  |
|- - -|- - - |- - - |
|offsetWidth | clientWidth | scrollWidth |
| offsetHeight | clientHeight | scrollHeight |
| offsetLeft | clientLeft | scrollLeft |
| offsetTop | clientTop | scrollTop |

1. *clientHeight* 和 *clientWidth* 用于描述元素**内尺寸**，是指【元素内容+内边距】大小，不包括边框（**IE下实际包括**）、外边距、滚动条部分

2. *offsetHeight*和*offsetWidth*用于描述元素**外尺寸**，是指【元素内容+内边距+边框】，不包括外边距和滚动条部分

3. *clientTop* 和 *clientLeft* 返回内边距的边缘和边框的外边缘之间的水平和垂直距离，也就是【左、上边框宽度】

4. *offsetTop* 和 *offsetLeft* 表示该元素的左上角（边框外边缘）与已定位的父容器（*offsetParent*对象）左上角的距离

5. *offsetParent*对象是指元素最近的定位（relative,absolute）祖先元素，递归上溯，如果没有祖先元素是定位的话，返回null

6. *scrollWidth* 和 *scrollHeight* 是元素的【内容区域+内边距+溢出尺寸】，当内容正好和内容区域匹配没有溢出时，这些属性与 *clientWidth* 和 *clientHeight* 相等

7. *scrollLeft* 和 *scrollTop* 是指【元素滚动条位置】，它们是**可写**的

<!-- more -->
