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


首先在github 上建立我们的远程仓库，执行git init ,然后执行命令git remote add origin git@github.com:用户名/learngit.git  建立本地和远程的链接，

下面注意： 如果你的远程仓库里面含有README.md  而你本地的仓库没有这个文件，你需要执行git pull --rebase origin master  先合并，

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





### 解决冲突

准备新的feature1分支，继续我们的新分支开发：

$ git checkout -b feature1

进行修改文件

在这个分支上提交

$ git add readme.txt

$ git commit -m "AND simple"


切换到master分支：

$ git checkout master


Git还会自动提示我们当前master分支比远程的master分支要超前1个提交。

在master分支上把readme.txt文件的最后一行进行修改

好了，提交：

$ git add readme.txt 
$ git commit -m "& simple"


现在，master分支和feature1分支各自都分别有新的提交，

这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，

来，执行下看看：

$ git merge feature1

果然冲突了！Git告诉我们，readme.txt文件存在冲突，必须手动解决冲突后再提交。git status也可以告诉我们冲突的文件：


我们可以直接查看我们修改的文件的内容：


Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改如下后保存：

把冲突的内容修改好，再提交

$ git add readme.txt 
$ git commit -m "conflict fixed"

最后，删除feature1分支：

$ git branch -d feature1


总结：

- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

- 解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

- 用git log --graph命令可以看到分支合并图。



### 分支管理策略

通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

下面我们实战一下--no-ff方式的git merge：

首先，仍然创建并切换dev分支：

$ git checkout -b dev

修改文件并提交

$ git add readme.txt 
$ git commit -m "add merge"

现在，我们切换回master：

$ git checkout master

准备合并dev分支，请注意--no-ff参数，表示禁用Fast forward：

$ git merge --no-ff -m "merge with no-ff" dev

因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。

合并后，我们用git log看看分支历史：


#### 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsueuf2dn8j30ec03wq2z.jpg)




### bug分支


软件开发中，bug就像家常便饭一样。有了bug就需要修复，在Git中，由于分支是如此的强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，但是，等等，当前正在dev上进行的工作还没有提交：

$ git status


看到还有没提交啊

并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？

幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：

$ git stash
Saved working directory and index state WIP on dev: f52c633 add merge


现在，用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。

首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支：

$ git checkout master

$ git checkout -b issue-101

现在修复bug，需要把“Git is free software ...”改为“Git is a free software ...”，然后提交：

$ git add readme.txt 
$ git commit -m "fix bug 101"

修复完成后，切换到master分支，并完成合并，最后删除issue-101分支：

$ git checkout master
$ git merge --no-ff -m "merged bug fix 101" issue-101

太棒了，原计划两个小时的bug修复只花了5分钟！现在，是时候接着回到dev分支干活了！

$ git checkout dev

查看下：
$ git status

工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：

$ git stash list
stash@{0}: WIP on dev: f52c633 add merge

工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了：

$ git stash pop

再用git stash list查看，就看不到任何stash内容了

小结
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。



#### 问题

修改完bug，master的内容已经和dev上的原始内容不一样了，在完成dev和master合并的时候，就会报有内容冲突。如果bug修改量很大，冲突的内容就会很多，如果高效的解决这种冲突？

答：把bug分支修改后再跟dev分支合并这样master和dev分支就都搞定了

为什么要用stash？一开始，我也觉得没必要，直接切换分支，再回来是一样的啊。
然后测试了一把，就知道原因了。
情景如下：
1、在dev分支，创建一个新文件test6.txt。并add它，让它stage。
2、这时切回master分支，你会看到这个test6.txt居然也在master分支里。但它实际上是属于dev分支的。怎么办？
3、git stash就有作用了。切回dev分支，执行git stach。这时git bash会告诉你
“Saved working directory and index state WIP on newF2: b63fbcb add test6.txt
HEAD is now at b63fbcb add test6.txt”。它已经把test6.txt的现场保存好了。
4、这时你在切回master分支，test6.txt就消失了。
现在懂了吧。。。。为什么要用git stash。




### feature分支

软件开发中，总有无穷无尽的新的功能要不断添加进来。

添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。

于是准备开发：

$ git checkout -b feature-vulcan

5分钟后，开发完毕：

$ git add vulcan.py
$ git status
$ git commit -m "add feature vulcan"

切回dev，准备合并：

$ git checkout dev

一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。

但是！

就在此时，接到上级命令，因经费不足，新功能必须取消！

虽然白干了，但是这个包含机密资料的分支还是必须就地销毁：

$ git branch -d feature-vulcan
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.

销毁失败。Git友情提醒，feature-vulcan分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用大写的-D参数。。

现在我们强行删除：

$ git branch -D feature-vulcan
Deleted branch feature-vulcan (was 287773e).

#### 小结

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。


### 多人协作

当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。

要查看远程库的信息，用git remote：

$ git remote

或者，用git remote -v显示更详细的信息：


推送分支
推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：

$ git push origin master
如果要推送其他分支，比如dev，就改成：

$ git push origin dev

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

master分支是主分支，因此要时刻与远程同步；

dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！



#### 抓取分支


多人协作时，大家都会往master和dev分支上推送各自的修改。

现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆：

$ git clone git@github.com:michaelliao/learngit.git


当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。不信可以用git branch命令看看：

$ git branch
* master

现在，你的小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支：

$ git checkout -b dev origin/dev


现在，他就可以在dev上继续修改，然后，时不时地把dev分支push到远程：

$ git add env.txt

$ git commit -m "add env"

$ git push origin dev


你的小伙伴已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送：

推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：

git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：

$ git branch --set-upstream-to=origin/dev dev

再pull：

$ git pull

这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：

$ git commit -m "fix env conflict"

$ git push origin dev


因此，多人协作的工作模式通常是这样：

- 首先，可以试图用git push origin <branch-name>推送自己的修改；

- 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

- 如果合并有冲突，则解决冲突，并在本地提交；

- 没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

- 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。





###   标签管理

在Git中打标签非常简单，首先，切换到需要打标签的分支上：

$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'


然后，敲命令git tag <name>就可以打一个新标签：

$ git tag v1.0

可以用命令git tag查看所有标签：

$ git tag
v1.0


默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？

方法是找到历史提交的commit id，然后打上就可以了：
$ git log --pretty=oneline --abbrev-commit

比方说要对add merge这次提交打标签，它对应的commit id是f52c633，敲入命令：

$ git tag v0.9 f52c633

注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：

$ git show v0.9
commit f52c63349bc3c1593499807e5c8e972b82c8f286 (tag: v0.9)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:56:54 2018 +0800

    add merge

diff --git a/readme.txt b/readme.txt
...

#### 小结

- 命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；

- 命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；

- 命令git tag可以查看所有标签。



### 操作标签

如果标签打错了，也可以删除：

$ git tag -d v0.1
Deleted tag 'v0.1' (was f15b0dd)

因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令git push origin <tagname>：


或者，一次性推送全部尚未推送到远程的本地标签：

$ git push origin --tags

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：

$ git tag -d v0.9
Deleted tag 'v0.9' (was f52c633)
然后，从远程删除。删除命令也是push，但是格式如下：

$ git push origin :refs/tags/v0.9
To github.com:michaelliao/learngit.git
 - [deleted]         v0.9


#### 小结

- 命令git push origin <tagname>可以推送一个本地标签；

- 命令git push origin --tags可以推送全部未推送过的本地标签；

- 命令git tag -d <tagname>可以删除一个本地标签；

- 命令git push origin :refs/tags/<tagname>可以删除一个远程标签。


#### 问答：

最好加上有标签了，怎么根据标签回溯版本的内容，否则只是加标签没意义呀！

先用 git show v1.0 就能知道tag标记的这次commit的节点的id 号码；
如果是 590cf6b63d1039a17869defb6b70e4fa977c073a那么就用git checkout 590cf6b（数字长度六七位就可以）
就能返回这个版本。
在版本之间切换的内容。