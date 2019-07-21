#### git 

Git 是一个开源的分布式版本控制系统

CVS 及 SVN 都是集中式的版本控制系统，而 Git 是分布式版本控制系统，集中式和分布a式版本控制系统有什么区别呢？
集中式：一定要联网，中央电脑必须。
公布式：不需要联网，中央电脑可有可无。

安装：直接下一步下一步。

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

把文件放进仓库
```
$ git add readme.txt
$ git commit -m “描述”
```

查看仓库状态  
`$ git status`

查看修改的地方  
`$ git diff readme.txt`

修改仓库的文件与提交文件到仓库的命令一样  
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
`$` git reset --hard commit_id(版本的id)`

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

***
### git的命令  
#### 分支：
##### 创建并切换：
`$ git checkout -b dev`
##### 相当于：
```
$ git branch dev
$ git checkout dev
```

#### 查看分支：
`$ git branch`

#### 切换分支：
`$ git checkout master`

##### 合并分支：
`$ git merge dev`

##### 删除分支：
`$ git branch -d dev`

##### 带参数的log查看分支合并的情况：
`$ git log --graph --pretty=oneline`

#### 分支管理策略

##### 非快速的方式合并分支：要新commit所以就-m，这种方式能看出来曾经做过合并
`$ git merge --no-ff -m "merge with on-ff" dev`

##### 将工作区隐藏  
`$ git stash`

##### 查看隐藏的列表
`$ git stash list`

##### 切换回隐藏区，同时把stash的记录删除  
`$ git stash pop`

##### 切换回隐藏区，不删除stash的记录
`$ git stash apply stash@{0}`  

##### 强制删除未合并的分支
`$ git branch -D feature-vulcan`

***

#### 远程学习

本地 Git 仓库和 GitHub 仓库之间的传输是通过 SS  
H 加密的，所以，需要一点设置：  

在本地增加.ssh  
`$ ssh-keygen -t rsa -C "1574165902@qq.com"`

在`C:\Users\Administrator\.ssh`目录下能看到`id_rsa.pub`和`id_rsa`文件，前者公有，后者保密  

登陆 `GitHub`，打开`“Account settings”`，`“SSH Keys”`页面：  
然后，点`“Add SSH Key”`，填上任意 `Title`，在 `Key` 文本框里粘贴 `id_rsa.pub` 文件的内容：  

***

在github上创建仓库，后的提示：  

建立远程：`$ git remote add origin git@github.com:Allen151/learngit.git`  
推仓库上去`git push -u origin master`
`-u`是第一次推上去，建立关联  


第二次后` $ git push origin master` 把本地master分支的最新修改推送至GitHub  

***

#### 从远程库克隆  

创建`gitskills`，勾选要` README  `

克隆命令：Git 支持多种协议，包括 https，但通过 ssh 支持的原生 git 协议速度最快。  
`$ git clone git@github.com:allen151/gitskills.git`
***
分支


多人协作

github上新建了分支，本地仓库无法识别问题  

```
$ git checkout master   //切换到master分支
$ git pull				//pull一下，更新一下
$ git branch -a 		//查看就可以看到分支了
```
然后本地分支，与github的分支连接
`$ git checkout -b dev origin/dev`


