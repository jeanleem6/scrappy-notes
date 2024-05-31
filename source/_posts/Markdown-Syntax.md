---
title: Markdown Syntax
date: 2016-08-09 11:25:38
tags: [markdown]
---

![Markdown] [img1]

**NOTE:** This is Traditional Chinese Edition Document of Markdown Syntax. If you are seeking for English Edition Document. Please refer to [Markdown Syntax] [a1].

[img1]: markdown_icon.png (Markdown)
[a1]: http://daringfireball.net/projects/markdown/syntax (Markdown Syntax)


## 概述

### 哲学

Markdown的目标是实现［易读易写］。

不过最需要强调的便是它的可读性。一份使用Markdown格式撰写的文件应该可以直接以纯文字发布，并且看起来不会像是由许多标签或是格式指令所构成。Markdown语法受到一些既有text-to-HTML格式的影响，包括[Setext][a2]、[atx][a3]、[Textile][a4]、[reStructuredText][a5]、[Grutatext][a6] 和 [EtText][a7]，然而最大灵感来源其实是纯文字的电子邮件格式。

[a2]: http://docutils.sourceforge.net/mirror/setext.html (Setext)
[a3]: http://www.aaronsw.com/2002/atx/ (atx)
[a4]: http://textism.com/tools/textile/ (Textile)
[a5]: http://docutils.sourceforge.net/rst.html (reStructuredText)
[a6]: http://www.triptico.com/software/grutatxt.html (Grutatext)
[a7]: http://ettext.taint.org/doc/ (EtText)

<!-- more -->

因此Markdown的语法全由标点符号所组成，并经过严谨慎选，是为了让它们看起来就像所要表达的意思。像是在文字两旁加上星号，看起来就像\*强调\*。Markdown的清单看起来，嗯，就是清单。假如你有使用过电子邮件，区块引言看起来就真的像是引用一段文字。

### 行内HTML

Markdown的语法有个主要的目的：用来作为一种网路内容的*写作*用语言。

Markdown不是要来取代HTML，甚至也没有要和它相似，它的语法种类不多，只和HTML的一部分有关系，重点*不是*要创造一种更容易写作HTML文件的语法，我认为HTML已经很容易写了，Markdown的重点在于，它能让文件更容易阅读、编写。HTML是一种*发布*的格式，Markdown是一种*编写*的格式，因此，Markdown的格式语法只涵盖纯文字可以涵盖的范围。

不在Markdown涵盖范围之内的标签，都可以直接在文件里面用HTML撰写。不需要额外标注这是HTML或是Markdown；只要直接加标签就可以了。

只有区块元素——比如`<div>`、`<table>`、`<pre>`、`<p>`等标签，必须在前后加上空行，以利于内容区隔。而且这些（元素）的开始与结尾标签，不可以用tab或是空白来缩排。Markdown的产生器有智慧型判断，可以避免在区块标签前后加上没有必要的`<p>`标签。

举例来说，在Markdown文件里加上一段HTML表格：

``` html
    This is a regular paragraph.

    <table>
        <tr>
            <td>Foo</td>
        </tr>
    </table>

    This is another regular paragraph.
```

请注意，Markdown语法在HTML区块标签中将不会被进行处理。例如，你无法在HTML区块内使用Markdown形式的*强调*。

HTML的区段标签如`<span>`、`<cite>`、`<del>`则不受限制，可以在Markdown的段落、清单或是标题里任意使用。依照个人习惯，甚至可以不用Markdown格式，而采用HTML标签来格式化。举例说明：如果比较喜欢HTML的`<a>`或`<img>`标签，可以直接使用这些标签，而不用Markdown提供的链接或是影像标示语法。

HTML区段标签和区块标签不同，在区段标签的范围内，Markdown的语法是有效的。

### 特殊字元自动转换

在HTML文件中，有两个字元需要特殊处理：<和&。<符号用于起始标签&符号则用于标记HTML实体，如果你只是想要使用这些符号，你必须要使用实体的形式，像是`&lt;`和`&amp;`。

&符号其实很容易让写作网路文件的人感到困扰，如果你要打`［AT&T］`，你必须要写成`［AT&amp;T］`，还得转换网址内的` & `符号，如果你要链接到：

`http://images.google.com/images?num=30&q=larry+bird`

你必须要把网址转成：

`http://images.google.com/images?num=30&amp;q=larry+bird`

才能放到链接标签的href属性里。不用说也知道这很容易忘记，这也可能是HTML标准检查所检查到的错误中，数量最多的。

Markdown允许你直接使用这些符号，但是你要小心跳脱字元的使用，如果你是在HTML实体中使用`&`符号的话，它不会被转换，而在其他情形下，它则会被转换成`&amp;`。所以你如果要在文件中插入一个著作权的符号，你可以这样写：

`&copy;`

Markdown将不会对这段文字做修改，但是如果你这样写：

`AT&T`

Markdown就会将它转为：

`AT&amp;T`

类似的状况也会发生在`<`符号上，因为Markdown支援行内HTML，如果你是使用`<`符号作为HTML标签使用，那Markdown也不会对它做任何转换，但是如果你是写：

`4 < 5`

Markdown将会把它转换为：

`4 &lt; 5`

不过需要注意的是，code范围内，不论是行内还是区块，`<`和`&`两个符号都一定会被转换成HTML实体，这项特性让你可以很容易地用Markdown写HTML code（和HTML相对而言。在HTML语法中，你要把所有的`<`和`&`都转换为HTML实体，才能在HTML文件里面写出HTML code。）

## 区块元素

### 段落和换行

一个段落是由一个以上相连接的行句组成，而一个以上的空行则会切分出不同的段落（空行的定义是显示上看起来像是空行，便会被视为空行。比方说，若某一行只包含空白和tab，则该行也会被视为空行），一般的段落不需要用空白或断行缩排。

［一个以上相连接的行句组成］这句话其实暗示里Markdown允许段落内的强迫断行，这个特性和其他大部分的text-to-HTML格式不一样（包括 MovableType的［Convert Line Breaks］选项），其他的格式会把每个断行都转成`<br />`标签。

如果你真的想要插入`<br />`标签的话，在行尾加上两个以上的空白，然后按`enter`。

是的，这确实需要花比较多功夫来插入`<br />`，但是［每个换行都转换为`<br />`］的方法在Markdown中并不适合，Markdown中email式的区块引言和多段落的清单在使用换行来拍版的时候，不但更好用，还更好阅读。

### 标题

Markdown支援两类标题的语法，Setext和atx形式。

Setext形式是用底线的形式，利用=（最高阶标题）和-（第二阶标题），例如：

``` markdown
    This is an H1
    =============

    This is an H2
    -------------
```

任何数量的=和-都可以有效果。

Atx形式则是在行首插入1到6个 # ，各对应到标题1到6阶，例如：

``` markdown
    # This is an H1

    ## This is an H2

    ###### This is an H6
```

你可以选择性的［关闭］atx样式的标题，这纯粹只是美观用的，若失觉得这样看起来比较舒适，你就可以在行尾加上#，而行尾的#数量也不用和开头一样（行首的井字数量决定标题的阶数）：

``` markdown
    # This is an H1 #

    ## This is an H2 ##

    ### This is an H3 ######
```

### 区块引言

Markdown使用email形式的区块引言，如果你很熟悉如何在email信件中引言，你就知道怎么在Markdown文件中建立一个区块引言，那会看起来像是你强迫断行，然后在每行的最前面加上>：

``` markdown
    > This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
    > consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
    > Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
    >
    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
    > id sem consectetuer libero luctus adipiscing.
```

Markdown也允许你只在整个段落的第一行最前面加上>：

``` markdown
    > This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
    consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
    Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
    id sem consectetuer libero luctus adipiscing.
```

区块引言可以有阶层（例如：引言内的引言），只要根据层数加上不同数量的`>`：

``` markdown
    > This is the first level of quoting.
    >
    > > This is nested blockquote.
    >
    > Back to the first level.
```

引言的区块内也可以使用其他的Markdown语法，包括标题、清单、程式码区块等：

``` markdown
    > ## This is a header.
    >
    > 1.   This is the first list item.
    > 2.   This is the second list item.
    >
    > Here's some example code:
    >
    >     return shell_exec("echo $input | $markdown_script");
```

任何标准的文字编辑器都能简单地建立email样式的引言，例如BBEdit，你可以选取文字后然后从选单中选择增加引言阶层。

### 清单

Markdown支援有序清单和无序清单。

无序清单使用星号、加号或是减号作为清单标记：

``` markdown
    -   Red
    -   Green
    -   Blue
```

等同于：

``` markdown
    *   Red
    *   Green
    *   Blue
```

也等同于：

``` markdown
    +   Red
    +   Green
    +   Blue
```

有序清单则使用数字接着一个英文句点：

``` markdown
    1.  Bird
    2.  McHale
    3.  Parish
```

很重要的一点是，你在清单标记上使用的数字并不会影响输出的HTML解果，上面的清单所产生的HTML标记为：

``` html
    <ol>
    <li>Bird</li>
    <li>McHale</li>
    <li>Parish</li>
    </ol>
```

如果你的清单标记写成：

``` markdown
    1.  Bird
    1.  McHale
    1.  Parish
```

或甚至是：

``` markdown
    1. Bird
    1. McHale
    8. Parish
```

你都会得到完全相同的HTML输出。重点在于，你可以让Markdown文件的清单数字和输出的结果相同，或是你懒一点，你可以完全不用在意数字的正确性。

如果你使用懒惰的写法，建议第一个项目最好还是从［1.］开始，因为Markdown未来可能会支援有序清单的start属性。

清单项目标记通常是放在最左边，但是其实也可以缩排，最多三个空白，项目标记后面则一定要接着至少一个空白或tab。

要让清单看起来更漂亮，你可以把内容用固定的缩排整理好：

``` markdown
    -   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
        Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
        viverra nec, fringilla in, laoreet vitae, risus.
    -   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
        Suspendisse id sem consectetuer libero luctus adipiscing.
```

但是如果你很懒，那也不一定需要：

``` markdown
    -   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
    -   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.
```

如果清单项目间用空行分开，Markdown会把项目的内容在输出时用`<p>`标签抱起来，举例来说：

``` markdown
    -   Bird
    -   Magic
```

会被转换为：

``` html
    <ul>
    <li>Bird</li>
    <li>Magic</li>
    </ul>
```

但是这个：

``` markdown
    -   Bird

    -   Magic
```

会被转换为：

``` html
    <ul>
    <li><p>Bird</p></li>
    <li><p>Magic</p></li>
    </ul>
```

清单项目可以包含多个段落，每个项目下的段落都必须缩排4个空白或是一个tab：

``` markdown
    1.  This is a list item with two paragraphs. Lorem ipsum dolor
        sit amet, consectetuer adipiscing elit. Aliquam hendrerit
        mi posuere lectus.

        Vestibulum enim wisi, viverra nec, fringilla in, laoreet
        vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
        sit amet velit.

    2.  Suspendisse id sem consectetuer libero luctus adipiscing.
```

如果你每行都有缩排，看起来会好看很多，当然，再次地，如果你很懒惰，Markdown也允许：

``` markdown
    -   This is a list item with two paragraphs.

        This is the second paragraph in the list item. You're
    only required to indent the first line. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit.

    -   Another item in the same list.
```

如果要在清单项目内放进引言，那>就需要缩排：

``` markdown
    -   A list item with a blockquote:

        > This is a blockquote
        > inside a list item.
```

如果要放程式码区块的话，该区块就需要缩排两次，也就是8个空白或是两个tab：

``` markdown
    -   A list item with a code block:

            <code goes here>
```

当然，项目清单很可能会不小心产生，像是下面这样的写法：

``` markdown
    1986. What a great season.
```

换句话说，也就是在行首出现数字－句点－空白，要避免这样的情况，你可以在句点前面加上反斜线。

``` markdown
    1986\. What a great season.
```

### 程式码区块

和程式相关的写作或是标签语言原始码通常会有已经拍版好的程式码区块，通常这些区块我们并不希望它以一般段落文件的方式去拍版，而是按照原来的样式显示，Markdown会用`<pre>`和`<code>`标签来把程式码区块包起来。

要在Markdown中建立程式码区块很简单，只要简单地缩排4个空白或是1个tab就可以，例如，下面滴输入：

``` markdown
    This is a normal paragraph:

        This is a code block.
```

Markdown会转换成：

``` html
    <p>This is a normal paragraph:</p>

    <pre><code>This is a code block.
    </code></pre>
```

这个每行一阶的缩排（4个空白或是1个tab），都会被移除，例如：

``` markdown
    Here is an example of AppleScript:

        tell application "Foo"
            beep
        end tell
```

会被转换为：

``` html
    <p>Here is an example of AppleScript:</p>

    <pre><code>tell application "Foo"
        beep
    end tell
    </code></pre>
```

一个程式码区块会一直持续到没有缩排的那一行（或是文件结尾）。

在程式码区块里面，`&`、`<`和`>`会自动转成HTML实体，这样的方式让你非常容易使用Markdown插入范例用的HTML原始码，只需要复制贴上，再加上缩排就可以了，剩下的Markdown都会帮你处理，例如：

``` markdown
        <div class="footer">
            &copy; 2004 Foo Corporation
        </div>
```
会被转换为：

``` html
    <pre><code>&lt;div class="footer"&gt;
        &amp;copy; 2004 Foo Corporation
    &lt;/div&gt;
    </code></pre>
```

程式码区块中，一般的Markdown语法不会被转换，像是星号便只是星号，这表示你可以很容易地以Markdown语法撰写Markdown语法相关的文件。

### 分割线

你可以在一行中用三个或以上的星号、减号、底线来建立一个分割线，行内不能有其他东西。你也可以在星号中间插入空白。下面每种写法都可以建立分割线：

``` markdown
    - * *

    ***

    *****

    + - -

    ---------------------------------------
```

## 区段元素

### 链接

Markdown支援两种形式的链接语法：*行内*和*参考*两种形式。

不管是哪一种，链接的文字都是用 [方括号] 来标记。

要建立一个行内形式的链接，只要在方括号后面马上接着括号并插入网址链接即可，如果你还想要加上链接的title文字，只要在网址后面，用引号把title文字包起来即可，例如：

``` markdown
    This is [an example](http://example.com/ "Title") inline link.

    [This link](http://example.net/) has no title attribute.
```

会产生：

``` html
    <p>This is <a href="http://example.com/" title="Title">
    an example</a> inline link.</p>

    <p><a href="http://example.net/">This link</a> has no
    title attribute.</p>
```

如果你是要链接到同样主机的资源，你可以使用相对路径：

``` markdown
    See my [About](/about/) page for details.
```

参考形式的链接使用另外一个方括号接在链接文字的括号后面，而在第二个方括号里面要填入用以辨识链接的标签：

``` markdown
    This is [an example][id] reference-style link.
```

你也可以选择性地在两个方括号中间加上空白：

``` markdown
    This is [an example] [id] reference-style link.
```

接着，在文件的任意处，你可以把这个标签的链接内容定义出来：

``` markdown
    [id]: http://example.com/  "Optional Title Here"
```

链接定义的形式为：

* 方括号，里面输入链接的辨识用标签
* 接着一个冒号
* 接着一个以上的空白或tab
* 接着链接的网址
* 选择性地接着title内容，可以用单引号、双引号或是括弧包着

下面这三种链接的定义都是相同的：

``` markdown
    [foo]: http://example.com/  "Optional Title Here"
    [foo]: http://example.com/  'Optional Title Here'
    [foo]: http://example.com/  (Optional Title Here)
```

请注意：有一个已知的问题是Markdown.pl 1.0.1会忽略单引号包起来的链接title。

链接网址也可以用尖括号包起来：

``` markdown
    [id]: <http://example.com/>  "Optional Title Here"
```

你也可以把title属性放到下一行，也可以加一些缩排，网址太长的话，这样会比较好看：

``` markdown
    [id]: http://example.com/longish/path/to/resource/here
        "Optional Title Here"
```

网址定义只有在产生链接的时候用到，并不会直接出现在文件之中。

链接辨识标签可以有字母、数字、空白和标点符号，但是并*不*区分大小写，因此下面两个链接是一样的：

``` markdown
    [link text][a]
    [link text][A]
```

*预设的链接标签*功能让你可以省略指定链接标签，这种情形下，链接标签和链接文字会视为相同，要用预设链接标签只要在链接文字后面加上一个空的方括号，如果你要让"Google"链接到google.com，你可以简化成：

``` markdown
    [Google][]
```

然后定义链接内容：

``` markdown
    [Google]: http://google.com/
```

由于链接文字可能包含空白，所以这种简化的标签内也可以包含多个文字：

``` markdown
    Visit [Daring Fireball][] for more information.
```

然后接着定义链接：

``` markdown
    [Daring Fireball]: http://daringfireball.net/
```

链接的定义可以放在文件中的任何一个地方，我比较偏好直接放在链接出线段落的后面，你也可以把它放在文件最后面，就像是注解一样。

下面是一个参考式链接的范例：

``` markdown
    I get 10 times more traffic from [Google] [1] than from
    [Yahoo] [2] or [MSN] [3].

      [1]: http://google.com/        "Google"
      [2]: http://search.yahoo.com/  "Yahoo Search"
      [3]: http://search.msn.com/    "MSN Search"
```

如果改成用链接名称的方式写：

``` markdown
    I get 10 times more traffic from [Google][] than from
    [Yahoo][] or [MSN][].

      [google]: http://google.com/        "Google"
      [yahoo]:  http://search.yahoo.com/  "Yahoo Search"
      [msn]:    http://search.msn.com/    "MSN Search"
```

上面两种写法都会产生下面的HTML。

``` html
    <p>I get 10 times more traffic from <a href="http://google.com/"
    title="Google">Google</a> than from
    <a href="http://search.yahoo.com/" title="Yahoo Search">Yahoo</a>
    or <a href="http://search.msn.com/" title="MSN Search">MSN</a>.</p>
```

下面是用行内形式写的同样一段内容的Markdown文件，提供作为比较之用：

``` markdown
    I get 10 times more traffic from [Google](http://google.com/ "Google")
    than from [Yahoo](http://search.yahoo.com/ "Yahoo Search") or
    [MSN](http://search.msn.com/ "MSN Search").
```

参考式的链接其实重点不在于它比较好些，而是它比较好读，比较一下上面的范例，使用参考式的文章本身只有81个字元，但是用行内形式的链接却会增加到176个字元，如果是用纯HTML格式来写，会有234个字元，在HTML格式中，标签比文字还要多。

使用Markdown的参考式链接，可以让文件更像是浏览器最后产生的结果，让你可以把一些标记相关的资讯移到段落文字之外，你就可以增加链接而不让文章的阅读感觉被打断。

### 强调

Markdown使用星号（`*`）和底线（`_`）作为标记强调字词的符号，被`*`或`_`包围的字词会被转成用`<em>`标签包围，用两个`*`或`_`包起来的话，则会被转成`<strong>`，例如：

``` markdown
    *single asterisks*

    _single underscores_

    **double asterisks**

    __double underscores__
```

会转成：

``` html
    <em>single asterisks</em>

    <em>single underscores</em>

    <strong>double asterisks</strong>

    <strong>double underscores</strong>
```

你可以随便用你喜欢的样式，唯一的限制是，你用什么符号开启标签，就要用什么符号结束。

强调也可以直接插在文字中间：

``` markdown
    un*frigging*believable
```

但是如果你的 `*` 和 `_` 两边都有空白的话，它们就只会被当成普通的符号。

如果好在文字前后直接插入普通的星号或底线，你可以用反斜线：

``` markdown
    \*this text is surrounded by literal asterisks\*
```

### 程式码

如果要标记一小段行内程式码，你可以用反引号把它包起来（\`），例如：

``` markdown
    Use the `printf()` function.
```

会产生：

``` html
    <p>Use the <code>printf()</code> function.</p>
```

如果要在程式码区段内插入反引号，你可以用多个反引号来开启和结束程式码区段：

``` markdown
    ``There is a literal backtick (`) here.``
```

这段语法会产生：

``` html
    <p><code>There is a literal backtick (`) here.</code></p>
```

程式码区段的起始和结束端都可以放入一个空白，起始端后面一个，结束端前面一个，这样你就可以在区段的一开始就插入反引号：

``` markdown
    A single backtick in a code span: `` ` ``

    A backtick-delimited string in a code span: `` `foo` ``
```

会产生：

``` html
    <p>A single backtick in a code span: <code>`</code></p>

    <p>A backtick-delimited string in a code span: <code>`foo`</code></p>
```

在程式码区段内，`&`和`方括号`都会被转成HTML实体，这样会比较容易插入HTML原始码，Markdown会把下面这段：

``` markdown
    Please don't use any `<blink>` tags.
```

转为：

``` html
    <p>Please don't use any <code>&lt;blink&gt;</code> tags.</p>
```

你也可以这样写：

``` markdown
    `&#8212;` is the decimal-encoded equivalent of `&mdash;`.
```

以产生：

``` html
    <p><code>&amp;#8212;</code> is the decimal-encoded
    equivalent of <code>&amp;mdash;</code>.</p>
```

### 图片

很明显地，要在纯文字应用中设计一个［自然］的语法来插入图片是有一定难度的。

Markdown使用一种和链接很相似的语法来标记图片，同样也允许两种样式：*行内*和*参考*。

行内图片的语法看起来像是：

``` markdown
    ![Alt text](/path/to/img.jpg)

    ![Alt text](/path/to/img.jpg "Optional title")
```

详细叙述如下：

* 一个惊叹号`!`
* 接着一个方括号，里面放上图片的替代文字
* 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上 选择性的\`title\`文字。

参考式的图片语法则长得像这样：

``` markdown
    ![Alt text][id]
```

［id］是图片参考的名称，图片参考的定义方式则和链接参考一样：

``` markdown
    [id]: url/to/image  "Optional title attribute"
```

到目前为止，Markdown还没有办法指定图片的宽高，如果你需要的话，你可以使用普通的`<img>`标签。

---

## 其他

### 自动链接

Markdown支援比较简短的自动链接形式来处理网址和电子邮件信箱，只要是用方括号包起来，Markdown就会自动把它转成链接，链接的文字就和链接位置一样，例如：

``` markdown
    <http://example.com/>
```
Markdown会转为：

``` html
    <a href="http://example.com/">http://example.com</a>
```

自动的邮件链接也很类似，只是Markdown会先做一个编码转换的过程，把文字字元转成16进位码的HTML实体，这样的格式可以混淆一些不好的信箱地址收集机器人，例如：

``` markdown
    <address@example.com>
```

Markdown会转成：

``` html
    <a href="&#x6D;&#x61;i&#x6C;&#x74;&#x6F;:&#x61;&#x64;&#x64;&#x72;&#x65;
	&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;
	&#109;">&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;
	&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;</a>
```

在浏览器里面，这段字串会变成一个可以点击的［address@example.com］链接。

（这种作法虽然可以混淆不少的机器人，但并无发全部挡下来，不过这样也比什么都不做好些。无论如何，公开你的信箱终究会引来广告信件的。）

### 跳脱字元

Markdown可以利用反斜线来插入一些在语法中有其他意义的符号，例如：如果你想要用星号加在文字旁边的方式来做出强调效果（但不用`<em>`标签），你可以在星号的前面加上反斜线：

``` markdown
    \*literal asterisks\*
```

Markdown支援在下面这些符号前面加上反斜线来帮助插入普通的符号：

``` dash
    \   # 反斜线
    `   # 反引号
    -   # 星号
    _   # 底线
    {}  # 大括号
    []  # 方括号
    ()  # 括号
    #   # 井字号
    *   # 星号
    +   # 加号
    .   # 英文句点
    !   # 惊叹号
```

---
From: [http://markdown.tw/][from-1]

[from-1]: http://markdown.tw/
