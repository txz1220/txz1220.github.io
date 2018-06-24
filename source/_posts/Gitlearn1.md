---
title: git学习
categories:
- 技术
- Git学习
tags:
- Git学习
---


1.初始化一个Git仓库，使用`git init`命令。

2.添加文件到Git仓库，分两步：

- 使用命令`git add` `<file>`，注意，可反复多次使用，添加多个文件；
- 使用命令`git commit -m` `<message>`，完成。


3.要随时掌握工作区的状态，使用`git status`命令。

4.如果`git status`告诉你有文件被修改过，用git diff可以查看修改内容。


<!--more-->
5.版本回退：


- HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard `commit_id` `    或者用 --hard HEAD^ 这种形式回到上一个版本   上上个版本用 --hard HEAD^^   

- 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

- 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。


6.工作区和暂存区

#### 工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：



#### 版本库（Repository）

工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为`stage`（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向master的一个指针叫`HEAD`。
![](http://ww1.sinaimg.cn/large/006c6oKBgy1fsktu0areaj30dv072jsf.jpg)

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。


6.撤销修改命令

命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。

>git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。



加入你已经add 了，但是还没有commit  你可以用命令git reset HEAD `<file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区：

git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。


接下来就是用git checkout -- readme.txt   撤回工作区的修改了。

7.删除命令


一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用rm命令删了：

这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了：

现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit：


另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

$ git checkout -- test.txt
git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。



### 远程仓库


首先在github 上建立我们的远程仓库，然后执行命令 git remote add origin git@github.com:用户名/learngit.git  建立本地和远程的链接，

下面注意： 如果你的远程仓库里面含有README.md  而你本地的仓库没有这个文件，你需要执行  git pull --rebase origin master  先合并，

然后再执行推送本地的内容，git push -u origin master

>由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。


#### 远程仓库进行克隆：

git clone git@github.com:你的用户名字/gitskills.git    再本地那个文件执行就会放在哪个文件下。


>你也许还注意到，GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。
使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。



### 分支管理


在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点

![](http://ww1.sinaimg.cn/large/006c6oKBgy1fsl0d3ajwwj309e04st92.jpg)


当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上：

![](http://ww1.sinaimg.cn/large/006c6oKBgy1fsl0dc8mi6j30ct06l3z0.jpg)


你看，Git创建一个分支很快，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变：

![](http://ww1.sinaimg.cn/large/006c6oKBgy1fsl0f39pwmj30fu06x74w.jpg)


假如我们在dev上的工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并：

![](http://ww1.sinaimg.cn/large/006c6oKBgy1fsl0fwsq6rj30ev06ljs0.jpg)

合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条master分支：

![](http://ww1.sinaimg.cn/large/006c6oKBgy1fsl0gt3jwxj30dl04vwew.jpg)






#### 下面看看具体是怎么做的呢

首先，我们创建dev分支，然后切换到dev分支：
```git
$ git checkout -b dev
Switched to a new branch 'dev'
```

git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
```git
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```

查看所处的分支：

```git
$ git branch
* dev
  master
```

切换回master分支：

```git
$ git checkout master
```



合并分支：

```git
git merge dev

```


git merge命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和dev分支的最新提交是完全一样的。

注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。

当然，也不是每次合并都能Fast-forward，我们后面会讲其他方式的合并。

合并完成后，就可以放心地删除dev分支了：

```git
$ git branch -d dev
```



总结：

Git鼓励大量使用分支：

- 查看分支：git branch
- 
- 创建分支：git branch <name>
- 
- 切换分支：git checkout <name>
- 
- 创建+切换分支：git checkout -b <name>
- 
- 合并某分支到当前分支：git merge <name>
- 
- 删除分支：git branch -d <name>

