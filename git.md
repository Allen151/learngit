## git学习笔记
***

Git 是一个开源的分布式版本控制系统

CVS 及 SVN 都是集中式的版本控制系统，而 Git 是分布式版本控制系统，集中式和分布式版本控制系统有什么区别呢？
集中式：一定要联网，中央电脑必须。
公布式：不需要联网，中央电脑可有可无。

安装git：下载软件后，直接下一步下一步完成安装。

设置用户
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```


创建本地仓库

创建目录/进入目录/查看路径
```
$ mkdir learngit
$ cd learngit
$ pwd
```

使目录成为仓库  
`$ git init`

创建readme.txt，把文件放进仓库
```
$ git add readme.txt
$ git commit -m “描述”
```

查看仓库状态  
`$ git status`

查看修改的地方  
`$ git diff readme.txt`

更新仓库的文件与提交新文件到仓库的命令一样  
```
$ git add readme.txt
$ git commit -m “描述”
```

查看文件的修改日志    
`$ git log `

文件修改日志以一行显示  
`$ git log --pretty=oneline`

返回到上一次修改的状态  
`$ git reset --hard HEAD^`

查看文件的内容  
`$ cat readme.txt`

返回到指定commit_id的版本  
`$ git reset --hard commit_id(版本的id)`

历史的id  
`$ git reflog`

清除工作区的更改，-- 很重要，如果没有就是创建一个新的分支了  
`$ git checkout -- hello.txt`

只放到缓存区，还没commit，退回工作区，然后清除工作区  
`$ git reset HEAD hello.txt`

文件已经commit，删除文件的方法  
```
$ git rm readme.txt
$ git commit -m “remove readme.txt”
```

恢复已经删除分支的文件  
`$ git checkout HEAD^ -- readme.txt`

#### 分支
***
创建并切换：  
`$ git checkout -b dev`

相当于：
```
$ git branch dev   //创建分支
$ git checkout dev  //切换分支
```

查看分支：  
`$ git branch`

切换分支：  
`$ git checkout master`

合并分支：  
`$ git merge dev`

删除分支：  
`$ git branch -d dev`

带参数的log查看分支合并的情况：  
`$ git log --graph --pretty=oneline`

### 分支管理策略
***
非快速的方式合并分支：要新commit所以就-m，这种方式能看出来曾经做过合并  
`$ git merge --no-ff -m "merge with on-ff" dev`

将工作区隐藏  
`$ git stash`

查看隐藏的列表  
`$ git stash list`

切换回最近的隐藏区，同时把stash的记录删除  
`$ git stash pop`

切换回隐藏区，不删除stash的记录  
`$ git stash apply stash@{0}`  

强制删除未合并的分支  
`$ git branch -D feature-vulcan`

### 远程学习
***

本地 Git 仓库和 GitHub 仓库之间的传输是通过 SSH 加密的，所以，需要配置一下    

在本地增加.ssh，如果已经有就不需要增加了  
`$ ssh-keygen -t rsa -C "1574165902@qq.com"`

在`C:\Users\Administrator\.ssh`目录下能看到`id_rsa.pub`和`id_rsa`文件，前者公有，后者保密  

登陆 `GitHub`，打开`“Account settings”`，`“SSH Keys”`页面  

然后，点`“Add SSH Key”`，填上任意 `title`，在 `Key` 文本框里粘贴 `id_rsa.pub` 文件的内容：  

在github上创建仓库，后的提示：  

本地建立远程：`$ git remote add origin git@github.com:Allen151/learngit.git`  
推仓库上去`git push -u origin master`  
`-u`是第一次推上去，建立关联，之后推上去就不用了  

第二次后` $ git push origin master` 把本地master分支的最新修改推送至GitHub  

### 将远程库克隆至本地  
***

在github上创建`gitskills`库，用于实验，勾选要` README  `

克隆命令：Git 支持多种协议，包括 https，但通过 ssh 支持的原生 git 协议速度最快。  
`$ git clone git@github.com:allen151/gitskills.git`

### 多人协作
***

github上新建了分支，本地仓库无法识别问题  

```
$ git branch -a         //查看本地仓库与远程仓库的所有分支
$ git checkout master   //切换到master分支
$ git pull				//pull一下，更新一下
$ git branch -a 		//查看所有分支是不是更新了
```
然后本地创建一个分支，与github的分支连接
`$ git checkout -b dev origin/dev`

### 标签
***
标签也是个快照，但是不会移动的，以下为当前指针打标签  
`$ git tag v1.0`

为过去的时间点打标签  
```
$ git log --pretty=oneline --abbrev-commit   //找到id
$ git tag v0.9 c6ecc61    //为这个id打标签
```  
复杂的添加标签方式，有描述  
`$ git tag -a v1.1 -m "这里添加的.project文件是HBuilder项目的默认文件" 5cf895a`  

查看标签的详细事情  
`$ git show v1.1`  

删除标签  
`$ git tag -d v0.9`

推标签到远程  
`$ git push origin v1.0`  

一次性推全部标签到远程  
`$ git push origin --tags`  

删除远程的标签  
```
$ git tag -d v1.0  //先在本地删除  
$ git push origin :refs/tags/v1.0     //再删除远程的
```  

设置git显示不同的颜色，git本来就有颜色显示了  
`$ git config --global color.ui true`  

配置别名，不学，因为用默认的有利于学习记忆  

搭建私人git仓库不学，不想花太多时间在这上面  