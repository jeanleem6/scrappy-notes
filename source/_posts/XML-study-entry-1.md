---
title: XML Entry-1
date: 2017-08-27 17:10:01
tags: [xml]
---

``` xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<bookstore>
    <book category="COOKING" id="501">
        <title lang="en">Every Italian</title>
        <author>Giada De Laurentiis</author>
        <date>
            <year>2005</year>
            <month>05</month>
            <day>23</day>
        </date>
        <price>30.00</price>
    </book>
    <book category="CHILDREN" id="502">
        <title lang="en">Harry Potter</title>
        <author>J K. Rowling</author>
        <date>2005/10/01</date>
        <price>29.99</price>
    </book>
    <book category="WEB" id="503">
        <title lang="en">Learning XML</title>
        <author>Erik T. Ray</author>
        <year>2003</year>
        <price>39.95</price>
    </book>
</bookstore>
```

1. **基础知识整理：**

    - 必须有根元素
    - 元素标签对大小写敏感
    - 标签必须闭合
    - 元素必须备正确的嵌套
    - 标签属性必须加引号（单／双都行）

    > 在此极力推荐的理念是：**元数据** *[有关数据的数据]* 应当存储为属性（如上面代码中的`id="501"`，它仅仅是一个标识符，用于标识不同的书籍，它并不是数据的组成部分）；而**数据本身**应当存储为元素。

2. **避免使用属性的理由：**

    - 属性无法包含多重的值（元素可以）
    - 属性无法描述树结构（元素可以）
    - 属性不易扩展（为未来的变化）
    - 属性难以阅读和维护

    尽量使用元素来描述数据。而仅仅使用属性来提供与数据无关的信息。

3. **xml 文档的合法性验证：**

    通过 DTD 验证的 xml 文档是合法的 xml。访问[DTD教程](http://www.w3school.com.cn/dtd/index.asp)

    ``` dtd
    <!DOCTYPE note [
      <!ELEMENT note (to,from,heading,body)>
      <!ELEMENT to      (#PCDATA)>
      <!ELEMENT from    (#PCDATA)>
      <!ELEMENT heading (#PCDATA)>
      <!ELEMENT body    (#PCDATA)>
    ]>
    ```

    另一种 DTD 的代替者是 XML Schema。访问[XML Schema 教程](http://www.w3school.com.cn/schema/index.asp)

    ``` schema
    <xs:element name="note">

    <xs:complexType>
      <xs:sequence>
        <xs:element name="to"      type="xs:string"/>
        <xs:element name="from"    type="xs:string"/>
        <xs:element name="heading" type="xs:string"/>
        <xs:element name="body"    type="xs:string"/>
      </xs:sequence>
    </xs:complexType>

    </xs:element>
    ```

4. **给 xml 添加样式**

    ``` xml
    <?xml version="1.0" encoding="ISO-8859-1"?>
    <?xml-stylesheet type="text/xsl" href="simple.xsl"?> <!-- xslt，xml 的推荐样式文件 -->
    <?xml-stylesheet type="text/css" href="simple.css"?> <!-- css -->
    <breakfast_menu>
      <food>
        <name>Belgian Waffles</name>
        <price>$5.95</price>
        <description>
           two of our famous Belgian Waffles
        </description>
        <calories>650</calories>
      </food>
    </breakfast_menu>
    ```

    访问[XSLT 教程](http://www.w3school.com.cn/xsl/index.asp)。
