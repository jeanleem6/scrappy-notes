---
title: javascript 用户代理(userAgent)
date: 2017-07-13 17:45:09
description: 💬聊一聊 javascript 中的 <code>userAgent</code> ...💬
tags: [javascript]
---

强调一下，**用户代理检测是**客户端检测的**最后一个选择**。只要可能，都**应该优先采用能力检测和怪癖检测**。用户代理检测一般适用以下情形：

- 不能直接准确地使用能力检测或怪癖检测。例如，某些浏览器实现了为将来功能预留的存根(stub)函数。在这种情况下，仅测试相应的函数是否存在还得不到足够的信息。
- 同一款浏览器在不同平台下具备不同的能力。这时候，可能就有必要确定浏览器位于哪个平台下。
- 为了跟踪分析等目的需要知道确切的浏览器。

``` javascript
// 引擎、浏览器版本检测
var client = function() {

    var engine = {
        //呈现引擎
        ie: 0,
        gecko: 0,
        webkit: 0,
        khtml: 0,
        opera: 0,
        // 具体的版本
        ver: null
    };
    var browser = {
        // 浏览器
        ie: 0,
        firefox: 0,
        safari: 0,
        kong: 0,
        opera: 0,
        chrome: 0,
        // 具体的版本
        ver: null
    };

    var ua = navigator.userAgent;

    if (window.opera) {
        engine.ver = browser.ver = window.opera.version();
        engine.opera = browser.opera = parseFloat(engine.ver);
    } else if (/AppleWebKit\/(\S+)/.test(ua)) {
        engine.ver = RegExp['$1'];
        engine.webkit = parseFloat(engine.ver);

        // 确定是 safari 还是 chrome
        if (/Chrome\/(\S+)/.test(ua)) {
            browser.ver = RegExp['$1'];
            browser.chrome = parseFloat(browser.ver);
        } else if (/Version\/(\S+)/.test(ua)) {
            browser.ver = RegExp['$1'];
            browser.safari = parseFloat(browser.ver);
        } else {
            // 近似地确定版本号
            var safariVersion = 1;

            if (engine.webkit < 100) {
                safariVersion = 1;
            } else if (engine.webkit < 312) {
                safariVersion = 1.2;
            } else if (engine.webkit < 412) {
                safariVersion = 1.3;
            } else {
                safariVersion = 2;
            }

            browser.safari = browser.ver = safariVersion;
        }

    } else if (/KHTML\/(\S+)/.test(ua) || /Konqueror\/([^;]+)/.test(ua)) {
        engine.ver = browser.ver = RgeExp['$1'];
        engine.khtml = browser.kong = parseFloat(engine.ver);
    } else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)) {
        engine.ver = RegExp['$1'];
        engine.gecko = parseFloat(engine.ver);

        if (/Firefox\/(\S+)/.test(ua)) {
            browser.ver = RegExp['$1'];
            browser.firefox = parseFloat(browser.ver);
        }

    } else if (/MSIE ([^;]+)/.test(ua)) {
        engine.ver = browser.ver = RegExp['$1'];
        engine.ie = browser.ie = parseFloat(engine.ver);
    }

    return {
        engine: engine,
        browser: browser
    };
}();

// 引擎版本
console.log(client.engine.ver);
// 浏览器版本
console.log(client.browser.ver);
```

> 还有一个**平台检测**功能此处未实现，待后续更新…
