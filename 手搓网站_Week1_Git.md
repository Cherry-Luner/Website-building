## 手搓网站_Week2_Git

### 什么是Git

Git是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到 非常大的项目版本管理。这是`Linus Torvalds`为了帮助管理Linux内核 开发而开发的一个开放源码的版本控制软件。 分布式：每个人在本地都拥有一个独立的代码仓库用于管理，各种版本 控制的操作都可以在本地完成。 版本管理：对于文件修改的管理。

### Git的工作流程

<img src="E:\Typore-Picture\image-20230322202502696.png" alt="image-20230322202502696" style="zoom:67%;" />

### Git的工作原理

![image-20230322202835673](E:\Typore-Picture\image-20230322202835673.png)

• workspace：工作区，存放项目代码的地方。 

• Index/Stage：暂存区，用于临时存放你的改动，保存即将提交的文件列 表信息。 

• Repository：仓库区，存放数据的位置，这里面有你提交到所有版本的 数据。其中HEAD指向最新放入仓库的版本。 

• Remote：远程仓库，托管代码的远程服务器。

### Git的本地操作

#### 安装配置

Windows/MacOS：官网下载安装。

 Linux：

```bash
apt-get install git
```

配置用户名和邮箱

```bash
git config --global user.name <username>  仅作为远程提交时的身份显示，无身份验证作用
git config --global user.email <email>  不提倡随意设置，最好与Github的邮箱相同。
```

查看配置信息

```bash
git config --list
git config user.name
git config user.email
```

#### 本地常用操作

```bash
git init	#初始化仓库
git add <filename>	#将文件添加到暂存区
git rm <filename>	#从暂存区和工作区删除
git rm --cached <filename>	#只从暂存区中移除
git status	#查看仓库状态
git diff #暂存区与工作区
git diff --cached #暂存区与上一次提交
git diff <first-branch> <second-branch> # 两个分支的差异
git commit -m <message>#After git add
git log	#查看历史提交记录

#回退，会删除当前的版本。比如version1 -> version2  在version2下回退，那么version2会消失
git reset HEAD^	# 回退到上一个版本，修改内容进工作区和暂存区，当前版本会消失
git reset --mixed <version>	#回退，修改内容进工作区
git reset --soft <version>	#回退，修改内容进暂存区
git reset --hard <version>	#修改内容清除，恢复该分支初始态
#不知道版本号怎么办？git log！

git reset HEAD <filename>	#撤销add操作

#分支管理
git branch <branch-name>#创建分支
git branch -v #查看所有分支
git branch -d <branch-name>#删除分支
git branch -m <old-name> <new-name> #分支改名
git checkout <branch-name>#切换分支
git checkout -b <branch-name>#创建新分支并切换（以当前分支为基础)
#分支合并:
git merge <branch-name># 将其他分支合并进本分支
#分支冲突:两分支对同一内容做了不同的修改
#解决方法:根据git的提示信息手动修改冲突位置，如VScode等编辑器中可以直接选择保留哪一个分支的内容

git remote add <name> <url> # name通常为origin
git remote -v #查看远程仓库地址
git remote rm <name>#解除绑定
git clone <url> #克隆仓库（对于开源项目均可以使用)
git pull origin <branch-name> ( :<branch-name>)   #拉取并合并仓库，一般拉取某一分支而不是全部仓库
git fetch origin <branch-name> ( :<branch-name>)  #同为pull，没有合并操作
git push origin <branch> #将本地仓库推送到远程仓库，只能推送有权限的
```

### 注意事项

**pull、clone、fetch的区别:**

git clone是直接把远程仓库复制到本地，不需要`git init`;

git fetch是拉取远程分支，只拉取不合并，需要手动merge到本地分支;

git pull = git fetch + git merge，直接将本地分支更新到远程版本。

使用pull和fetch可能会出现冲突，原因是远程版本和本地版本对于同一内容有不同修改，解决方法是拉取到一个新的分支，手动解决冲突后再merge。

推送到别人的仓库:

别人的仓库是无法直接push的(不能往别人的仓库里随意丢东西)，一种方法是让别人把自己加为collaborators，另一种方法则是发起pull request (github中为pullrequest, gitlab为merge request) 。

**gitignore**

在实际开发时，我们并不需要提交所有的文件。例如我们使用Visual Studio写了一个C++程序，项目文件夹会相当大，但是我们其实只需要提交其中的.cpp文件即可，这时我们如果直接使用git add .，就会提交很多不必要的文件。

`Gitignore` 的作用是设置文件的忽略规则，让Git根据该规则有选择地忽略文件的更改。使用`gitignore`的方式便是在目录中创建名为`.gitignore`的文本文件，在该文本文件里编写忽略规则。

最常见的规则:

直接写上文件名，例如: `main.o`

重名文件则需要给出目录，例如:

`./bin/ main.o`

忽略文件夹:

#忽略所有名为bin 的文件夹内的文件`bin/`

#忽略当前目录下的 bin文件夹内的文件`./bin/`

如果想要进一步了解（(通配符，反向操作...):语法详解:https://blog.csdn.net/nyist_zxp/ article/details/119887324

`Gitignore`模板:`https:// github.com/github/gitignore`