---
title: iOS 微信 音频 视频自动播放
date: 2017-11-15 15:27:04
description: iPhone 中的音频、视频无法自动播放？⏯️本文旨在解决 iPhone 微信中音频/视频自动播放的问题▶️
tags: [ios,autoplay]
---

iPhone手机音频、视频无法自动播放？

通过下面的方式可以解决，在iPhone手机微信中正常自动播放。

必须在微信Weixin JSAPI的WeixinJSBridgeReady才能生效，猜测微信接口做了处理~

测试了90%的iPhone机型，大部分直接调用audio的play方法就可以自动播放了，但是一些奇葩iPhone机不可以。

另外，微信中不设置静音可以自动播放，但safari中不能。

``` html
<audio preload="preload" controls id="car_audio" src="http://media.xitaoinfo.com/ei_zamenjiehunba.mp3" loop></audio>
<video id="video" controls preload="auto" mediagroup="myVideoGroup" poster="http://media.w3.org/2010/05/sintel/poster.png" muted autoplay playsinline>
      <source id="mp4" src="http://media.w3.org/2010/05/sintel/trailer.mp4" type="video/mp4">
      <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
      <source id="ogv" src="http://media.w3.org/2010/05/sintel/trailer.ogv" type="video/ogg">
      <p>Your user agent does not support the HTML5 Video element.</p>
</video>
<!-- 必须加在微信api资源 -->
<script src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>
<script>
     //一般情况下，这样就可以自动播放了，但是一些奇葩iPhone机不可以
     document.getElementById('car_audio').play();
    //必须在微信Weixin JSAPI的WeixinJSBridgeReady才能生效
    document.addEventListener("WeixinJSBridgeReady", function () {
        document.getElementById('car_audio').play();
        document.getElementById('video').play();
    }, false);
</script>
```

@Nokey 提问：最近又发现一个问题，Android不能同时播放两个音频? @李猜猜回答：因为ready只会触发一次，所以不能播放多个音频。但是如果需要播放多个音频，其实只要调用一下eixinJSBridge进行包裹即可。 示例代码如下

``` javascript
function playAudio() {
    if (setting.autoplay) {
        if (window.WeixinJSBridge) {
            WeixinJSBridge.invoke('getNetworkType', {}, function (e) {
                audio.play();
            }, false);
        } else {
            document.addEventListener("WeixinJSBridgeReady", function () {
                WeixinJSBridge.invoke('getNetworkType', {}, function (e) {
                    audio.play();
                });
            }, false);
        }
        audio.play();
    } else {
        audio.pause();
    }
    return false;
}
```

reference: [https://www.w3ctech.com/topic/1165]()
