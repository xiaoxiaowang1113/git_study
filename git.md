# Git是什么

## 1、了解Git

Git是一个免费的、开源的`分布式版本控制系统`，可以高速处理从小型到大型的各种项目
版本控制：是一种记录文件内容变化，以便将来查阅特定版本修订情况的系统
了解一下：集中式与分布式版本控制工具

         -- 集中式版本控制工具：如CVS、`SVN`等，都有一个单一的几种管理服务器，保存所有文件的修订版本，而协同工作的人通过客户端连接到这台服务器，从而取出最新的文件或者提交更新。缺点：中央服务器的单点故障；多(程序员)对一(中央服务器)
    
         -- 分布式版本控制工具：如git,客户端取的不是最新的文件快照，而是把代码仓库完整的镜像下来到本地库(克隆/备份)

工作机制：

![1](img\2.png)

## 2、 常见命令：

| git config --global user.name 用户名 | 设置用户签名的姓名 |
| ------------------------------------ | ------------------ |
| git config --global user.email 邮箱  | 设置用户签名的邮箱 |
| git init                             | 初始化本地库       |
| git add 文件名                       | 添加到暂存区       |
| git commit -m “日志信息” 文件名      | 提交到本地库       |
| git reset --hard 版本号              | 版本穿梭           |
| git status                           | 查看本地库状态     |
| git reflog/git log                   | 查看历史记录       |



## 3、 常见命令的使用

git restore <file>...                             to discard changes in working directory)          取消修改

1、本地首先创建对应gitcode对应的工作区，在这个文件夹下使用git bash

> git init 初始化git
>
> 将文件传入对应文件夹

2、存入暂存区

> git add .			存入所以改变的到暂存区
>
> git add a.text   存入对应文件名到暂存区
>
> git test/			存入对应文件夹到暂存区



3.存入仓库

> git commit -m ”日志信息“  文件名

4、

本地误删除，但未提交删除操作，复原：

> git restore 文件名

本地误删除，但已经提交删除操作，复原：

也叫版本切换

> 版本回退 ，git reset --hard 版本号（为希望复原的版本号）

本地误删除，但已经提交删除操作，复原：

> 版本恢复（撤回操作），git revert 版本号（为错误提交的版本号）





## 4、分支操作：（本质是引用）

### 4.1、分支的好处

 同时并进行多个功能开发，提高了开发效率

各个分支再开发过程中，如果某个分支开发失败，不会对其他分支有任何影响，失败的分支删除重新开始即可

### 4.2、分支操作常用命令

| git branch 分支名          | 创建分支                     |
| -------------------------- | ---------------------------- |
| git branch -v              | 查看分支                     |
| git checkout 分支名        | 切换分支                     |
| git merge 需要合并的分支名 | 把指定的分支合并到当前分支上 |



### 4.3、分支的前提：

master主分支有提交



> 创建分支命令：`git branch 分支名`



> 切换指定分支：`git checkout 分支名`



> 创建+切换分支名：`git checkout -b 分支名`



> 删除分支:`git -d 分支名` 



### 4.4 分支的合并：

前提：一般合并的操作是为了将其他分支更新的内容，更新到master主分支上

所以先要切换到主分支上，然后在进行合并操作

**1、正常的合并**

假设master主分支和其他分支order，相差一个文件或文件夹为controller，即order多了这个文件夹

> 合并：`git merge 分支名`

**2.冲突的合并**

> 系统是无法识别细微的修改的，假设主分支和其他分支在合并的过程中，存在相同文件，但是内容不同的情况

解决：人工修改，将需要合并的地方手动合并，

> 再放到本地库，即`git add 文件名`再进行`git commit -m "操作名称"`

这样就是直接合并成功了

==警示：==

**当前分支和合并的分支都不要同时修改，多人合作时，商量好，最好是等到上一个人合并好之后，下一个人再合并进去/提取出来**







## 5、远程克隆文件至本地

前提：

1、在远端已经建立好了仓库

2、github与本地git建立了ssh连接

> 参考文章：（https://blog.csdn.net/qq_35206244/article/details/97698815）
>
> https://blog.csdn.net/qq_45796592/article/details/128953729

**命令：**

> 先去本地工作区域建立目录，一直到文件层
>
> 执行 clone 命令默认会拉取远程仓库的所有内容
>
> `git clone git@github.com:用户名/仓库名.git`
>
> 用户名和仓库从哪里来：

![3](img\3.png)

> 由于使用的是ssh，从对应github项目里面看
>
> 克隆成功
>
> ![4](D:\桌面\学习\01后端代码笔记\18 git\img\4.png)
>
> 

clone 命令是一个复合命令，相当于连续执行了下面三个命令。

> git remote add origin git@gitee.com:iam17/git-learn.git
> git fetch
> git checkout master



> pull从远程获取最新版本并merge到本地
>
> - `git pull origin 分支名称`



## 6、从本地推送到远端（这是远端配置已经弄好了的）

①建立本地仓库

②与远程建立连接的测试

> ssh -T ssh的地址
>
> ![7](img\7.png)

③init命令初始化仓库

> git init

④手动拷贝文件（如 README.md），并执行add命令

> 命令：
>
> `git add .`
>
> `git commit -m "提交注释"`

2.push推送

> 命令：`git push -u origin 分支名称`
>
> origin是什么？
>
> 这是在远端注册ssh时，生成的origin的名称。这相当于本地git连接的项目地址
>
> ![6](img\6.png)
>
> 现在github分支名称为main

![5](img\5.png)

![8](img\8.png)

### create a new repository on the command line（在本地文件夹下推送到远端）

```java
echo "# git_study" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:xiaoxiaowang1113/git_study.git
git push -u origin main
```

### push an existing repository from the command line（已经存在仓库）

```java
git remote add origin git@github.com:xiaoxiaowang1113/git_study.git
git branch -M main
git push -u origin main
```

