
#git 指令说明

##一、增加和删除文件

### 1. git add 
1. 描述
	1. 此命令将要提交的文件的信息添加到索引库中（将修改添加到暂存区），以准备为下一次提交分段的内容。
	2. 在git commit之前必须使用git add命令将任何新的修改的文件添加到索引；
	3. git status命令可用于获取那些文件具有下一次提交分段的更改的摘要；
2. 示例
	1. git add documentation/*.txt  将文件夹下面的*.txt文件内容添加；
	2. git add dir  将dir目录下的所有文件提交到暂存区
	3. git add .  # 将所有修改添加到暂存区
	4. git add *  # Ant风格添加修改
	5. git add *Controller   # 将以Controller结尾的文件的所有修改添加到暂存区
	6. git add Hello*   # 将所有以Hello开头的文件的修改添加到暂存区 例如:HelloWorld.txt,Hello.java,HelloGit.txt ...
	7. git add Hello?   # 将以Hello开头后面只有一位的文件的修改提交到暂存区 例如:Hello1.txt,HelloA.java 如果是HelloGit.txt或者Hello.java是不会被添加的
	8. git add -u [<path>]: 把<path>中所有跟踪文件中被修改过或已删除文件的信息添加到索引库。它不会处理那些不被跟踪的文件。省略<path>表示 . ,即当前目录。
	9. git add -A: []表示把中所有跟踪文件中被修改过或已删除文件和所有未跟踪的文件信息添加到索引库。省略<path>表示 . ,即当前目录。


3. 注意的点：
	1. git add . :会监控工作区的状态树，使用它会把工作时的所有变化提交到暂存区，包括文件的修改和新文件，但是不包括删除的文件；
	2. git add -A:提交所有变化，也就是无论是否被tracked到，所有的文件都会被提交到暂存区；
	3. git add -u:提交被修改的和被删除的文件，不包括新的文件，也就是添加被tracked的文件，新的文件还没有被tracked到，所以若是新建的文件不想被提交可以使用此命令；
	4. git的四个分区：工作区，暂存区，本地仓库，远程仓库
4. git add 添加错误文件撤销
	1. git add如果添加错的文件的话；
	2. git status先看一下add中的文件
	3. git reset HEAD 如果后面什么都不跟的话就是将上一次add里面的全部撤销了；
	4. git reset HEAD  XXX/XXX/XXX.java就是将对某一个文件撤销了；

###2. git rm
1. 删除本地和远程的文件(本地和远程仓库的文件都会被删除)
	1. git rm xxx/xxx.java  （  删除工作区文件，并且将这次删除放入暂存区）
	2. git commit -m "删除文件"
	3. git push -u origin master
2. 只删除远程的文件
	1. git rm --cached xxx/xxx.java
	2. git commit -m "删除远程文件"
	3. git push -u origin master

##二、提交代码

###1. git commit 命令用于将暂存区中的变化提交到仓库区。
1.  git commit -m "message" (-m参数用于指定 commit 信息，是必需的。如果省略-m参数，git commit会自动打开文本编辑器，要求输入)
2.   git commit <filename>  -m "message"  : git commit命令可以跳过暂存区，直接将文件从工作区提交到仓库区。


###2. git status 查看工作目录和暂存区的状态
1. git status 查看当前 作用：使用此命令能看到那些修改被暂存到了，那些没有，那些文件有没有被git tracked到，git status不显示已经commit到项目历史中去的信息
2. git status -s 使用，可以简便显示信息



##三、分支管理

###1. 创建分支  git branch <本地分支名>
1. 创建本地分支的两种办法：
	1. git branch <本地分支名>
	2. git checkout -b <本地分支名>  ；创建本地分支并且切换到新创建的分支上

2. 删除本地分支 git branch -d <本地分支名>
	1. 查看分支名
		1. git branch  查看本地分支名
		2. git branch -a 查看远程分支名和本地分支

	2. 删除本地分支git branch -d <本地分支名>

3. 创建远程分支：也就是提交本地分支到远程分支
	1. git push origin <本地分支名>  

4. 删除远程分支：
	1. git push origin --delete <远程分支>

5. 本地分支与远程分支光联
	1. git branch -set-upstream <本地分支名> origin/<远程分支名>
	2. 本地分支和远程分支关联之后就可以不用指定本地和远程分支名了，可以直接进行推送和拉取了





##四、 拉去代码git pull/git fetch

###1. git pull
1. git pull origin <remote_branch>：<local_branch> 这个是拉取合并到不是当前本地分支上
2. git pull origin <remote_branch>将远程的指定分支上的信息拉去并合并到当前分支上
3. git pull 将本地当前分支关联的远程分支上的信息拉取到本地并合并

###2.git fetch
1. git fetch origin master:tmp
	1. git fetch origin master:tmp//在本地新建一个tmp分支，并拉取master分支的代码到本地
	2. git diff tmp//将本地代码和刚刚拉取到tmp分支的代码做比较
	3. git merge tmp//合并tmp的代码到master分支上
	4. git branch -d tmp/删除tmp分支

2. git fetch origin//指定了远程主机名通常远程和本地的分支默认是master分支
3. git fetch origin dev//指定了远程分支，只会拉取远程指定分支的修改部分；
###3. git fetch 和git pull的区别
1. 差异：git pull 是git fetch 和 git merge两个步骤的结合；
2. git pull 会自动merge，而git fetch并不会自动合并，需要手动合并

##五、代码合并

###1. git merge 

1. git merge dev //用于合并dev分支到当前分支
2. git merge --no-ff -m "merge with no-ff" dev //加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并；

##六、代码回滚

###1. git reset HEAD^
1. 恢复成上次提交的版本

###2. git reset HEAD^^
1. 恢复成上上次提交的版本，就是多加了^,以此类推或者使用~次数

###3. git reflog

###4. git reset --hard 版本号
--soft：只是改变HEAD指针指向，缓存区和工作区不变
--mixed：修改HEAD指针指向，缓存区内容丢失，工作区不变
--hard：修改HEAD指针指向，暂存区内容丢失，工作区回复以前的状态；