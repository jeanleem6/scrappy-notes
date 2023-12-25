---
title: Guide to use git - Section 2
date: 2016-09-02 16:54:07
tags: [git]
---

## Getting a Git Repository

You can get a Git project using two main approaches. The first takes an existing project or directory and imports it into Git. The second clones an existing Git repository from another server.

1. **Initializing a Repository in an Existing Directory**
    If you’re starting to track an existing project in Git, you need to go to the project’s directory and type:

    ``` bash
        $ git init
    ```

    This creates a new subdirectory named .git that contains all of your necessary repository files – a Git repository skeleton. At this point, nothing in your project is tracked yet. (See [Git Internals][link-1] for more information about exactly what files are contained in the .git directory you just created.)

2. **Cloning an Existing Repository**

    <!-- more -->

    If you want to get a copy of an existing Git repository – for example, a project you’d like to contribute to – the command you need is `git clone`.Every version of every file for the history of the project is pulled down by default when you run git clone. In fact, if your server disk gets corrupted, you can often use nearly any of the clones on any client to set the server back to the state it was in when it was cloned (you may lose some server-side hooks and such, but all the versioned data would be there – see [Getting Git on a Server][link-2] for more details).

    You clone a repository with `git clone [url]`. For example, if you want to clone the Git linkable library called libgit2, you can do so like this:

    ``` bash
        $ git clone https://github.com/libgit2/libgit2
    ```

    That creates a directory named “libgit2”, initializes a `.git` directory inside it, pulls down all the data for that repository, and checks out a working copy of the latest version. If you go into the new libgit2 directory, you’ll see the project files in there, ready to be worked on or used. If you want to clone the repository into a directory named something other than “libgit2”, you can specify that as the next command-line option:

    ``` bash
        $ git clone https://github.com/libgit2/libgit2 mylibgit
    ```

    That command does the same thing as the previous one, but the target directory is called `mylibgit`.

    Git has a number of different transfer protocols you can use. The previous example uses the `https://` protocol, but you may also see `git://` or `user@server:path/to/repo.git`, which uses the SSH transfer protocol. [Getting Git on a Server][link-2] will introduce all of the available options the server can set up to access your Git repository and the pros and cons of each.


[link-1]: https://git-scm.com/book/en/v2/ch00/_git_internals
[link-2]: https://git-scm.com/book/en/v2/ch00/_git_on_the_server

