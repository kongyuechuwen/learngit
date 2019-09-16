# GitHub 学习指南

2019年9月16日 开始学习 kongyue

[参考廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600/896827951938304)

## 1. 创建版本库

    win CMD
    $ mkdir learngit
    $ cd learngit
    $ pwd

```pwd```命令用于显示当前目录,我的目录是/e/learngit

## 2.初始化版本库

    $ git init
    Initialized empty Git repository in /Users/michael/learngit/.git/

通过```git init```命令把这个目录变成Git可以管理的仓库

## 3.提交

### (1)用命令git add告诉Git，把文件添加到仓库：
  
    $ git add git\ 学习指南.md git\ 学习指南.md 

### (2)用命令git commit -m 告诉Git，把文件提交到仓库：

    git commit -m "git 学习 新建 增加 提交"
    [master (root-commit) e09fc67] git 学习 新建 增加 提交
    2 files changed, 1109 insertions(+)
    create mode 100644 "git \345\255\246\344\271\240\346\214\207\345\215\227.html"
    create mode 100644 "git \345\255\246\344\271\240\346\214\207\345\215\227.md"


### (3)git status 查看目前状态

    $ git status
    On branch master
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
        modified:   "git \345\255\246\344\271\240\346\214\207\345\215\227.html"
        modified:   "git \345\255\246\344\271\240\346\214\207\345\215\227.md"

    no changes added to commit (use "git add" and/or "git commit -a")

上面的命令输出告诉我们，```git 学习指南.md``` 被修改过了，但还没有准备提交的修改。
### (4)git diff 查看修改后与之前的不同

    $ git diff 'git 学习指南.md'
    diff --git "a/git \345\255\246\344\271\240\346\214\207\345\215\227.md" "b/git \345\255\246\344\271\240\346\214\207\345\215\227.md"
    index d045deb..5ce6956 100644
    --- "a/git \345\255\246\344\271\240\346\214\207\345\215\227.md"
    +++ "b/git \345\255\246\344\271\240\346\214\207\345\215\227.md"
    @@ -1,6 +1,7 @@
    # GitHub 学习指南

再次```git add``` ```git commit```,即可。
### (5)git log 查看版本历史

    $ git log
    commit e9c498254844406e8a16b9ca7f9bf52d5e08f2e5 (HEAD -> master)
    Author: kongyue <wenzheng@whu.edu.cn>
    Date:   Mon Sep 16 20:29:12 2019 +0800
    增加了git diff

    commit e09fc678f62015853898c84084f74bc8ddf46eae
    Author: kongyue <wenzheng@whu.edu.cn>
    Date:   Mon Sep 16 20:12:12 2019 +0800
    git 学习 新建 增加 提交

### (6)git 回滚

首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交e9c4...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

现在回滚到上一个版本
git reset --hard HEAD^

    $ git reset --hard head^
    HEAD is now at e09fc67 git 学习 新建 增加 提交



