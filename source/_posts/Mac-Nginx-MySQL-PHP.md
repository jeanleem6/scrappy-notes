---
title: Mac下使用Homebrew安装ST/Nginx/MySQL/PHP
date: 2016-11-21 08:43:11
tags: [Mac, nginx, mysql, php, server]
---

## 使用homebrew-cask安装sublime

先安装cask, 使用cask可以安装一些应用程序，如QQ，迅雷，谷歌浏览器等，功能和App store差不多，个人觉得这个更好管理

``` bash
    brew cask # 没有安装cask会自动安装，已经安装cask的，会跳出cask命令列表
```


``` bash
    # Cask 常用命令
    brew cask search        #列出所有可以被安装的软件
    brew cask search sublime    #查找所有和sublime相关的应用
    brew cask list          #列出所有通过cask安装的软件
    brew cask info sublime-text  #查看 sublime 的信息
    brew cask install sublime-text  # 安装sublime
    brew cask uninstall sublime-text   #卸载sublime
```

<!-- more -->

通常我们是不知道软件的全称的，比如安装sublime,我们可以先使用`brew cask serach`搜索：

``` bash
    brew cask search sublime
    ==> Exact match
    caskroom/cask/sublime
    ==> Partial matches
    caskroom/cask/sublime-text               caskroom/cask/sublime-text
```

从上面我们可以看出，要安装的sublime全称是sublime-text,我们使用`brew cask install sublime-text`来安装它

``` bash
    brew cask install sublime-text
```

先给sublime text 3安装Package Control, 按住`` control + ` ``,在弹出的命令行输入：

``` bash
    import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

### 给sublime换主题

然后`command + shift + p`,打开Package Control,输入`install`,选择`Package Control:Install Package`回车，在跳出的命令行输入选择`Material Theme`安装，然后按下图启用

![sublime Theme](sublime_theme.png)

## 安装Mysql

先查找下mysql

``` bash
    ➜  ~ brew search mysql
    automysqlbackup            mysql-cluster              mysql-sandbox
    mysql                      mysql-connector-c          mysql-search-replace
    mysql++                    mysql-connector-c++        mysqltuner
    homebrew/php/php53-mysqlnd_ms            homebrew/versions/mysql56
    homebrew/php/php54-mysqlnd_ms            Caskroom/cask/mysql-connector-python
    homebrew/php/php55-mysqlnd_ms            Caskroom/cask/mysqlworkbench
    homebrew/php/php56-mysqlnd_ms            Caskroom/cask/navicat-for-mysql
    homebrew/versions/mysql55                Caskroom/cask/sqlpro-for-mysql
```

看一下mysql的版本信息

``` bash
    ➜  ~ brew info mysql
    mysql: stable 5.7.16 (bottled)
    Open source relational database management system
    # 下面信息省略
```

安装MySql

``` bash
    brew install mysql
```

设置MySql开机启动

``` bash
    mkdir -p ~/Library/LaunchAgents    # 首先确认该目录是否存在，若已经存在不用执行本命令
    ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents
    launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```

启动MySql服务

``` bash
    mysql.server start
```

**错误修复**

如果在启动过程中出现如下错误：`ERROR! The server quit without updating PID file` ，使用以下方法修复。

``` bash
    sudo chmod -R 755 /usr/local/var/mysql
    rm -Rf /usr/local/var/mysql/Your-Machine-Name.local.err
```

> 注:将`Your-Machine-Name`替换为机器名称。

MySql安全性设置

``` bash
    mysql_secure_installation

    Set root password? [Y/n] Y
    Remove anonymous users? [Y/n] Y
    Disallow root login remotely? [Y/n] Y
    Remove test database and access to it? [Y/n] Y
    Reload privilege tables now? [Y/n] Y
```

好了，进入mysql看下

``` bash
    ➜  ~ mysql -u root -p
    Enter password:
    Welcome to the MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 4
    Server version: 5.7.16 Homebrew

    Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

    mysql> show databases;
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | mysql              |
    | performance_schema |
    | sys                |
    +--------------------+
    4 rows in set (0.00 sec)

    mysql>
```

使用Homebrew卸载MySql

``` bash
    brew uninstall mysql
    brew cleanup
    launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
    rm -Rf ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```

## 安装php

---

### `* 2019.03.01 updated *`

> Warning!
> If you have existing PHP installations via Brew, you need to first cleanup your setup with our Upgrading Homebrew guide before continuing with this section.

Up until the end of March 2018, all PHP related brews were handled by `Homebrew/php` tab, but that has been deprecated, so now we use what's available in the `Homebrew/core` package. This should be a better maintained, but is a much less complete, set of packages.

Both **PHP 5.6** and **PHP 7.0** has been deprecated and removed from Brew [because they are out of support](http://php.net/supported-versions.php), and while it's **not recommended for production**, there are legitimate reasons to test these unsupported versions in a development environment.

Remember only **PHP 7.1 through 7.3** are officially supported by Brew so if you want to install **PHP 5.6** or **PHP 7.0** you will need to add this tap:

``` bash
$ brew tap exolnet/homebrew-deprecated
```

We will proceed by installing various verions of PHP and using a simple script to switch between them as we need. Feel free to exclude any versions you don't want to install.

``` bash
$ brew install php@5.6
$ brew install php@7.0
$ brew install php@7.1
$ brew install php@7.2
$ brew install php@7.3
```

The first one will take a little bit of time as it has to install a bunch of brew dependencies. Subsequent PHP versions will install faster.

> Note:
> You no longer have to `unlink` each version between installing PHP versions as they are not linked by default

Also, you may have the need to tweak configuration settings of PHP to your needs. A common thing to change is the memory setting, or the `date.timezone` configuration. The `php.ini` files for each version of PHP are located in the following directories:

``` bash
/usr/local/etc/php/5.6/php.ini
/usr/local/etc/php/7.0/php.ini
/usr/local/etc/php/7.1/php.ini
/usr/local/etc/php/7.2/php.ini
/usr/local/etc/php/7.3/php.ini
```

Let's switch back to the first PHP version now:

``` bash
$ brew unlink php@7.3 && brew link --force --overwrite php@5.6
```

> Info:
> At this point, I strongly recommend closing **ALL your terminal tabs and windows**. This will mean opening a new terminal to continue with the next step. This is strongly recommended because some really strange path issues can arise with existing terminals (trust me, I have seen it!).

Quick test that we're in the correct version:

``` bash
php -v

PHP 5.6.39 (cli) (built: Dec  7 2018 08:27:47)
Copyright (c) 1997-2016 The PHP Group
Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
    with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies
```

---


安装php之前，请先用brew tap命令引入第三方的php库，brew仓库中没有php的安装包。
``` bash
    brew update # 安装软件前都要习惯的更新下brew源
    brew tap homebrew/dupes
    brew tap josegonzalez/homebrew-php
```

现在`brew search php`就可以了，出来一堆版本的php，我们就安装php5.6版本吧。
可以先`brew options php56`看看你安装的时候要哪些选项，我选择了下面这些,因为后面我们会用nginx作为反向代理，所以就不要用--with-apache选项了，也不要添加--without-fpm选项

``` bash
    brew install php56 --with-imap --with-tidy --with-debug --with-pgsql --with-mysql --with-fpm
```

单独安装 php 扩展
``` bash
    brew install php56-apcu php56-intl php56-redis php56-uuid php56-zookeeper
        php56-thrift php56-solr php56-ssh2 php56-gmagick php56-kafka php56-libevent
        php56-imagick php56-msgpack php56-geoip php56-mcrypt php56-swoole
        php56-scrypt php56-xdebug php56-yaf php56-yaml php56-xhprof
        php56-memcache php56-memcached php56-gearman
```

由于Mac自带了php和php-fpm，因此需要添加系统环境变量PATH来替代自带PHP版本,我们用的是zsh,所以放进.zshrc中,如果你用的shell是bash,那么可以把下面的信息写入到`~/.bash_profile`文件中，如果这个文件没有，你自己建一个就行。

``` bash
    echo 'export PATH="$(brew --prefix php56)/bin:$PATH"' >> ~/.zshrc  #for php
    echo 'export PATH="$(brew --prefix php56)/sbin:$PATH"' >> ~/.zshrc  #for php-fpm
    echo 'export PATH="/usr/local/bin:/usr/local/sbib:$PATH"' >> ~/.zshrc #for other brew install soft
    source ~/.zshrc
```
设置开机启动php
``` bash
    mkdir -p ~/Library/LaunchAgents
    cp /usr/local/opt/php56/homebrew.mxcl.php56.plist ~/Library/LaunchAgents/
    launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.php56.plist
```

> 注意：如果要搭建帝国cms，请安装 `php56`，因为帝国cms 7.2版及之前的版本不支持 `php7`，但是 `php7` 之前的版本都可以。

测试下效果

``` bash
    # brew安装的php
    ➜  ~ php -v
    PHP 7.0.12 (cli) (built: Oct 24 2016 00:06:38) ( NTS DEBUG )
    Copyright (c) 1997-2016 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies

    # brew安装的php-fpm
    ➜  ~ php-fpm -v
    PHP 7.0.12 (fpm-fcgi) (built: Oct 24 2016 00:06:45) (DEBUG)
    Copyright (c) 1997-2016 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies

    # Mac自带的php, 我以前的项目有些依赖不支持php7,所以这个我是留着的，随时切换使用
    ➜  ~ /usr/bin/php -v
    PHP 5.6.24 (cli) (built: Aug  8 2016 16:58:37)
    Copyright (c) 1997-2016 The PHP Group
    Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies

    # Mac自带php-fpm
    ➜  ~ /usr/sbin/php-fpm -v
    PHP 5.6.24 (fpm-fcgi) (built: Aug  8 2016 16:58:54)
    Copyright (c) 1997-2016 The PHP Group
    Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
    ➜  ~
```

下面先来看下`php-fpm`的配置文件，路径在`/usr/local/etc/php/7.0/php-fpm.conf`，大家应该都猜的到。我们主要看下pid和log文件会放在哪里

``` bash
     13 [global]
     14 ; Pid file
     15 ; Note: the default prefix is /usr/local/var
     16 ; Default Value: none
     17 ;pid = run/php-fpm.pid
     18
     19 ; Error log file
     20 ; If it's set to "syslog", log is sent to syslogd instead of being written
     21 ; in a local file.
     22 ; Note: the default prefix is /usr/local/var
     23 ; Default Value: log/php-fpm.log
     24 ;error_log = log/php-fpm.log
```

自己看下上面的信息，去掉17行和24行前面的分号,使用`php-fpm -t`测试下配置是否正确,按提示信息是不管它也可以，默认就是在`/usr/local/var`路径下的，不过还是设置下吧；

``` bash
    ➜  7.0 php-fpm -t
    [24-Oct-2016 11:20:31] NOTICE: configuration file /usr/local/etc/php/7.0/php-fpm.conf test is successful
```

php-fpm的一些管理:

``` bash
    #测试php-fpm配置
    php-fpm -t

    #启动php-fpm
    php-fpm -D

    #关闭php-fpm
    kill -INT `cat /usr/local/var/run/php-fpm.pid`

    #重启php-fpm
    kill -USR2 `cat /usr/local/var/run/php-fpm.pid`

    #也可以用上文提到的brew命令来管理php-fpm
    brew services start|stop|restart php70

    #还可以用这个命令来管理php-fpm
    php70-fpm start|stop|restart
```

启动php-fpm之后，确保它正常运行监听9000端口：

``` bash
    ➜  ~ lsof -Pni4 | grep LISTEN | grep php
    php-fpm   18381  zjp    8u  IPv4 0xbca78421d968b30f      0t0  TCP 127.0.0.1:9000 (LISTEN)
    php-fpm   18382  zjp    0u  IPv4 0xbca78421d968b30f      0t0  TCP 127.0.0.1:9000 (LISTEN)
    php-fpm   18383  zjp    0u  IPv4 0xbca78421d968b30f      0t0  TCP 127.0.0.1:9000 (LISTEN)
```

### 卸载php

``` bash
brew uninstall php70
brew cleanup
xcode-select --install # An "install" window will appear. Click "yes" on all the things.
brew install php70
```

---
`* 2019.03.01 updated *`

- Uninstall your existing Homebrew PHP version if it is the latest release from php.net
``` bash
brew uninstall --force php56
```

- Update your formulas:
``` bash
brew update
```

- Fix any tap link errors:
``` bash
brew tap --repair
```

---

## 安装Nginx

查找nginx

``` bash
    brew search nginx
```

看下信息

``` bash
    brew info nginx
```

安装

``` bash
    brew install nginx
```

安装信息记录下，用的到：

``` bash
    ➜  ~ brew install nginx
    ==> Auto-updated Homebrew!
    Updated 1 tap (homebrew/core).
    ==> New Formulae
    gitless
    ==> Updated Formulae
    fzf                                                                              gammu

    ==> Downloading https://homebrew.bintray.com/bottles/nginx-1.10.2.sierra.bottle.tar.gz
    ######################################################################## 100.0%
    ==> Pouring nginx-1.10.2.sierra.bottle.tar.gz
    ==> Using the sandbox
    ==> Caveats
    Docroot is: /usr/local/var/www

    The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that
    nginx can run without sudo.

    nginx will load all files in /usr/local/etc/nginx/servers/.

    To have launchd start nginx now and restart at login:
      brew services start nginx
    Or, if you don't want/need a background service you can just run:
      nginx
    ==> Summary
```

开机自启动nginx服务设置：
``` bash
    mkdir -p ~/Library/LaunchAgents
    cp /usr/local/Cellar/nginx/1.12.0_1/homebrew.mxcl.nginx.plist ~/Library/LaunchAgents/
    launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist
```

配置非管理员开机nginx自动启动的权限和分组：
``` bash
    sudo chown root:wheel /usr/local/Cellar/nginx/1.12.0_1/bin/nginx
    sudo chmod u+s /usr/local/Cellar/nginx/1.12.0_1/bin/nginx
```

Nginx启动关闭命令：

``` bash
    #测试配置是否有语法错误
    nginx -t

    #打开 nginx
    sudo nginx

    #重新加载配置|重启|停止|退出 nginx
    nginx -s reload|reopen|stop|quit
```

好了，来跑下nginx

``` bash
    sudo nginx
```

![Welcome to nginx!](nginx_success.png)

> 到这里为止，我们已经安装完了`mysql php nginx`, 在安装php的时候添加了--with-mysql, 所以php操作mysql是没有问题的，现在我们就要配置nginx,让它监听php-fpm的进程，这样当用户打开浏览器访问的时候，身为反向代理的nignx就能把东西让php去执行了。

接下来，我们要配置`nginx.conf`文件，创建一个`php-fpm`文件（监听php-fpm）, 还要约定下将`nginx.pid`文件，log日志，以及以后我们要配置的站点.conf的路径，我们的路径约定还是按照brew默认的目录来设置,如下:

``` bash
    # nginx.conf,已经被创建好了，我们一会要更改下
    /usr/local/etc/nginx/nginx.conf

    # php-fpm,这个我们就放在和nginx.conf一样的路径下吧，这个要我们自己创建
    /usr/local/etc/nginx/php-fpm

    # 日志文件放在/usr/local/var/log/nginx中，默认已经有了access.log和error.log文件了
    /usr/local/var/log/nginx/

    # nginx.pid文件,放在/usr/local/var/run/下面，和php-fpm.pid放一堆
    /usr/local/var/run/

    # 以后要配置的站点.conf, 我们就放在/usr/local/etc/nginx/servers/下面，这个servers文件夹本身就存在的
    /usr/local/etc/nginx/servers/

    # 站点的根目录,也就用brew给我们设置的吧
    /usr/local/var/www/
```

下面我们先来修改nginx.conf, 用vim打开，把下面的信息覆盖nginx.conf, `vim /usr/local/etc/nginx/nginx.conf`, 如果你不习惯vim, 那就用sublime打开吧

``` bash
    worker_processes  1;

    error_log   /usr/local/var/log/nginx/error.log debug;
    pid        /usr/local/var/run/nginx.pid;

    events {
        worker_connections  256;
    }

    http {
        include       mime.types;
        default_type  application/octet-stream;

        log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                          '$status $body_bytes_sent "$http_referer" '
                          '"$http_user_agent" "$http_x_forwarded_for"';

        access_log  /usr/local/var/log/nginx/access.log  main;

        sendfile        on;
        keepalive_timeout  65;
        port_in_redirect off;

        include /usr/local/etc/nginx/servers/*;
    }
```

接下来，将下面的信息放入到php-fpm文件中，`vim /usr/local/etc/nginx/php-fpm`

``` bash
    location ~ \.php$ {
        try_files                   $uri = 404;
        fastcgi_pass                127.0.0.1:9000;
        fastcgi_index               index.php;
        fastcgi_intercept_errors    on;
        include /usr/local/etc/nginx/fastcgi.conf;
    }
```

ok, 下面就能配置站点了，先到`/usr/local/var/www`目录下建立站点根目录，就叫做default吧，然后在里面建立个info.php,内容就放phpinfo()函数就行.

``` bash
    mkdir /usr/local/var/www/default
    vi /usr/local/var/www/default/info.php #输入 <?php  phpinfo(); ?>
```

最后，去创建站点.conf文件

``` bash
    /usr/local/etc/nginx/servers/default.conf
```

输入下面的内容

``` bash
    server {
        listen       80;
        server_name  localhost;
        root         /usr/local/var/www/default;

        access_log  /usr/local/var/log/nginx/default.access.log  main;

        location / {
            index  index.html index.htm index.php;
            autoindex   on;
            include     /usr/local/etc/nginx/php-fpm;
        }

        error_page  404     /404.html;
        error_page  403     /403.html;
    }
```

测试下配置文件

``` bash
    ➜  servers sudo nginx -t
    nginx: the configuration file /usr/local/etc/nginx/nginx.conf syntax is ok
    nginx: configuration file /usr/local/etc/nginx/nginx.conf test is successful
```

然后开启php-fpm,已经开启的就不用开了

``` bash
    php-fpm -D
```

开启nginx服务

``` bash
    sudo nginx # 已经开启的用sudo nginx -s reload 重启下
```

浏览器打开http://localhost/info.php测试下

![php.info](php_info.png)

## 别名

上面的php-fpm关闭和重启的命令有点长，我们给它做个别名，在你的个人主目录下先建立一个`.aliases`文件，然后放入下面的内容

``` bash
    alias fpm.start='php-fpm -D'
    alias fpm.stop='kill -INT `cat /usr/local/var/run/php-fpm.pid`'
    alias fpm.restart='kill -USR2 `cat /usr/local/var/run/php-fpm.pid`'
    alias fpm.status='lsof -Pni4 | grep LISTEN | grep php-fpm'
```

然后

``` bash
    echo 'source ~/.aliases' >> ~/.zshrc
    source ~/.zshrc
```

> 如果执行命令（如：`php-fpm -D`）时报错，很多情况可以通过在命令前加 `sudo` 解决。

本文结束。
