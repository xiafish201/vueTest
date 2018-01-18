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


