# 设置用户名邮箱

说明：**签名的作用是区分不同操作者身份**。用户的签名信息在每一个版本的提交信息中能够看到，以此确认本次提交是谁做的。 **Git 首次安装必须设置一下用户签名，否则无法提交代码**。

**注意**： 这里设置用户签名和将来登录 GitHub（或其他代码托管中心）的账号没有任何关系。

```java
git config --global user.name abc #有户名
git config --global user.email abc@123.com
```



# 查看设置过用户签名

```
cat ~/.gitconfig
```



# 初始化本地库

### ==打开文件所在位置，鼠标右键选中Git Bash here，进入图形化页面==

## 快捷键的使用

### ==ESC+dd删除一行==

### ==复制粘贴ctrl+ins shift+ins==

### ==q为退出键==

```
git init    初始化并创建.git文件（需打开隐藏的项目）
ll 			查看当前文件下的数量
ll -a 		查看可以进入那些文件
cd .git/  	进入.git文件下
cd ..    	回退到上级目录
```



# 查看本地库状态

```
git status 				首次查看（工作区没有任何文件）
	On branch master   	在主分支下
		No commits yet	没有任何执行

```
## ==编辑5步骤==

1. ==vim hello.txt      				       新增文件（hello.txt）==
2. ==按下键盘的‘i’键                         即可添加内容==
3. ==在第一行先按"ESC"再按"yy"   即可复制本行内容==
4. ==按下"p"键                                 即可粘贴复制的内容==
5. ==再次按"ESC",并且输入":wq"   即可完成编辑==
## ==cat hello.txt  查看文件内容==



# 添加暂存区

```
git status       	        查看当前文件的状态
根据下方提示将文件添加至暂存区： git add hello.txt(文件名)
再次查看状态    git status     发现红色的字变成绿色
git rm --cached hello.txt   #移除暂存区的hello.txt
```



# 提交本地库

```
git status   查看状态准备提交
git commit -m "记录提交信息名，方便日后查看进度" hello.txt(文件名)

```



# 查看提交记录

```
git reflog    查看提交记录（显示的是“”内的内容）
git log			查看提交的详细信息
```



# 修改文件

```
vim hello.txt 		进入文件内部（具体步骤见高亮的五步）
git  status 		 提示 hello.txt 被修改过（modified）
git add hello.txt	 将修改的文件再次添加暂存区
git commit -m "second commit" hello.txt  再次提交
git reflog
git status
```



# git log与git reflog区别

git log 命令可以显示所有提交过的版本信息，如果感觉太繁琐，可以加上参数 --pretty=oneline，只会显示版本号和提交时的备注信息。

git reflog 可以查看所有分支的所有操作记录（包括已经被删除的 commit 记录和 reset 的操作）。例如，执行 git reset --hard HEAD~1，退回到上一个版本，用git log则是看不出来被删除的commitid，用git reflog则可以看到被删除的commitid，我们就可以买后悔药，恢复到被删除的那个版本。


# 版本穿梭

```
git reflog  			 首先查看当前的历史记录
git reset --hard xx      切换到xx的指针文件下
git reflog   切换完毕之后再查看历史记录，当前成功切换到了xxx版本
然后对文件进行修改并提交在查看
```

## ==git clean -f -d  清除Untracked files==

# 分支

## 查看分支

```
git branch -v
```

## 创建分支

```
git branch hot-fix
```

## 切换分支

```
git checkout hot-fix
```

## 合并分支

```
git merge hot-fix       在master分支上使用此命令
```

## 冲突合并

```
若两个文件格式一样 但相同行内容不同 就需要人为合并
```
### ==冲突四步走==

1. cat hello.txt	查看文件内容
2. 编辑有冲突的文件，删除特殊符号，决定要使用的内容 git clean -f -d
3. git add hello.txt   提交到本机库
4. git commit -m ""  (master|MERGING)的|MERGING消失了，冲突解决



# 远程仓库操作

```
git remote -v 查看当前所有远程地址别名
git remote add 别名 远程地址
```





# 长传文件到Github

## ==详细步骤==

1. 在Github中创建一个repository，起一个名字，然后复制文件名.git的http网址
2. 在本机创建文件夹，并把所要上传的文件放入其中
3. 在当前文件内右键选中Git Bash Here
4. git init 					  初始化
5. git status 				查看要未提交的文件
6. git add .  				 将当前文件下的所有都上传到暂存区
7. git status 			    若刚才的红字全部变绿，则说明已上传到暂存区
8. git commit -m "init"  提交到本机库
9. git remote -v   		  查看所有别名
10. git  remote add   ‘和Github中创建的文件名相同’的别名   带文件名.git的http网址
11. git remote -v            再次查看别名，发现有有两个，非别是：(fetch)和(push)
12. git push 别名 master       提交到Github
13. 唤醒一个登录的小页面，则说明上传成功就在眼前



