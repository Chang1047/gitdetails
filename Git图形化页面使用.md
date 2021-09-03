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

## 拉取远程库到本地库

```
在Github上修改文件，并提交。
git pull 别名 master     从别名拉取到master分支上
cat 文件名				  可看到从Github上修改后痕迹	
```



## 克隆远程库到本地

```
git clone 		远程地址（http.git网址）
ll         		查看需要进入的文件名
cd 				文件名/
git remote -v   查看别名(链接前面的别名为origin)


clone 会做如下操作：
拉取代码。
初始化本地仓库。
创建别名。
```



## 团队内协作

1. ==选择邀请合作者：Settings->Mange access invit==
2. ==复制邀请的网址==
3. ==目标合作者接收到网址，用浏览器打开它，点击接受邀请。==
4. ==接受邀请成功之后，可以在目标合作者Github账号上看到将来共同开发远程仓库。==
5. ==标合作者可以修改内容并 push 到远程仓库。==
6. ==回到发送合作邀请者的 GitHub 远程仓库中可以看到，最后一次是目标合作者提交的。==



## 跨团队协作

一、将远程仓库的地址复制发给邀请跨团队协作的人，比如Others。

二、在Others的 GitHub 账号里的地址栏复制收到的链接，然后点击 网页右上方的Fork按钮，将项目叉到自己的本地仓库。

​		叉成功后可以看到当前仓库信息。

三、Others就可以在线编辑叉取过来的文件。

四、Others编辑完毕后，填写描述信息并点击左下角绿色按钮提交。

五、接下来点击上方的 Pull 请求，并创建一个新的请求。

六、回到My GitHub 账号可以看到有一个 Pull request 请求

​		进入到聊天室，可以讨论代码相关内容。

​		点击Others描述信息即可查看源代码

七、如果代码没有问题，可以点击 Merge pull reque 合并代码。

​		下面可以填写对合并代码的描述，团队内可以看到

​		再次确认提交



## SSH免密登录

github->code->ssh下面有：

```
You don't have any public SSH keys in your GitHub account. You can [add a new public key](https://github.com/settings/ssh/new), or try cloning this repository via HTTPS.
```

1. 先到用户的主页目录，删除.ssh文件夹（如果没有.ssh文件夹，忽略此步）
2. ssh-keygen -t rsa -C  Chang1047.com(邮箱地址)
3. 然后按三次回车，生成一个私钥和公钥
4. 把公钥内的内容复制到github账号->settings->ssh and gpg->ssh keys->add  new ->复制到key中
5. 若出现一个钥匙形状的图案，则添加成功！
6. 刷新，ssh下方出现git@github.com:Chang1047/gitdetails.git，则成功！



# Idea忽略.idea之类的文件

在idea内

Settings->Editor->File Type->Ignored Files and Folders->添加要忽略的文件即可

不需要那么麻烦，so easy！



# IDEA集成GitHub

## 设置GitHub账号

Setting->Version Control->GitHub->add account 自动跳转页面，添加成功！



## 分享项目到GitHub

VCS->ShareProject Github->使用token登录，点击Generate，到Github复制token粘贴过来即可->Share



## 推送代码到远程库

Git->commit(起个名字)

在Github远程库中复制ssh的git网址

Git->Push->origin->Define remote->添加刚才复制的网址(给Name去个名字)->ok->选中刚才起的名字->Push

## 拉取远程库代码合并本地库

修改远程库的代码

Git->pull->选择ssh网址的名字->ok



## 克隆代码到本地

在菜单栏的File->Close Project->Get From VCS->选择git，复制远程库的git网址，选择文件放的位置



# Gitee码云的使用

码云是开源中国推出的基于 Git 的代码托管服务中心， 

```
网址是 https://gitee.com
```

使用方式跟 GitHub 一样，而且它还是一个中文网站。



# Gitee导入Github文件

用户名旁边的+->新建仓库->右上角有一个导入->复制github的http网址

