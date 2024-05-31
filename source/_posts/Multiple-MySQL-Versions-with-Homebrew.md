---
title: Multiple MySQL Versions with Homebrew
date: 2019-05-08 11:20:10
tags: [mysql]
---

## CONTENT

For homebrew version 2.1.2

``` bash
brew -v # => Homebrew 2.1.2
```

Install the current version of mysql.

``` bash
# Install current mysql version
brew install mysql

# Start agent for current version of mysql (including on login)
ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```

Install the older version of mysql.

``` bash
# Find older mysql versions
brew search mysql

# Install older mysql version
brew install mysql@5.6

# Start agent for older version of mysql (including on login)
ln -sfv /usr/local/opt/mysql@5.6/*.plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql@5.6.plist
```

Then to switch to the older version.

``` bash
# Unlink current mysql version
brew unlink mysql

# Check older mysql version
ls /usr/local/Cellar/mysql@5.6 # => 5.6.43

# Link the older version
brew switch mysql@5.6 5.6.43
# If the above didn't working, try this:
brew link mysql@5.6 --force
```

And to switch back to the current version.

``` bash
# Unlink older mysql version
brew unlink mysql@5.6

# Check current mysql version
ls /usr/local/Cellar/mysql # => 8.0.16

# Link the current version
brew switch mysql 8.0.16
```

To verify which mysql version you're on at any time.

``` bash
# Check which version of mysql is currently symlinked
ls -l /usr/local/bin/mysql # => /usr/local/bin/mysql@ -> ../Cellar/mysql56/5.6.43/bin/mysql

# Or using the mysql command
mysql --version
```

And to unload a mysql agent for a given version.

``` bash
# Stop agent for current version of mysql
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
rm ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist

# Stop agent for older version of mysql
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.mysql@5.6.plist
rm ~/Library/LaunchAgents/homebrew.mxcl.mysql@5.6.plist
```

---
## Caution

> *jpmelguizo:*
> Went with mysql@5.6 and I'm getting: `ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)` Although brew services list says mysql@5.6 is started, there's no mysqld process running and no mysql.sock file anywhere. Any ideas on how to fix it? should I just go with the deprecated mysql56 instead?

> *jsweeney:*
>
> **(NOTICE: If you see `\@`, it is just `@`, remove the backslash(`\`) when you copy.)**
> I also had your problem. My issue was that the mysql\@5.6 was trying to boot the mysql 5.7 database (installed in the default `/usr/local/var` folder). If you want to run both in parallel on their own distinct databases, there are a few more steps to do.
>
> 1. Create a new (separate) data directory and database for the 5.6 version
    Run `/usr/local/Cellar/mysql\@5.6/5.6.36/bin/mysql_install_db --user=root --datadir=/usr/local/var/mysql56`
> 2. Change the configuration to start the 5.6 version pointing to this database
>   Edit `/usr/local/Cellar/mysql\@5.6/5.6.36/homebrew.mxcl.mysql\@5.6.plist` to change both `/usr/local/var/mysql` instances to `/usr/local/var/mysql56` (I didn't put the `@` in the folder name just in case it would cause issues).
    ``` xml
    <plist version="1.0">
    <dict>
      <key>KeepAlive</key>
      <true/>
      <key>Label</key>
      <string>homebrew.mxcl.mysql@5.6</string>
      <key>ProgramArguments</key>
      <array>
        <string>/usr/local/opt/mysql@5.6/bin/mysqld_safe</string>
        <string>--bind-address=127.0.0.1</string>
        <string>--datadir=/usr/local/var/mysql56</string> <!-- <<<<<<<<<<<<<<<<<< HERE -->
      </array>
      <key>RunAtLoad</key>
      <true/>
      <key>WorkingDirectory</key>
      <string>/usr/local/var/mysql56</string> <!-- <<<<<<<<<<<<<<<<<< AND HERE -->
    </dict>
    </plist>
    ```
> 3. Change the port of the 5.6 server - if ever you want to start both at the same time.
> Edit `/usr/local/Cellar/mysql\@5.6/5.6.36/my.cnf`, uncomment `port` and change it to some other value than `3306`.
    ``` bash
    # These are commonly set, remove the # and set as required.
    # basedir = .....
    # datadir = .....
    port = 3356
    # server_id = .....
    # socket = .....
    ```
> NOTE A little caveat about connecting to the MySQL instances after such a setup. Using any kind of driver will > work out of the box if you set the correct port. However, at the command line, `mysql` ignores the `--port` > value by default, so you need something like this>
    ``` bash
    mysql -uroot --port=3356 --protocol=TCP
    ```
> See this article for more details: https://dev.mysql.com/doc/refman/5.7/en/connecting.html

---
mysql_downgrade:

``` bash
# Kill rails server and guard
bin/spring stop
brew services stop mysql
brew uninstall mysql
brew install mysql@5.5
brew link mysql@5.5 --force
brew services start mysql@5.5
rbenv uninstall 2.3.3
rbenv install 2.3.3
gem install bundle
gem install rubocop-rspec rubocop scss_lint rails_best_practices # (optional)
bundle install
be rails db:migrate:reset
```

---
via:
from: https://gist.github.com/benlinton/d24471729ed6c2ace731
mysql_downgrade: https://gist.github.com/6temes/3c52f8a472f61d9676e7218a98812286
