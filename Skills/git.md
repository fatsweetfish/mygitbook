## Git 实用操作



### 1.一般操作

#### 配置

```
git -config --global user.name "fatsweetfish"
git -config --global user.email "xxx@xxx.com"
```

#### 创建切换分支

```
git checkout -b dev   等同于 git branch dev 和　git checkout dev
```

#### 查看分支

```
git branch -a/--all　所有
git branch -r　远程
git branch -vv 本地分支关联的远程分支
```

#### 查看远程仓库

```
git remote
git remote -v 列出url
```

#### 关联分支

关联的目的在于git pull和git　push不需要指定远程分支

```
git branch --set-upstream-to=origin/dev dev
git branch -vv　本地分和远程分支关联的情况
git checkout -b myrelease origin/myrelease  把远程myrelease分支checkout 到本地并跟踪　
git push -u origin master    push并跟踪
```

心得：本地分支可以关联多个远程分支，但是这些分支应该属于不同的仓库，不能关联同一个仓库的不同分支

#### 同步代码

<font color=red>**git pull <远程仓库> <远程分支> **</font>

```
git pull origin dev
```

#### 提交代码

<font color=red>**git push <远程仓库> <本地分支名>:<远程分支名>**</font>

```
git push origin master:dev 将本地master分支推送到远程origin的dev分支
git push origin :dev　本地分支为空，等同于推送一个空本地分支到dev，表示删除远程dev分支
＃效果等于
git push origin --delete dev
```

<font color=red>**git push <远程仓库> <本地分支名>**</font>　最常用

```
git push origin master 将本地master推送到origin的master分支，如果远程master不存在则创立
```

<font color=red>**git push <远程仓库> **</font>

```
git push origin　表示关联了远程分支，如果关链的远程分支不止一个，要指明远程仓库
```

<font color=red>**git push **</font>

```
git push  表示本地分支关联了远程分支
```



**完整的提交**

```
git add .
git commit -m "sxxxx"
git push -u origin master  把本地master代码提交到远程origin/master分支, -u表示跟踪，揭交后就本地master与origin　master有关联了
```



#### 缓存远程代码到本地

<font color=red>**git fetch  远程仓库　远程分支**</font>

```
git fetch   已经有关联的可以用
git fetch origin　　缓存远程仓库所有分支到本地
git fetch origin dev 缓存远程dev分支到本地，存在本地临时分支origin/dev
```



#### 合并代码

<font color=red>**git merge 源分支 目标分支 **</font> 把源分支合并到目标分支

<font color=red>**git merge 源分支 **</font>　把源分支合并到当前分支

```
$ git checkout feature
$ git merge master

等同于
$ git merge master feature
```



```
git checkout master
git merge origin/home　把远程origin仓库下home分支merger到本地master分支
git status
git add .
git commit -m "merge home branch to master"
git push origin master
```

开发分支合并到master分支

```
git checkout dev
git pull
git checkout master
git merge dev
git push -u origin master
```



#### 删除分支

```
git branch -d dev　　　删除本地分支
git branch -D dev:　　　强制删除本地分支
git push origin :dev　　　删除远程分支
git push origin --delete dev  删除远程分支
```

删除远程仓库

```
git remote rm paul
```



#### 版本回退

```
git reset --hard <commit_id>
git push origin master -f
```



#### commet修改

```
git commit -m "ssssss"
＃修改内容
git commit --amend
```



#### 删除缓存区所有文件命令

```
git rm -r --cached .   #主要这个点一定要写
```



#### 给分支重命名

```
git branch -m oldname newname
```

#### 远程仓库重命名

```
git remote rename pb paul
```

#### 远程操作

<font color=red>**git remote **</font>

```
git remote -v　查看远程仓库　-v带仓库url信息
git remote add pb https://xxxxx 增加远程仓库pb
git fetch pb　缓存远程仓库pb到本地
git remote show origin/pb 查看远程仓库的信息
git remote rename pb paul 远程仓库重命名
git remote rm paul　　删除远程仓库

```

#### git的tag功能

<font color=red>**git tag **</font>

```
git tag v1.0　打在当前分支最新commit上
git tag 查看标签
git show v1.0

给之前提交的代码打标签
git log --pretty=online --abbrev-commit
找到简化的commit id f92853
git tag v0.9 f92853

给标签带说明
git tag -a v1.0 -m "version 1.0 release"
```

我们常常在代码封板时,使用git 创建一个tag ,这样一个不可修改的历史代码版本就像被我们封存起来一样,不论是运维发布拉取,或者以后的代码版本管理,都是十分方便的

git 下打标签其实有2种情况

- 轻量级的：它其实是一个独立的分支,或者说是一个不可变的分支.指向特定提交对象的引用
- 带附注的：实际上是存储在仓库中的一个独立对象，它有自身的校验和信息，包含着标签的名字，标签说明，标签本身也允许使用 GNU Privacy Guard (GPG) 来签署或验证,电子邮件地址和日期，一般我们都建议使用含附注型的标签，以便保留相关信息

所以我们推荐使用第二种标签形式

##### 创建tag

```
git tag -a V1.2 -m 'release 1.2'
```

上面的命令我们成功创建了本地一个版本 V1.2 ,并且添加了附注信息 'release 1.2'

##### 查看tag

```
git tag
```

要显示附注信息,我们需要用 show 指令来查看

```
git show V1.2
```

但是目前这个标签仅仅是提交到了本地git仓库.如何同步到远程代码库

```
git push origin --tags
```

如果刚刚同步上去,你缺发现一个致命bug ,需要重新打版本,现在还为时不晚.

```
git tag -d V1.2
```

到这一步我们只是删除了本地 V1.2的版本,可是线上V1.2的版本还是存在,如何办?这时我们可以推送的空的同名版本到线下,达到删除线上版本的目标:

```
git push origin :refs/tags/V1.2
```

如何获取远程版本?

```
git fetch origin tag V1.2
```

这样我们可以精准拉取指定的某一个版本.适用于运维同学部署指定版本.



#### 忽略文件.gitignore

```
#
build
_book
```



#### **git rebase**

Rebase 是合并两个分支的另一种方式。Rebase 把所有的提交压缩成一个 “patch”。然后把 patch 添加到目标分支里。和 merging 不同，rebasing 清除了历史，因为它完全是从一个分支转移到了另一个分支。在这个过程中，多余的记录被移除了。

把 feature 分支 rebase 到 master 分支上。

```text
$ git checkout feature
$ git rebase master
```

### 2.流程操作

* **撤消修改**

  * 末git add

    ```
    git checkout -- filename 放弃修改，让文件回到最近一次git commit或git add 状态
    git checkout . 放弃当前目录修改
    ```

  * 已经add,缓存了代码

    ```
    git reset HEAD filename
    git reset HEAD .　　放弃所有缓存的文件
    ＃或者
    git rm -r --cached . 
    ```

  * 已经commit

    ```
    git reset --hard HEAD^ 回退到上一次的状态
    git reset --hard commitid 回退到某一次的版本
    ```

* **新建一个仓库推送到远端**

  ```
  mkdir mydoc
  cd mydoc
  touch README.md
  git init
  git add .
  git commit -m "init commit"
  git remote add origin https://github.com/fatsweetfish/mydoc
  git push -u origin master
  ```

* **github从原项目同步fork出来的项目**

  以我fork的battery-histroian为例，专门建了一个google分支专门同步原项目

  方法１:在源码操作

  ```
  
  git checkout google  (已关联)
  git remote add upstream https://github.com/google/battery-histroian
  git remote -v 将会看到远程分支多了一个upstream仓库
  git fetch upstream master 缓存远程ustream master分支到本地，保存在临时分支upstream/master上
  git merge upstream/master 合并到本地google分支，相当于git merge FETCH_HEAD
  git log
  git push
  ```

  

  方法２:在github界面操作

  ```
  New pull request后
  base fork选自己fork后的项目的google分支
  head fork选原项目的master分支
  
  如果base fork选择自己fork的项目后变成两个master,点一下"compare across forks"
  Creat pull request
  Merge pull request
  ```

* **删除远程文件**

  ```
  git rm xxxfile
  git rm -rf xxxdir
  
  git commit -m "delete files"
  git push origin master
  ```

  

### 3.问题

* git branch -r无法查看远程分支需要手动更新远程仓库

```
git fetch origin
```

* git pull产生冲突

  ```
  git reset --merge 回退
  ```

* git push产生冲突

  ```
  git checkout --theirs conflicted-file 保留远端文件
  git checkout --ours conflicted-file　保留本地的
  ```

  























































## Ref:

[github上fork项目同步更新原项目](https://www.cnblogs.com/eyunhua/p/8463200.html)