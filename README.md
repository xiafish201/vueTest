# vueTest
每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

总结创建与合并分支命令如下：

　　查看分支：git branch

　　创建分支：git branch name

　　切换分支：git checkout name

　　创建+切换分支：git checkout –b name

　　合并某分支到当前分支：git merge name

　　删除分支：git branch –d name

1.如何决绝冲突？
	1.新建并切换分支 git checkout -b bug1
	2.修改文件，增加内容 
	3.提交进暂存区 git add .  git commit -m "修改readme.md"
	4.切换分支master git checkout -b master
	5.修改文件，增加内容
	6.提交进暂存区 git add . git commit -m "master上修改readme.md"
	7.在master上合并bug1 git merge bug1
	参数冲突
	8.查看状态 git status
	Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，其中<<<HEAD是指主分支修改的内容，>>>>>bug1 是指bug1上修改的内容
	9.修改文件，解决冲突
	10.提交
	11.查看合并情况，git log


多人协作。

　　当你从远程库克隆时候，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且远程库的默认名称是origin。

要查看远程库的信息 使用 git remote
要查看远程库的详细信息 使用 git remote –v
　　如下演示：

 

　　一：推送分支：

      推送分支就是把该分支上所有本地提交到远程库中，推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：

      使用命令 git push origin master

　　比如我现在的github上的readme.txt代码如下：



　　本地的readme.txt代码如下：

 

　　现在我想把本地更新的readme.txt代码推送到远程库中，使用命令如下：



　　我们可以看到如上，推送成功，我们可以继续来截图github上的readme.txt内容 如下：



　　可以看到 推送成功了，如果我们现在要推送到其他分支，比如dev分支上，我们还是那个命令 git push origin dev

　　那么一般情况下，那些分支要推送呢？

master分支是主分支，因此要时刻与远程同步。
一些修复bug分支不需要推送到远程去，可以先合并到主分支上，然后把主分支master推送到远程去。
　　二：抓取分支：

　　多人协作时，大家都会往master分支上推送各自的修改。现在我们可以模拟另外一个同事，可以在另一台电脑上（注意要把SSH key添加到github上）或者同一台电脑上另外一个目录克隆，新建一个目录名字叫testgit2

　　但是我首先要把dev分支也要推送到远程去，如下



　　接着进入testgit2目录，进行克隆远程的库到本地来，如下：

 

　　现在目录下生成有如下所示：



　　现在我们的小伙伴要在dev分支上做开发，就必须把远程的origin的dev分支到本地来，于是可以使用命令创建本地dev分支：git checkout  –b dev origin/dev

　　现在小伙伴们就可以在dev分支上做开发了，开发完成后把dev分支推送到远程库时。

　　如下：



　　小伙伴们已经向origin/dev分支上推送了提交，而我在我的目录文件下也对同样的文件同个地方作了修改，也试图推送到远程库时，如下：



　　由上面可知：推送失败，因为我的小伙伴最新提交的和我试图推送的有冲突，解决的办法也很简单，上面已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后在本地合并，解决冲突，再推送。



　　git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：如下：



　　这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的 解决冲突完全一样。解决后，提交，再push：

　　我们可以先来看看readme.txt内容了。



　　现在手动已经解决完了，我接在需要再提交，再push到远程库里面去。如下所示：



　　因此：多人协作工作模式一般是这样的：

首先，可以试图用git push origin branch-name推送自己的修改.
如果推送失败，则因为远程分支比你的本地更新早，需要先用git pull试图合并。
如果合并有冲突，则需要解决冲突，并在本地提交。再用git push origin branch-name推送。
　　Git基本常用命令如下：

　　mkdir：         XX (创建一个空目录 XX指目录名)

　　pwd：          显示当前目录的路径。

　　git init          把当前的目录变成可以管理的git仓库，生成隐藏.git文件。

　　git add XX       把xx文件添加到暂存区去。

　　git commit –m “XX”  提交文件 –m 后面的是注释。

　　git status        查看仓库状态

　　git diff  XX      查看XX文件修改了那些内容

　　git log          查看历史记录

　　git reset  --hard HEAD^ 或者 git reset  --hard HEAD~ 回退到上一个版本

　　(如果想回退到100个版本，使用git reset –hard HEAD~100 )

　　cat XX         查看XX文件内容

　　git reflog       查看历史记录的版本号id

　　git checkout -- XX  把XX文件在工作区的修改全部撤销。

　　git rm XX          删除XX文件

　　git remote add origin https://github.com/tugenhua0707/testgit 关联一个远程库

　　git push –u(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库

　　git clone https://github.com/tugenhua0707/testgit  从远程库中克隆

　　git checkout –b dev  创建dev分支 并切换到dev分支上

　　git branch  查看当前所有的分支

　　git checkout master 切换回master分支

　　git merge dev    在当前的分支上合并dev分支

　　git branch –d dev 删除dev分支

　　git branch name  创建分支

　　git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作

　　git stash list 查看所有被隐藏的文件列表

　　git stash apply 恢复被隐藏的文件，但是内容不删除

　　git stash drop 删除文件

　　git stash pop 恢复文件的同时 也删除文件

　　git remote 查看远程库的信息

　　git remote –v 查看远程库的详细信息

　　git push origin master  Git会把master分支推送到远程库对应的远程分支上


