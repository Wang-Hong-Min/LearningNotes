# Git&GitHub——分布式版本控制

## 1.版本控制工具应该具备的功能

- 协同修改
    - 多人并行不悖的修改服务器端的同一个文件。
- 数据备份
    - 不仅保存文件和目录的当前状态，还能保存每一次提交过的历史状态
- 版本管理
    - 在保存每一个版本的文件信息的时候要做到不保存重复的数据，以节约存储空间，提高运行效率。这方面SVN采用的是**增量式管理**的方式，而Git采用**文件系统快照**的方式。
- 权限控制
    - 对团队参与开发的人员进行权限控制
    - 对团队外开发者贡献的代码进行审核——Git独有
- 历史记录
    - 查看修改人、修改时间、修改内容、日志信息
    - 将本地文件恢复到某一个历史
- 分支管理
    - 允许开发团队在开发过程中    多条生产线同时推进任务，进一步提高效率

## 2.版本控制简介

### 2.1 版本控制

工程设计领域中适用版本控制管理工程蓝图的设计过程。在IT开发过程中也可以使用版本控制管理代码的版本迭代。

### 2.2版本控制工具

通过版本控制工具实现版本控制

集中式版本控制工具：

​	CVD、SVN、VSS……

分布式版本控制工具：

​	Git、Mercurial、Bazaar、Darcs……

## 3.Git介绍

### 3.1 Git简介

略

### 3.2 Git的优势

- 大部分操作在本地完成，不需要联网
- 完整性保证
- 尽可能添加数据，而不是删除或修改数据
- 分支操作非常快捷流畅
- 与linx命令全面兼容

### 3.3 Git 安装

安装到非中文无空格目录（任何软件安装须遵循这个原则，防止安装出错）。

具体安装过程，自行百度。

### 3.4 Git本地结构

-  三个区域
    - 工作区
    - 暂存区
    - 本地库

![1573801693732](Git_Images/1573801693732.png)

- 文件的5中状态
    - 未追踪
    - 已追踪
    - 已暂存
    - 已提交
    - 已忽略

### 3.5 Git 和代码托管中心

代码托管中心的任务：维护远程库

- 局域网环境下
    -  GitLab 服务器
- 外网环境
    - GitHub
    - 码云

### 3.6 本地库与远程库的交互方式

- 团队内部协作
- ![](Git_Images/1573802469282.png)
- 跨团队协作

![1573802684653](Git_Images/1573802684653.png)

## 4.命令行操作

### 4.1 本地库初始化

-  命令 git init

-  效果  生成.git文件，默认隐藏

    ![1573803084027](Git_Images/1573803084027.png)

-  注意  .git文件中存放着本地库相关的子目录和文件，不要删除，也不要轻易修改。

### 4.2 设置签名

- 形式

    ​	用户名： whm

    ​	邮箱：whm111@163.com

- 作用 区分不同开发人员的身份

- 辨析 设置签名与远程库的用户名、邮箱、密码没有任何关系，只用于区分身份。

- 命令

    - 项目、仓库级别  仅在当前本地库范围生效
        - git **config** user.name whm
        - git **config** user.email whm111@163.com
        - 信息保存位置  .git/config

    ![1573807753093](Git_Images/1573807753093.png)

    

    - 系统用户级别 登录当前操作系统的范围（如win10管理员账户）
        - git **config** *--global* user.name whm
        - git **config** *--global* user.email whm111@163.com
        - 信息保存位置  管理员目录下隐藏文件.gitconfig 如：C:\Users\Administrator\.gitconfig

    ![](Git_Images/1573808038211.png)

    - 级别优先级
        - 就近原则：项目级别优先于系统用户级别
        - 二者都没有是不允许的

### 4.3 具体操作命令

- git status 查看工作区、暂存区信息
    - 分支信息
    - 提交记录
    - 可提交内容 （git add 命令添加到暂存区中文件）
    
- git add .  工作区“新建/修改”的文件添加到暂存区，文件由**未追踪**状态变为**追踪**状态

- git add [file name] 工作区“新建/修改”的文件添加到暂存区，文件由**未追踪**状态变为**追踪**状态

- git rm --cached 文件名  将提交到暂存区的文件撤销，文件回到工作区，文件从**追踪**状态回到**未追踪**状态

- git commt -m ‘提交信息说明’ [file name]  暂存区文件提交到本地库，**不加文件名**，提交暂存区所有文件，**加了文件名**则只提交具体的文件。

- git commit -a 已提交过的文件做了修改，可直接使用此命令提交到本地库，跳过git add这一步

- 查看历史记录

    - git log 日志完整显示，HEAD->master 表明当前版本。

        ![1573886116986](Git_Images/1573886116986.png)

        - 多屏显示控制方式
            - 空格向下翻页
            - b向上翻页
            - q退出

    - git log --pretty=oneline

        ![1573886044450](Git_Images/1573886044450.png)

    - git log --oneine

        ![1573886278935](Git_Images/1573886278935.png)

    - git reflog   指明HEAD版本，HEAD@{num}，到某个版本需要回退num步

        ![1573886401622](Git_Images/1573886401622.png)

- 版本前进后退

    - 本质 依赖于|HEAD的指针，指向哪个版本就是哪个版本。

    ![](Git_Images/1573886865341.png)

    - 基于索引值操作[推荐]

        git reset --hard [hash值一部分]

        ![1573887067148](Git_Images/1573887067148.png)

        ![1573887143578](Git_Images/1573887143578.png)

    - 使用^符号  只能后退

        git reset --hard HEAD^      "^"有几个，版本回退几次

    - 使用~符号  只能后退

        git reset --hard HEAD~[num]      版本回退num步

    - reset命令三个参数

        - --soft

            - 仅移动本地库HEAD指针

                ![1573888266035](Git_Images/1573888266035.png)

        - --mixed

            - 移动本地库HEAD指针

            - 重置暂缓区

                ![1573888293223](Git_Images/1573888293223.png)

        - --hard

            - 移动本地库HEAD指针

            - 重置暂缓区和工作区

                
    
- 删除文件找回

    - 前提：删除前文件存在时的状态提交到了本地库，git只会增加新版本，不会删除，本地库永远存在之前版本。
    - 删除操作提交到本地库，回到上一个版本
        - git reset --hard [上一版本]
    - 删除操作未提交到本地库，重回本版本（相当于还未做删除操作）
        - git reset --hard [当前版本]

- 文件比较

    - git diff [file name]     将工作区的文件与暂存区的对应文件比较
    - git diff HEAD(本地库当前版本，或某一个版本) [file name]       将工作区的文件与本地库某一版本中对应文件比较
    - 不带文件名，可比较多个文件

## 5. 分支

### 5.1 什么是分支

Git在版本控制中的表现方式，一个分支代表一条任务线，使用多条线同时推进多个任务

![1574063966493](Git_Images/1574063966493.png)

### 5.2 分支的好处

1. 同时并行多个功能模块开发，体改开发效率
2. 各个分支任务开发过程中如果某一分支开发失败不会对其它分支有任何影响。失败分子删除重新开始即可

### 5.3 分支操作

- 创建分支

    - git branch [分支名]

- 删除分支

    - git branch -d [分支名] （不可删除当前分支）

- 恢复被删除的分支

    - git branch [分支名] [部分hash值] 

- 查看分支

    - git branch -v

- 切换分支

    - git checkout [分支名]

- 合并分支

    - 切换到被合并分支上（分支1合并到master，切换到master）
        - git checkout [分支名]（master）
    - git  merge [分支名] （分支1）

- 解决冲突

    - 合并时若产生冲突，合并失败，进去分支合并进行中的状态。

        ![1574063394518](Git_Images/1574063394518.png)

    - 冲突表现

        ![1574063457969](Git_Images/1574063457969.png)

    - 解决冲突

        - 编辑文件，删除特殊符号
        - 修改文件，根据需要选择保留某一个分支内容或同时保留两个分支内容
        - git add [修改文件名]
        - git commit -m “提交日志“
            - 不得携带具体文件名

## 6. Git基本原理

### 6.1 哈希

![1574065827941](Git_Images/1574065827941.png)

哈希是一系列加密算法，不同的hash算法虽然加密强度不同，但有一下几个共同点：

1. 不管输入数据的数据量有多大，同一个hash算法得出的结果长度固定
2. hash算法相同且输入数据相同，得出结果必然相同
3. hash算法相同，但输入数据有一丁点改变，结果必然不同
4. hash算法不可逆，无法通过结果逆推输入数据

hash算法通常用来验证文件：

![1574065784736](Git_Images/1574065784736.png)

Git 就是靠这种机制来从根本上保证数据完整性的。

### 6.2 Git保存版本的机制

#### 6.2.1 集中式版本控制工具的文件管理机制

以文件变更列表的方式存储信息。这类系统将它们保存的信息看作是一组基本文件和每个文件随时间逐步积累的差异。

![1574067428755](Git_Images/1574067428755.png)

#### 6.2.2 Git文件管理机制

Git 把数据看作小型文件系统的一组快照。每次提交更新时都会对当前的全部文件只做一个快照，并保存这个快照的索引。为了高效，如果文件没有修改Git不会重新存储该文件而是只保存一个链接指向之前存储的文件。所以Git 的工作方式称作快照流。

![1574067719574](Git_Images/1574067719574.png)

#### 6.2.3 Git 文件管理机制细节

- Git的“提交对象”

![1574067815552](Git_Images/1574067815552.png)

- 提交对象及其父对象形成的链条

![1574067929243](Git_Images/1574067929243.png)

### 6.3 Git分支管理机制

6.3.1 分支创建

![1574068225864](Git_Images/1574068225864.png)

6.3.2 分支切换

![1574068241750](Git_Images/1574068241750.png)



![1574068265315](Git_Images/1574068265315.png)



![1574068282856](Git_Images/1574068282856.png)

![1574068290925](Git_Images/1574068290925.png)

## 7.GitHub

### 7.1创建远程仓库

远程仓库名不需要与本地仓库名一致，**但**为了方便识别，一般**统一**本地仓库和远程仓库名

### 7.2为远程仓库起别名（方便后面使用）

- git remote add [远程仓库别名，一般设置为origin] [远程仓库地址，https/ssh都可]
    - 例：git remote add origin git@github.com:Wang-Hong-Min/LearningNotes.git 
- git remote -v 查看远程仓库别名
    - ![1574126237043](Git_Images/1574126237043.png)
    - fetch 用来拉取代码
    - push用来推送代码，成对。
- 移除远程仓库别名
    - git remote remove [别名]

### 7.3 向远程仓库推送本地仓库文件

git push [远程仓库地址，可用别名，如“origin”] [分支名]

示例：git push origin master

![1574126715216](Git_Images/1574126715216.png)

origin 为远程仓库别名，不用输一长串地址。

master为分支，远程库若没有，会自动创建。

### 7.4 克隆

进入克隆项目本地存放地址目录，执行：

git clone [远程仓库地址]

![1574127235079](Git_Images/1574127235079.png)

效果：

- 完整的把远程仓库下载到本地目录

- 创建origin远程仓库别名地址

    ![1574127161305](Git_Images/1574127161305.png)

- 初始化本地项目

    ![1574127140070](Git_Images/1574127140070.png)

### 7.5 团队成员邀请

### 7.6 从远端拉取代码

- pull=fetch + merge
- git fetch [远程仓库地址别名] [远程分支名]
    - 从远程仓库拉取到本地，但不与工作区文件合并
- git merge [远程仓库地址别名/远程分支名] 
    - 将拉取下来的代码与工作取文件合并
- git pull [远程仓库地址别名] [远程分支名]
    - 拉取代码并合并文件

### 7.7 解决冲突

- 要点
    - 如果不是基于GitHub最新版所做的修改不能推送，必须拉取下最新版。
    - 拉取下来如果进入冲突状态，按分支冲突解决办法解决。

### 7.8跨团队协作

![1573802684653](Git_Images/1573802684653.png)

步骤:

- 东方不败到岳不群项目地址去fork项目到自己的远程库
- 东方不败从自己的远程库clone到本地进行编码，完成后推送到自己的远程库
- 东方不败发送pull request请求
- 岳不群查看请求，确认代码，确认无误后merge到岳不群的远程仓库中。

### 7.9 SSH秘钥方式（只能一个人使用）

- 进入当前用户的家目录
    $ cd ~
- 删除.ssh 目录
    $ rm -rvf .ssh
-  运行命令生成.ssh 密钥目录
    $ ssh-keygen -t rsa -C [GitHub账号邮箱]
- 注意：这里-C  这个参数是大写的 C
- 进入.ssh 目录查看文件列表
    $ cd .ssh
    $ ls -lF
- 查看 id_rsa.pub 文件内容
    $ cat id_rsa.pub
- 复制 id_rsa.pub 文件内容，登录 GitHub，点击用户头像→Settings→SSH and GPG
    keys
    New SSH Key
- 输入复制的密钥信息
    回到 Git bash 创建远程地址别名
    git remote add origin_ssh [远程仓库地址]
    推送文件进行测试

## 8.Eclipse中Git应用

略。

## 9.Git工作流

### 9.1 概念

在项目开发过程中使用 Git 的方式

### 9.2 分类

**集中式工作流**

像 SVN 一样，集中式工作流以中央仓库作为项目所有修改的单点实体。所有
修改都提交到 Master 这个分支上。
这种方式与 SVN 的主要区别就是开发人员有本地库。Git 很多特性并没有用到。

![](Git_Images/1574167744542.png)

**GitFlow工作流**

Gitflow 工作流通过为功能开发、发布准备和维护设立了独立的分支，让发布
迭代过程更流畅。严格的分支模型也为大型项目提供了一些非常必要的结构。

![1574168042558](Git_Images/1574168042558.png)

**forking工作流**

Forking 工作流是在 GitFlow 基础上，充分利用了 Git 的 Fork 和 pull request 的
功能以达到代码审核的目的。更适合安全可靠地管理大团队的开发者，而且能接受
不信任贡献者的提交。

![](Git_Images/1574168097512.png)

### 9.3GitFlow工作流（主流）

 主干分支 master
		主要负责管理正在运行的生产环境代码。永远保持与正在运行的生产环境
完全一致。
		 开发分支 develop
		主要负责管理正在开发过程中的代码。一般情况下应该是最新的代码。
		 bug 修理分支 hotfix
		主要负责管理生产环境下出现的紧急修复的代码。 从主干分支分出，修
理完毕并测试上线后，并回主干分支。并回后，视情况可以删除该分支。
		 准生产分支（预发布分支） release
		较大的版本上线前，会从开发分支中分出准生产分支，进行最后阶段的集
成测试。该版本上线后，会合并到主干分支。生产环境运行一段阶段较稳定后
可以视情况删除。
		 功能分支 feature
为了不影响较短周期的开发工作，一般把中长期开发模块，会从开发分支
中独立出来。 开发完成后会合并到开发分支。

![1574167204559](Git_Images/1574167204559.png)

开发过程

![1574168268638](Git_Images/1574168268638.png)

## 10.搭建GitLab服务器

### 10.1官网地址

首页：https://about.gitlab.com/
		安装说明：https://about.gitlab.com/installation/

### 10.2 安装命令摘录

```linx
sudo yum install -y curl policycoreutils-python openssh-server cronie
sudo lokkit -s http -s ssh
sudo yum install postfix
sudo service postfix start
sudo chkconfig postfix on
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | sudo bash
sudo EXTERNAL_URL="http://gitlab.example.com" yum -y install gitlab-ee
```

实际问题：yum 安装 gitlab-ee(或 ce)时，需要联网下载几百 M 的安装文件，非常耗
时，所以应提前把所需 RPM 包下载并安装好。
下载地址为：
https://packages.gitlab.com/gitlab/gitlab-ce/packages/el/7/gitlab-ce-10.8.2-ce.0.el7.x86_64.rpm

### 10.3 调整后安装命令

```linx
sudo rpm -ivh /opt/gitlab-ce-10.8.2-ce.0.el7.x86_64.rpm
sudo yum install -y curl policycoreutils-python openssh-server cronie
sudo lokkit -s http -s ssh
sudo yum install postfix
sudo service postfix start
sudo chkconfig postfix on
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
sudo EXTERNAL_URL="http://gitlab.example.com" yum -y install gitlab-ce
```

**注意：**此处调整后需要与视频教程中CentOS7，gitlab-ce-10.8.2-ce.0.el7.x86_64.rpm配套

建议：创建脚本文件，将命令写入脚本文件，保存快照。再执行安装，若出错，回到快照，仔细检查。

安装完成后需要**重启**

### 10.4 GitLab服务操作

 初始化配置 gitlab
		gitlab-ctl reconfigure
		 启动 gitlab 服务
		gitlab-ctl start
		 停止 gitlab 服务
		gitlab-ctl stop

### 10.5 浏览器访问

访问 Linux 服务器 IP 地址即可，如果想访问 EXTERNAL_URL 指定的域名还需要配置
域名服务器或本地 hosts 文件。
		初次登录时需要为 gitlab 的 root 用户设置密码。

![1574214734136](Git_Images/1574214734136.png)

※应该会需要停止防火墙服务：（自己测试）
				service firewalld stop

正式使用应配置合适防火墙策略，开放相应端口，不能直接关闭防火墙

