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


