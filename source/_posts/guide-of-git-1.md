---
title: Guide to use git - Section 1
date: 2016-09-02 08:34:52
tags: [git]
---

> You'll getting to know **install git** on different OS from this section, and then **configure** it on your local computer, indeed to **get help** somewhere.


## Install git

1. **Installing on Linux**
    If you’re on Fedora for example, you can use yum:
    ``` bash
        $ sudo yum install git-all
    ```
    If you’re on a Debian-based distribution like Ubuntu, try apt-get:
    ``` bash
        $ sudo apt-get install git-all
    ```
    For more options, there are instructions for installing on several different Unix flavors on the Git website, at <http://git-scm.com/download/linux>.

2. **Installing on Mac**

    <!-- more -->

    There are several ways to install Git on a Mac. The easiest is probably to install the Xcode Command Line Tools. On Mavericks (10.9) or above you can do this simply by trying to **run `git` from the Terminal** the very first time. If you don’t have it installed already, it will prompt you to install it.

    If you want a more up to date version, you can also install it via a binary installer. An OSX Git installer is maintained and available for download at the Git website, at http://git-scm.com/download/mac.

    You can also **install it as part of the GitHub** for Mac install. Their GUI Git tool has an option to install command line tools as well. You can download that tool from the GitHub for Mac website, at http://mac.github.com.

3. **Installing on Windows**
    There are also a few ways to install Git on Windows. The most official build is available for download on the Git website. Just go to <http://git-scm.com/download/win> and the download will start automatically. Note that this is a project called Git for Windows, which is separate from Git itself; for more information on it, go to <https://git-for-windows.github.io/>.

    Another easy way to get Git installed is by installing GitHub for Windows. The installer includes a command line version of Git as well as the GUI. It also works well with Powershell, and sets up solid credential caching and sane CRLF settings. We’ll learn more about those things a little later, but suffice it to say they’re things you want. You can download this from the GitHub for Windows website, at <http://windows.github.com>.

## Getting Started - First-Time Git Setup

Git comes with a tool called `git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates. These variables can be stored in three different places:

1. `/etc/gitconfig` file: Contains values for every user on the system and all their repositories. If you pass the option `--system` to `git config`, it reads and writes from this file specifically.

2. `~/.gitconfig` or `~/.config/git/config` file: Specific to your user. You can make Git read and write to this file specifically by passing the `--global` option.

3. `config` file in the Git directory (that is, `.git/config`) of whatever repository you’re currently using: Specific to that single repository.

Each level overrides values in the previous level, so values in `.git/config` trump those in `/etc/gitconfig`.

On Windows systems, Git looks for the `.gitconfig` file in the `$HOME` directory (`C:\Users\$USER` for most people). It also still looks for `/etc/gitconfig`, although it’s relative to the MSys root, which is wherever you decide to install Git on your Windows system when you run the installer. If you are using version 2.x or later of Git for Windows, there is also a system-level config file at `C:\Documents and Settings\All Users\Application Data\Git\config `on Windows XP, and in `C:\ProgramData\Git\config` on Windows Vista and newer. This config file can only be changed by `git config -f <file>` as an admin.

### Your Identity

**The first thing** you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:

``` bash
    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com
```

Again, you need to do this only once if you pass the `--global` option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or email address for specific projects, you can run the command without the `--global` option when you’re in that project.

### Your Editor

Now that your identity is set up, you can configure the default text editor that will be used when Git needs you to type in a message. If not configured, Git uses your system’s default editor.

If you want to use a different text editor, such as Nano, you can do the following:

``` bash
    $ git config --global core.editor nano
```

While on a Windows system, if you want to use a different text editor, such as Notepad++, you can do the following:

On a x86 system

``` bash
    $ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession"
```

On a x64 system

``` bash
    $ git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"
```

> NOTE
> [Vim](/2016/08/05/Mac-OS-X-Terminal/), Emacs and Notepad++ are popular text editors often used by developers on Unix based systems like Linux and OS X or a Windows system. If you are not familiar with either of these editors, you may need to search for specific instructions for how to set up your favorite editor with Git.

### Checking Your Settings

If you want to check your settings, you can use the `git config --list` command to list all the settings Git can find at that point:

``` bash
    $ git config --list
    user.name=John Doe
    user.email=johndoe@example.com
    color.status=auto
    color.branch=auto
    color.interactive=auto
    color.diff=auto
    ...
```

You may see keys more than once, because Git reads the same key from different files (`/etc/gitconfig` and `~/.gitconfig`, for example). In this case, Git uses the last value for each unique key it sees.

You can also check what Git thinks a specific key’s value is by typing `git config <key>`:

``` bash
    $ git config user.name
    John Doe
```

### Git Aliases

Git doesn’t automatically infer your command if you type it in partially. If you don’t want to type the entire text of each of the Git commands, you can easily set up an alias for each command using `git config`. Here are a couple of examples you may want to set up:

``` bash
    $ git config --global alias.co checkout
    $ git config --global alias.br branch
    $ git config --global alias.ci commit
    $ git config --global alias.st status
    $ git config --global alias.unstage 'reset HEAD --'  # to correct the usability problem you encountered with unstaging a file
    $ git config --global alias.last 'log -1 HEAD'       # show the last commit
```

As you can tell, Git simply replaces the new command with whatever you alias it for. However, maybe you want to run an external command, rather than a Git subcommand. In that case, you start the command with a ! character. This is useful if you write your own tools that work with a Git repository. We can demonstrate by aliasing `git visual` to run `gitk`:

``` bash
    $ git config --global alias.visual '!gitk'
```

## Getting Help

If you ever need help while using Git, there are three ways to get the manual page (manpage) help for any of the Git commands:

``` bash
    $ git help <verb>
    $ git <verb> --help
    $ man git-<verb>
```

For example, you can get the manpage help for the config command by running

``` bash
    $ git help config
```

These commands are nice because you can access them anywhere, even offline.

---

reference: <https://git-scm.com/doc>
