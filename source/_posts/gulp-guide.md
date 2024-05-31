---
title: 前端构建工具gulp入门教程
date: 2016-08-19 08:43:34
tags: [javascript, gulp]
---

**本文假设你之前没有用过任何任务脚本（task runner）和命令行工具，一步步教你上手Gulp。不要怕，它其实很简单，我会分为五步向你介绍gulp并帮助你完成一些惊人的事情。那就直接开始吧。**


## 第一步：安装Node
首先，最基本也最重要的是，我们需要搭建node环境。访问[http://nodejs.org] [a1]，然后点击大大的绿色的install按钮，下载完成后直接运行程序，就一切准备就绪。npm会随着安装包一起安装，稍后会用到它。

[a1]: http://nodejs.org/

## 第二步：使用命令行
也许现在你还不是很了解什么是命令行——OS X中的*终端*（Terminal），windows中的*命令提示符*（Command Prompt），但很快你就会知道。它看起来没那么简单，但一旦掌握了它的窍门，就可以很方便的执行很多命令行程序，比如[Sass] [a2]，[Yeoman] [a3]和[Git] [a4]等，这些都是非常有用的工具。

[a2]: http://sass-lang.com/
[a3]: http://yeoman.io/
[a4]: http://git-scm.com/

<!-- more -->

> 如果你很熟悉命令行，直接跳到步骤四。

为了确保Node已经正确安装，我们执行几个简单的命令。

``` bash
    $ node -v
```

回车（Enter），如果正确安装的话，你会看到所安装的Node的版本号，接下来看看npm。

``` bash
     npm -v
```

这同样能得到npm的版本号。

如果这两行命令没有得到返回，可能node就没有安装正确，尝试重启下命令行工具，如果还不行的话，只能回到第一步进行重装。

## 第三步：定位到项目
现在，我们已经大致了解了命令行并且知道如何简单使用它，接下来只需要两个简单的命令就能定位到文件目录并看看目录里都有些什么文件。

* 定位到目录

	``` bash
	    cd ~/path/filename  # OS X
	    cd d:/www/my-project  # windows
	```

* 列出文件列表

	``` bash
        ls  # OS X
        dir # windows
	```
> 注意OS X与windows之间的区别，建议多敲敲这两个命令，了解文件系统并知道文件都在哪里。

习惯使用了这两个命令后，就要进入我们的项目目录，这个目录各不相同，举个例子，这是我进入我项目目录的命令：

``` bash
    cd /Applications/XAMPP/xamppfiles/htdocs/my-project
```

成功进入项目目录后，我们开始安装gulp。

## 第四步：安装gulp
我们已经知道如何使用命令行，现在尝试点新的东西，认识npm然后安装gulp。

> *NPM*是基于命令行的node包管理工具，它可以将node的程序模块安装到项目中，在它的[官网] [a5]中可以查看和搜索所有可用的程序模块。作为练习你可以搜索gulp试试看。

[a5]: http://npmjs.org/

在命令行中输入

``` bash
    npm install -g gulp
```

* `npm` 基于命令行的package（包）管理**工具**
* `install` npm工具的一个指令－－**安装**
* `-g` 表示安装到**全局环境**（可选项），以便任何项目都能使用它
* 最后，`gulp`是将要安装的**package（包）**的名字

> 如果你在安装模块过程中遇到报错提示**目录没有写入权限**，你可以在该命令最前面加上`sudo`，但是不建议，因为这可能导致后续出现其它问题。更多解决方法可访问[Fixing npm Permissions] [a6]。

[a6]: https://docs.npmjs.com/getting-started/fixing-npm-permissions

运行时注意查看命令行有没有错误信息，安装完成后，你可以使用下面的命令查看*gulp的版本号*以确保gulp已经被正确安装。

``` bash
    gulp -v
```

接下来，我们需要将gulp安装到项目本地

``` bash
    cd ~/path/project  # 切换到项目目录(如果当前不在项目目录)
    npm install --save-dev gulp
```

这里，我们使用`--save-dev`来更新**package.json**文件，更新**devDependencies**值，以表明项目需要*依赖*gulp。

Dependencies可以向其他参与项目的人指明项目在开发环境和生产环境中的node模块依懒关系，想要更加深入的了解它可以看看[package.json文档][a7]。

[a7]: https://docs.npmjs.com/files/package.json#dependencies

现在，gulp已经安装好了，下一步将设置我们的gulp文件。差不多快要完成✅了！

## 第五步：新建Gulpfile文件，运行gulp

安装好gulp后我们需要告诉它要为我们执行哪些任务，首先，我们自己需要弄清楚项目需要哪些任务。假定我们已经设计好如下任务：

* 检查Javascript
* 编译Sass（或Less之类的）文件
* 合并Javascript
* 压缩并重命名合并后的Javascript

**安装依赖组件**

``` bash
    npm install gulp-jshint gulp-sass gulp-concat gulp-uglify gulp-rename --save-dev
```

提醒下，如果以上命令提示权限错误，需要添加sudo再次尝试。

**新建gulpfile文件**

现在，组件都可以为我们所用，可以开始写gulpfile文件让gulp来完成我们之前设计好的任务。

gulp只有*五个方法*： **task**，**run**，**watch**，**src**，和**dest**，在项目根目录新建一个js文件并命名为`gulpfile.js`，把下面的代码粘贴进去：

**gulpfile.js**

``` javascript
    // 引入 gulp
    var gulp = require('gulp');

    // 引入组件
    var jshint = require('gulp-jshint');
    var sass = require('gulp-sass');
    var concat = require('gulp-concat');
    var uglify = require('gulp-uglify');
    var rename = require('gulp-rename');

    // 检查脚本
    gulp.task('lint', function() {
      return gulp.src('js/*.js')
          .pipe(jshint())
          .pipe(jshint.reporter('default'));
    });

    // 编译Sass
    gulp.task('sass', function() {
      return gulp.src('scss/*.scss')
          .pipe(sass())
          .pipe(gulp.dest('dist/css'));
    });

    // 合并，压缩文件
    gulp.task('scripts', function() {
      return gulp.src('js/*.js')
          .pipe(concat('all.js'))
          .pipe(gulp.dest('dist'))
          .pipe(rename('all.min.js'))
          .pipe(uglify())
          .pipe(gulp.dest('dist/js'));
    });

    // 监听文件变化
    gulp.task('watch', function() {
        gulp.watch('js/*.js', ['lint', 'scripts']);
        gulp.watch('scss/*.scss', ['sass']);
    });

    // 默认任务
    gulp.task('default', ['lint', 'sass', 'scripts', 'watch']);
```

现在，分段解释下这段代码。

### 引入组件

``` javascript
    var gulp = require('gulp');

    var jshint = require('gulp-jshint');
    var sass = require('gulp-sass');
    var concat = require('gulp-concat');
    var uglify = require('gulp-uglify');
    var rename = require('gulp-rename');
```

这一步，我们引入了核心的gulp和其他依赖组件，接下来，分开创建`lint`, `sass`, `scripts` 和 `default`这四个不同的任务。

### Lint任务

``` javascript
    gulp.task('lint', function() {
        gulp.src('js/*.js')
            .pipe(jshint())
            .pipe(jshint.reporter('default'));
    });
```

Lint任务会检查`js/`目录下的js文件有没有报错或警告。

### Sass任务

``` javascript
    gulp.task('sass', function() {
        gulp.src('scss/*.scss')
            .pipe(sass())
            .pipe(gulp.dest('dist/css'));
    });
```

**sass**任务会编译`scss/`目录下的scss文件，并把编译完成的css文件保存到`dist/css`目录中。

### Scripts 任务

``` javascript
    gulp.task('scripts', function() {
        gulp.src('js/*.js')
            .pipe(concat('all.js'))
            .pipe(gulp.dest('dist/js'))
            .pipe(rename('all.min.js'))
            .pipe(uglify())
            .pipe(gulp.dest('dist/js'));
    });
```

**scripts**任务会合并`js/`目录下所有的js文件并输出到`dist/js`目录，然后gulp会重命名、压缩合并的文件，也输出到`dist/js`目录。

### Watch任务

``` javascript
    gulp.task('watch', function() {
        gulp.watch('js/*.js', ['lint', 'scripts']);
        gulp.watch('scss/*.scss', ['sass']);
    });
```

**watch**任务用于监听指定目录文件的变化。当你书写代码或修改文件时，`gulp.watch()`方法会监听到这些变化并自动运行回调定义的其他任务，所以我们不用每次都切换到命令行工具去执行gulp命令。

### Default任务

``` javascript
    gulp.task('default', ['lint', 'sass', 'scripts', 'watch']);
```

最后，我们通过**default**任务来分组索引其它任务，在命令行中输入（不带参数的）`gulp`命令后，将执行**default**任务中定义的所有任务。

现在，回到命令行，可以直接运行gulp任务了。

``` bash
    gulp
```

这将执行定义的default任务，换言之，这和以下的命令式同一个意思

``` bash
    gulp default
```

当然，我们可以运行在gulpfile.js中定义的任意任务，比如，现在运行sass任务：

``` bash
    gulp sass
```

Pretty cool, eh?

## 结束语

现在已经做到了设置gulp任务然后运行他们，现在再回顾下之前学习的。
1. 学习了安装Node环境
2. 学习了简单使用命令行
3. 学习了用命令行进入项目目录
4. 学习了使用npm和安装gulp
5. 学习了如何运行gulp任务

另外，有一些参考资源供进一步学习：
1. [npm上的gulp组件] [a3]
2. [gulp的Github主页] [a4]
3. [官方package.json文档] [a5]

[a3]: https://npmjs.org/search?q=gulpplugin
[a4]: https://github.com/wearefractal/gulp
[a5]: https://npmjs.org/doc/json.html

---

From: [http://travismaynard.com/writing/getting-started-with-gulp] [a6]

[a6]: http://travismaynard.com/writing/getting-started-with-gulp
