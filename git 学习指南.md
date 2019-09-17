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

最新的那个版本```git diff```已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个append GPL的commit id是e9c49...，于是就可以指定回到未来的某个版本：

    $ git reset --hard e9c49
    HEAD is now at e9c4982 增加了git diff

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，Git仅仅是把HEAD从指向```增加了git diff```：

现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的commit id怎么办？

在Git中，总是有后悔药可以吃的。当你用$ git reset --hard HEAD^回退到1版本时，再想恢复到2版本，就必须找到1的commit id。Git提供了一个命令git reflog用来记录你的每一次命令：

    $ git reflog
    39f2d23 (HEAD -> master) HEAD@{0}: reset: moving to 39f2d
    e9c4982 HEAD@{1}: reset: moving to e9c49
    39f2d23 (HEAD -> master) HEAD@{2}: commit: 2019年9月16日 20点41分 增加了git log
    和git reset
    e09fc67 HEAD@{3}: reset: moving to head^
    e9c4982 HEAD@{4}: commit: 增加了git diff
    e09fc67 HEAD@{5}: commit (initial): git 学习 新建 增加 提交

现在总结一下：

HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

## (4)工作区和暂存区

### 工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区。
#### 版本库（Repository）
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
### 暂存区
前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

## (5)撤销修改
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

## (6)删除
```rm test.txt``` 删除本地文件

    $ git rm test.txt
    rm 'test.txt'
    git commit -m "remove test.txt"
删除git文件
