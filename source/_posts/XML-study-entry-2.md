---
title: XML Entry-2
date: 2017-08-29 10:25:54
description: XML 用作数据存储媒介。本文讲解通过 Javascript 的 <code>XMLHttpRequest</code> 方法与服务器交换 xml 数据，解析 xml 文档；将 xml 文档转换为 DOM 🫱🫲👌
tags: [xml]
---

## XMLHttpRequest 对象

XMLHttpRequest 对象用于在后台与服务器交换数据。
它是开发者的梦想，因为它可以做以下事情：

- 在不重新加载页面的情况下更新网页
- 在页面已加载后从服务器请求数据
- 在页面已加载后从服务器接收数据
- 在后台向服务器发送数据

## 创建 XMLHttpRequest 对象

``` Javascript
xmlhttp = new XMLHttpRequest();
xmlhttp = new ActiveXObject("Microsoft.XMLHTTP"); //老版本IE（IE5 和 IE6）使用 ActiveX 对象
```

**下面的代码片段把 xml 文档解析到 xml DOM 对象中**

``` Javascript
function xmlHttpRequest(url) {
    var xmlhttp = null;
    try {
        xmlhttp = new XMLHttpRequest();
    } catch (e) {
        try {
            xmlhttp = new ActiveXObject('Microsoft.XMLHTTP');
        } catch (e) {
            alert('Your browser does not support XMLHTTP!');
            return;
        }
    }

    var xmlDoc;

    xmlhttp.onreadystatechange = state_Change;
    xmlhttp.open('GET', url, true);
    xmlhttp.send(null);
    xmlDoc = xmlhttp.responseXML;
    return xmlDoc;
}

function state_Change() {
    if (xmlhttp.readyState==4) {// 4 = "loaded"
        if (xmlhttp.status==200) {// 200 = OK
            // ...our code here...
        } else {
            alert("Problem retrieving XML data");
        }
    }
}
```

> 注释：`onreadystatechange` 是一个事件句柄。它的值 (state_Change) 是一个函数的名称，当 `XMLHttpRequest` 对象的状态发生改变时，会触发此函数。状态从 0 (uninitialized) 到 4 (complete) 进行变化。仅在状态为 4 时，我们才执行代码。

## 解析 xml 文档

``` Javascript
var xmlhttp = null;
if(window.XMLHttpRequest) {
    xmlhttp = new xmlHttpRequest();
} else {
    xmlhttp = new ActiveXObject('Microsoft.XMLHTTP');
}

xmlhttp.open('GET','book.xml',false);
xmlhttp.send(null);
xmlDoc = xmlhttp.responseXML;
```

**其它方法：**

``` Javascript
// 微软的 XML 解析，内建于IE5+
var xmlDoc=new ActiveXObject("Microsoft.XMLDOM"); //创建一个空的 XML 文档对象
xmlDoc.async="false"; //关闭异步加载，确保在文档完全加载之前解析器不会继续脚本的执行。
xmlDoc.load("note.xml"); //加载名为 "note.xml" 的 XML 文档
```

``` Javascript
// 在 Firefox 及其他浏览器中的 XML 解析器
var xmlDoc=document.implementation.createDocument("","",null);
xmlDoc.async="false";
xmlDoc.load("note.xml");
```

## 解析 XML 字符串

``` Javascript
txt="<bookstore><book>";
txt=txt+"<title>Everyday Italian</title>";
txt=txt+"<author>Giada De Laurentiis</author>";
txt=txt+"<year>2005</year>";
txt=txt+"</book></bookstore>";

if (window.DOMParser) {
    parser=new DOMParser();
    xmlDoc=parser.parseFromString(txt,"text/xml");
} else { //IE
    xmlDoc=new ActiveXObject("Microsoft.XMLDOM");
    xmlDoc.async="false";
    xmlDoc.loadXML(txt);
}
  ```

> 注：IE 使用 `loadXML()` 方法来解析 XML 字符串，而其他浏览器使用 `DOMParser` 对象。
> 注：`loadXML()` 方法用于加载字符串（文本），`load()` 用于加载文件。

## xml DOM

``` xml
<!-- xml 文档：cd_catalog.xml -->
<?xml version="1.0" encoding="ISO-8859-1"?>
<CATALOG>
    <CD>
        <TITLE>Empire Burlesque</TITLE>
        <ARTIST>Bob Dylan</ARTIST>
        <COUNTRY>USA</COUNTRY>
        <COMPANY>Columbia</COMPANY>
        <PRICE>10.90</PRICE>
        <YEAR>1985</YEAR>
    </CD>
    ...
</CATALOG>
```

``` html
<h1>CD List</h1>
<div id="showCD"></div>
```

``` Javascript
//加载 xml 文档
var xmlhttp,xmlDoc;
if (window.XMLHttpRequest) {// code for IE7+, Firefox, Chrome, Opera, Safari
    xmlhttp=new XMLHttpRequest();
} else {// code for IE6, IE5
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}

xmlhttp.open("GET","cd_catalog.xml",false);
xmlhttp.send();
xmlDoc=xmlhttp.responseXML;

//在 HTML 元素中显示 XML 数据

function displayCD() {
    var cds=xmlDoc.getElementsByTagName("CD");
    var cd_shelves = document.getElementById('showCD');
    var cd_list = document.createElement('ul');
    cd_list.setAttribute('class','cd_list');
    cd_shelves.appendChild(cd_list);

    var title,artist,price,cd_item,txt;

    for(var i=0,lens = cds.length; i<lens; i++) {
        cd_item = document.createElement('li');

        //获取 xml DOM 内容
        title=(cds[i].getElementsByTagName("TITLE")[0].childNodes[0].nodeValue);
        artist=(cds[i].getElementsByTagName("ARTIST")[0].childNodes[0].nodeValue);
        price=(cds[i].getElementsByTagName("PRICE")[0].childNodes[0].nodeValue);
        txt='<span class="title">' + title +
            '</span><span class="artist">' + artist +
            '</span><span class="price">'+ price + '</span>';

        //将 xml DOM 内容添加到 HTML 文档
        cd_item.innerHTML = txt;
        cd_list.appendChild(cd_item);
    }

}
```

``` css
/*CD List*/
.cd_list{margin:0 3.2%;}
.cd_list li{position:relative;margin-top:5px; overflow:hidden;}
.cd_list span{float:left;padding:10px 2% 1000px;margin-bottom:-990px;}
.cd_list .title{width:36%;background-color:#f0f8ff}
.cd_list .artist{width:31%;background-color:#fff0f8;font-style:italic;}
.cd_list .year{width:21%;background-color:#f0f1ff;text-align:center}
```

** Result:**
![XML DATA](1767C1AB-4580-46BF-B912-9FA31A30B592.png)
