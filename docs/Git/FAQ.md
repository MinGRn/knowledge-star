# 常见问题

该文档主要记录在开发过程中遇到的问题。

## Everything up-to-date

`git` 在提交时提示 `Everything up-to-date`。

```
$ git push origin master
Everything up-to-date
```

原因如下：

```note
Why does Git refuse to push, saying “everything up to date”?
git push with no additional arguments only pushes branches that exist in the remote already. 
If the remote repository is empty, nothing will be pushed. 
In this case, explicitly specify a branch to push, e.g. `git push master`.
```

也就是说一开始 `git` 服务器仓库是完全空的，不包含任何一个分支(`branch`)，因此刚开始 `Push` 时需要指定一个。

执行 `git remote -v` 后看到自己的 `remote` 端名字为 `origin`:

```
$ git remote -v
origin  https://github.com/(***).git (fetch)
origin  https://github.com/(***).git (push)
```

执行 `git branch` 后查看本地当前分支，执行 `git branch -a` 查看全部分支（包括远程分支）。

```
$ git branch
* master
```

可以看到当前远程名为 `origin` 并且分支为 `master`。那为什么在提交时看提示 `Everything up-to-date` 呢？

现在来执行命令 `git status` 看下工作空间:

```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   SUMMARY.md
        modified:   book.json
        modified:   docs/MySQL/mysql-config-set.md
        modified:   images/favicon.ico

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/
        _book/
        docs/GitBook/插件管理.md
        node_modules/
        nohup.out
```

其实真正原因是在提交提交时执行命令：

```
$ git add file...
```

后并没有进行 `git commit`，所以在进行推送远程时并没有要进行推送的文件。

所以，当提示 `Everything up-to-date` 原因有两个：没有远程仓库或者本地没有需要提交的文件。