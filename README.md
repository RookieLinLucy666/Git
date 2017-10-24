# Git Note [![Build Status](https://travis-ci.com/cvno/Git_Project.svg?token=pi6b5mfzZ59odqp5Yuyi&branch=master)](https://travis-ci.com/cvno/Git_Project)

- [基本命令](#基本命令)
- [连接目录,文件和锚点](#目录-文件-锚点)
- [回滚](#回滚)
- [开发模式](#开发模式)
    1. [stash-方式](#stash-方式)
        - [处理bug](#处理bug)
        - [其它命令](#其它命令)
    2. [分支](#分支)
        - [出现bug](#出现bug)
        - [合并](#合并)
- [远程仓库](#远程仓库)
    - [基本使用](#基本使用)
    - [家/公司忘记提交代码](#家/公司忘记提交代码)
- [协同开发](#协同开发)
- [fork](#fork)
- [配置用户信息](#配置用户信息)
- [其它命令](#其它命令)
- [忽略文件](#忽略文件)
- [Github连接方式](#Github连接方式)
    - [https](#https)
    - [ssh](#ssh)

# 基本命令

```sh
git init        # 初始化 生成 .git 文件
git status      #  查看状态
git add .       # 把所有文件添加到暂存区
git add '文件名'   # 添加到缓存去
git reset HEAD .    # 撤销所有的已经add的文件
git reset HEAD -filename # 撤销某个文件或文件夹
git commit -m '提交信息'    # 添加到分支

git commit -a -m '提交信息'   # 一句命令来提交
git checkout -b '分支'    # 创建分支并切换
git branch -vv # 查看本地分支与远程分支之间关联的关系
```

# 回滚

```sh
git log
git reset --hard '版本号'  # 一步到位 git log 中的版本号(随机字符串)
git log   # 这里没有回滚之前的内容

git reflog  # 这里有所有的版本,整个的状况

# 再回滚回去
git reflog
git rest --mix a615783
git checkout '文件名'
git log     # 查看日志 谁提交的,提交信息
```

# 开发模式
## stash方式
### 处理bug

```sh
git stash     # 将当前已经做过的修改，保存到一个临时地方

# 修复 bug
git add .
git commit -m '修复bug'
git stash list  # 查看临时暂存地方
git stash pop   # 临时地方内容重新放回工作区

# 出现冲突，手动解决
'''
<<<<<<< Updated upstream
同城交友网站
张小戈
=======
同城交友网站
张小戈
开发直播功能到一半
>>>>>>> Stashed changes
'''
```
![出现冲突](http://onk83djzp.bkt.clouddn.com/15021201202862.jpg)
> bug 出现的地方可能和正在开发的文件是同一个

### 其它命令

```sh
git stash apply '名称'
git stash drop  '名称'
git stash list
git stash pop
```

## 分支

| 分支 | 版本用处 |
| --- | --- |
| master | 只保留线上版本 |
|  dev(develop) | 保存所有开发版本 |
|  bug | 修复 bug版本/可删除 |


``` sh
git branch      # 查看当前在那个分支
git branch dev      # 创建分支(注意当前所在分支)
git checkout master     # 进入分支
```

### 出现bug

```sh
git checkout master     # 回主分支来修复 bug
git branch bug          # 创建 bug 分支
git checkout bug        # 进入 bug 分支
```
### 合并

```sh
git checkout master     #  回主分支
git merge bug           # 同步已修复 bug 的分支

# 如果出现冲突,手动解决
git add .
git commit -m '解决冲突'

# 删除分支
git beamch -d bug
```
![没有冲突](http://onk83djzp.bkt.clouddn.com/15021209863919.jpg)

# 远程仓库
- 现有的(国内):
    - BitBucket：https://bitbucket.org/
    - 开源中国：http://git.oschina.net/
    - GitCafe：https://gitcafe.com/
    - GitLab：http://www.gitlab.org/
    - coding：https://coding.net/

- 自己/公司搭建(gitlab)

## 基本使用

``` sh
# ---------------- home -----------------
# 新建项目或已有项目
git clone https://github.com/a877252372/wwwww.git

cd wwwww

# 设置远程仓库 并设置别名/已有项目则省略
# 此处使用 https 可能需要输入用户名&密码
git remote add origin https://github.com/a877252372/wwwww.git

git checkout master     # 切换分支
git push origin master      # 推送 同步到仓库 / 可能需要输入用户名&密码

git branch dev origin/dev       # 创建一个镜像分支
git checkout dev 

# 提交代码
git add .
git commit ...
git push origin dev     # 同步到仓库

# ---------------- 公司 -----------------
# 下载代码到本地
git checkout dev
git fetch origin dev    # 同步
git pull origin dev     # 劲大
```
![fetch/pull 区别](http://onk83djzp.bkt.clouddn.com/15021218825961.jpg)


## 家/公司忘记提交代码
>push/下载 代码,先开发别的功能

``` python
git branch dev
git pull origin dev
# 别的功能：
git add .
git commit ...
git push origin dev

# 回到家/功能    !!!!
'''先把代码下载到本地'''
git pull origin dev     # 同步到本地
# 然后解决冲突
```

# 协同开发
>A----B----C(组织/邀请)

- 同一个远程仓库
    1. 代码
    2. 开发 ing
    3. 合并
        - 没问题 > pass
        - 有问题 > 改

![提交晚了出错](http://onk83djzp.bkt.clouddn.com/15021226892328.jpg)

# fork
> 拉到自己的仓库,帮别人修改 bug/修改代码

1. fork别人项目
2. git clone xxxxxx
3. 修改
4. 提交【自己】(自己创建的分支fork仓库)
5. new pull request(去别人的代码仓库提交)
6. 等(等别人通过)
7. fork别人项目




# 配置用户信息

```
git config --local user.name '名称'
git config --local user.email '邮箱'
```

# 其它命令

```sh
git ls-tree head   # 查看版本中所有文件 不包括暂存区
git ls-files -s    # 查看暂存区和版本中所有文件
vim .git/config     # 查看当前项目配置
```
# 目录-文件-锚点
在写README.md文件时,GitHub不能解析[toc] 这个命令,那我们就来手写.

**前提:**
使用的是markdown语法的超链接 `[描述](网址)`,所有的url地址前缀都是基于当前
存储库

- [锚点](#锚点)
- [连接到文件和目录](#连接到文件和目录)

## 锚点
基于当前页面

```
[锚点一](#锚点一)
[锚点二](#锚点二)
```
---

- [锚点一](#锚点一)

[锚点二](#锚点二)

## 连接到文件和目录
**当前存储库 markdown 生成的url 前缀统一是当前存储库的根目录**

1. 链接接文件 or 目录

```
[文件1](/文件1)
[文件2](/文件2.py)
[目录1](/目录1)
```
[文件1](/文件1)

[文件2](/文件2.py) 不存在的文件示范

[目录1](/目录1)

2. 链接到目录下的文件

```
[文件2](/目录1/文件2.py)
```
[文件2](/目录1/文件2.py)

不管这个存储库有多少级目录,不管`README.md`在哪个文件夹下面,`链接目录下在文件`**要基于存储库的根目录至这个文件的绝对地址写全**,

markdown生成的url都是基于存储库根目录来进行生成,不信?试试看 [传送门](/目录1)

PS: `[]` 中括号的内容可以随意写,`()` 小括号里面的才是真实的URL地址

# 忽略文件
`vim .gitignore`
[Python .gitignore Github](https://github.com/github/gitignore/blob/master/Python.gitignore)


# Github连接方式
## https
## ssh

```sh
# 生成
ssh-keygen
# 查看并拷贝公钥
cat ~/.ssh/id_rsa.pub
# 公钥放在 github
# clone 克隆
git clone '仓库 ssh 地址'
```

