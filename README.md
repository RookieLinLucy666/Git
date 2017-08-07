# Git Note

- 修复1 bug
- 修复2 bug


# 基本命令

```
git init        # 初始化
git status      #  查看状态
git add .
git add '文件名'   # 添加到缓存去
git commit -m '提交信息'    # 提交到?
```

# 回滚

```
git reflog

# 再回滚回去
git redlog
git rest --mix a615783
git checkout '文件名'
```

# 开发模式
## 1.stash 方式
### 处理 bug

```python
git stash     # 将当前已经做过的修改，保存到一个临时地方

# 修复 bug
git add .
git commit -m '修复bug'
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
### 其它命令

```python
git stash
git stash apply ‘名称’
git stash drop  ‘名称’
git stash list
git stash pop
```

## 2. 分支

| 分支 | 版本用处 |
| --- | --- |
| master | 只保留线上版本 |
|  dev(develop) | 保存所有开发版本 |
|  bug | 修复 bug版本/可删除 |


``` python
git branch dev      # 创建分支(注意当前所在分支)
git checkout master     # 进入分支
```

### 出现 bug

```python
git checkout master     # 回主分支来修复 bug
git branch bug          # 创建 bug 分支
git checkout bug        # 进入 bug 分支
```
### 合并

```python
git checkout master     #  回主分支
git merge bug           # 同步已修复 bug 的分支

# 如果出现冲突,手动解决
git add .
git commit -m '解决冲突'

# 删除分支
git beamch -d bug
```

# 远程仓库
>国内:
>BitBucket：https://bitbucket.org/
>开源中国：http://git.oschina.net/
>GitCafe：https://gitcafe.com/
>GitLab：http://www.gitlab.org/
>coding：https://coding.net/

## 基本使用

``` python
# 新建项目或已有项目
git clone https://github.com/a877252372/wwwww.git
cd wwwww

# 设置远程仓库 并设置别名/已有项目则省略
git remote add origin https://github.com/a877252372/wwwww.git

git checkout master
git push origin master      # 同步到仓库

git branch dev origin/dev       # 创建一个镜像分支
git checkout dev 

# 提交代码
git add .
git commit ...
git push origin dev     # 同步到仓库

# 下载代码到本地
git checkout dev
git fetch origin dev    # 同步
git pull origin dev     # 劲大
```

## 家/公司忘记提交代码
>push/下载 代码,先开发别的功能
>

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
>A,B,C(组织/邀请)

- 同一个远程仓库
    1. 代码
    2. 开发 ing
    3. 合并
        - 没问题 > pass
        - 有问题 > 改

# fork

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

```
git ls-tree head   // 查看版本中所有文件
git ls-files -s    // 查看暂存区和版本中所有文件
```

#忽略文件
`vim .gitignore`
[Python .gitignore Github](https://github.com/github/gitignore/blob/master/Python.gitignore)



