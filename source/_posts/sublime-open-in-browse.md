---
title: sublime text 3 实现浏览器预览
date: 2017-06-13 08:07:54
tags: [sublime]
---

Tools>build system>new build system
``` bash
    {
      "cmd": ["/Applications/Google Chrome.app/Contents/MacOS/Google Chrome", "$file"],
      "selector": ["text.html"]
    }
```
保存为browse.sublime-build，然后写一个html。mac上用`command+b`,windows上用`win+b`
