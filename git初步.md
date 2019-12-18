
作者：DongdongBai
邮箱： baidongdong@nudt.edu

一、github基本概念
Repository
仓库的意思，即你的项目，你想在 GitHub 上开源一个项目，那就必须要新建一个 Repository ，如果你开源的项目多了，你就拥有了多个 Repositories 。

Issue
问题的意思，举个例子，就是你开源了一个项目，别人发现你的项目中有bug，或者哪些地方做的不够好，他就可以给你提个 Issue ，即问题，提的问题多了，也就是 Issues ，然后你看到了这些问题就可以去逐个修复，修复ok了就可以一个个的 Close 掉。

Star
这个好理解，就是给项目点赞，但是在 GitHub 上的点赞远比微博、知乎点赞难的多，如果你有一个项目获得100个star都算很不容易了！

Fork
这个不好翻译，如果实在要翻译我把他翻译成分叉，什么意思呢？你开源了一个项目，别人想在你这个项目的基础上做些改进，然后应用到自己的项目中，这个时候他就可以 Fork 你的项目，这个时候他的 GitHub 主页上就多了一个项目，只不过这个项目是基于你的项目基础（本质上是在原有项目的基础上新建了一个分支，分支的概念后面会在讲解Git的时候说到），他就可以随心所欲的去改进，但是丝毫不会影响原有项目的代码与结构。

Pull Request
发起请求，这个其实是基于 Fork 的，还是上面那个例子，如果别人在你基础上做了改进，后来觉得改进的很不错，应该要把这些改进让更多的人收益，于是就想把自己的改进合并到原有项目里，这个时候他就可以发起一个 Pull Request（简称PR） ，原有项目创建人，也就是你，就可以收到这个请求，这个时候你会仔细review他的代码，并且测试觉得OK了，就会接受他的PR，这个时候他做的改进原有项目就会拥有了。

Watch
这个也好理解就是观察，如果你 Watch 了某个项目，那么以后只要这个项目有任何更新，你都会第一时间收到关于这个项目的通知提醒。

Gist
有些时候你没有项目可以开源，只是单纯的想分享一些代码片段，那这个时候 Gist 就派上用场了！

二、git仓库的三个状态
git的仓库由的三棵”树”组成。第一个是你的工作目录(working dir)，它持有实际文件；第二个是暂存区（Index），它像个缓存区域，临时保存你的改动；最后是HEAD，它指向你最后一次提交的结果。



三、git使用要点
初始化一个新建的Git仓库，在新建的仓库的文件夹下面运行使用git init命令

添加文件到Git仓库，分两步：

第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件，其中git add *为添加文件夹下所有的文件
第二步，使用命令git commit -m <本次提交的说明>，完成。
git status命令可以让我们时刻掌握仓库当前的状态

如果输出

Untracked files:(关注点 1)
(use "git add <file>..." to include in what will be committed)

readme.txt(关注点 2)
1
2
3
4
Untracked files说明readme.txt是刚刚创建的，没有被加入到暂存区（Index）中

如果输出

Changes not staged for commit:(关注点 1)
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt(关注点 2)
1
2
3
4
5
Changes not staged for commit和modified: readme.txt说明readme.txt是被暂存区（Index）监视的，而且被修改了，但是还没有被提交（commit）

如果输出

Changes not staged for commit:(关注点 1)
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    deleted:    readme.txt(关注点 2)
1
2
3
4
5
Changes not staged for commit和deleted:readme.txt说明readme.txt是被暂存区（Index）监视的，而且被删除了，但是还没有被提交（commit）

git diff用来查看当前暂存区（Index）中监视的文件与HEAD中文件的区别
HEAD指向的版本就是当前版本，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard <commit的编号>。

穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

撤销修改

命令git checkout -- readme.txt意思是，把readme.txt文件在工作区的修改全部撤销(包括修改和删除），这里有两种情况：

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- <file>。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考第5条的版本穿梭。

撤销修改

在Git中，删除也是一个修改操作,命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。详见。

四、github使用要点
4.1、添加远程仓库
要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；比如：

git remote add origin git@github.com:DongdongBai/learngit.git
1
关联后，使用命令git push -u origin master第一次推送master（可以变为其他分支）分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

4.2、从远程库克隆
从github克隆一个仓库有两种协议:ssh和https，但是使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。
以下是克隆一个仓库的两种方法：

ssh方法： git clone git@github.com:DongdongBai/learngit.git
https方法： git clone https://github.com/DongdongBai/learngit.git
1
2
五、分支管理
5.1、创建和合并分支
查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name> = git branch <name> + git checkout <name>
合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>

5.2、解决冲突
解决冲突

5.3、分支管理策略
在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

分支管理策略

5.4、分支挂起方法
当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，但是，等等，当前正在dev上进行的工作还没有commit，如果没有将当前的dev分支中的修改commit，而直接将分支切换为master，会把在dev中修改的内容一起带到master中去。

分支挂起方法

5.5、删除没有合并过得分支
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

5.6、推送分支
推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：

推送主分支 git push origin master
推送dev分支 git push origin dev
1
2
但是，并不是一定要把本地分支往远程推送，master分支是主分支，因此要时刻与远程同步；dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步

六、github关系图

作者 : Dongdong Bai
邮箱： baidongdong@nudt.edu
