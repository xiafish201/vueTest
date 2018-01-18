# vueTest
每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

1.分支管理策略
通常合并分支时，git一般使用”Fast forward”模式，在这种模式下，删除分支后，会丢掉分支信息，现在我们来使用带参数 –no-ff来禁用”Fast forward”模式。首先我们来做demo演示下：

	创建一个dev分支。
	修改readme.txt内容。
	添加到暂存区。
	切换回主分支(master)。
	合并dev分支，使用命令 git merge –no-ff  -m “注释” dev
	查看历史记录
分支策略：首先master主分支应该是非常稳定的，也就是用来发布新版本，一般情况下不允许在上面干活，干活一般情况下在新建的dev分支上干活，干完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来。

总结创建与合并分支命令如下：

　　查看分支：git branch

　　创建分支：git branch name

　　切换分支：git checkout name

　　创建+切换分支：git checkout –b name

　　合并某分支到当前分支：git merge name

　　删除分支：git branch –d name

2.如何决绝冲突？
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

增加一行，测试git stash
3.bug分支
在开发中，会经常碰到bug问题，那么有了bug就需要修复，在Git中，分支是很强大的，每个bug都可以通过一个临时分支来修复，修复完成后，合并分支，然后将临时的分支删除掉。

　　比如我在开发中接到一个404 bug时候，我们可以创建一个404分支来修复它，但是，当前的dev分支上的工作还没有提交

并不是我不想提交，而是工作进行到一半时候，我们还无法提交，比如我这个分支bug要2天完成，但是我issue-404 bug需要5个小时内完成。怎么办呢？还好，Git还提供了一个stash功能，可以把当前工作现场 ”隐藏起来”，等以后恢复现场后继续工作

所以现在我可以通过创建issue-404分支来修复bug了。

　　首先我们要确定在那个分支上修复bug，比如我现在是在主分支master上来修复的，现在我要在master分支上创建一个临时分支
修复完成后，切换到master分支上，并完成合并，最后删除issue-404分支

现在，我们回到dev分支上干活了。

工作区是干净的，那么我们工作现场去哪里呢？我们可以使用命令 git stash list来查看下

工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，可以使用如下2个方法：

git stash apply恢复，恢复后，stash内容并不删除，你需要使用命令git stash drop来删除。
另一种方式是使用git stash pop,恢复的同时把stash内容也删除了。


