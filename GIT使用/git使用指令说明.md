##git 指令说明
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
	2. git add -A:提交所有变化；
	3. git add -u:提交被修改的和被删除的文件，不包括新的文件
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
1. 作用：使用此命令能看到那些修改被暂存到了，那些没有，那些文件有没有被git tracked到，git status不显示已经commit到项目历史中去的信息

