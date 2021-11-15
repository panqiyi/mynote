## Git分布式版本控制工具

## 1. Git概述

### 1.1 Git历史

Git 诞生于一个极富纷争大举创新的年代。Linux 内核开源项目有着为数众多的参与者。 绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上（1991－2002年间）。 到 2002 年，整个项目组开始启用一个专有的分布式版本控制系统 BitKeeper 来管理和维护代码。

到了 2005 年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。 这就迫使 Linux 开源社区（特别是 Linux 的缔造者 Linus Torvalds）基于使用 BitKeeper 时的经验教训，开发出自己的版本系统。 

他们对新的系统制订了若干目标：

速度

 简单的设计

 对非线性开发模式的强力支持（允许成千上万个并行开发的分支）

 完全分布式

 有能力高效管理类似 Linux 内核一样的超大规模项目（速度和数据量）

### 1.2 Git与SVN对比

SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而开发人员工作的时候，用的都是自己的电脑，所以首先要从中央服务器下载最新的版本，然后开发，开发完后，需要把自己开发的代码提交到中央服务器。

集中式版本控制工具缺点：

  服务器单点故障

  容错性差

![1559580034272](img/图片1.png)

Git是分布式版本控制系统（Distributed Version Control System，简称 DVCS） ，分为两种类型的仓库：

本地仓库和远程仓库

本地仓库：是在开发人员自己电脑上的Git仓库		

远程仓库：是在远程服务器上的Git仓库

Clone：克隆，就是将远程仓库复制到本地

Push：推送，就是将本地仓库代码上传到远程仓库

Pull：拉取，就是将远程仓库代码下载到本地仓库

![1559580115132](img/图片2.png)

### 1.3 Git工作流程

工作流程如下：

1．从远程仓库中克隆代码到本地仓库

2．从本地仓库中checkout代码然后进行代码修改

3．在提交前先将代码提交到暂存区

4．提交到本地仓库。本地仓库中保存修改的各个历史版本

5．修改完成后，需要和团队成员共享代码时，将代码push到远程仓库

![1559580145716](img/图片3.png)

### 1.4 Git下载与安装

下载地址： <https://git-scm.com/download>

![1559580189784](img/图片4.png)

下载完成后可以得到如下安装文件：

![1559580208972](img/图片5.png)

## 2. Git代码托管服务

### 2.1 常用的Git代码托管服务

前面我们已经知道了Git中存在两种类型的仓库，即本地仓库和远程仓库。那么我们如何搭建Git远程仓库呢？我们可以借助互联网上提供的一些代码托管服务来实现，其中比较常用的有GitHub、码云、GitLab等。

gitHub（ 地址：https://github.com/ ）是一个面向开源及私有软件项目的托管平台，因为只支持Git 作为唯一的版本库格式进行托管，故名gitHub

码云（地址： https://gitee.com/ ）是国内的一个代码托管平台，由于服务器在国内，所以相比于GitHub，码云速度会更快

GitLab （地址： https://about.gitlab.com/ ）是一个用于仓库管理系统的开源项目，使用Git作为代码管理工具，并在此基础上搭建起来的web服务

### 2.2 在码云注册账号

要想使用码云的相关服务，需要注册账号（地址： https://gitee.com/signup ）

![1559580306570](img/图片6.png)

### 2.3 登录码云并创建Git远程仓库

注册完成后就可以使用刚刚注册的邮箱进行登录（地址： https://gitee.com/login ）

![1559580325617](img/图片7.png)

登录成功后就可以创建Git远程仓库

![1559580374460](img/图片8.png)

![1559580393455](img/图片9.png)

创建完成后可以查看仓库信息

![1559580419103](img/图片10.png)

每个Git远程仓库都会对应一个网络地址，可以点击克隆/下载按钮弹出窗口并点击复制按钮获得这个网络地址

![1559580453747](img/图片11.png)

我们当前创建的Git远程仓库对应的地址为：https://gitee.com/ChuanZhiBoKe/myGitRepo.git

### 2.4 邀请其他用户成为仓库成员

前面已经在码云上创建了自己的远程仓库，目前仓库成员只有自己一个人（身份为管理员）。在企业实际开发中，一个项目往往是由多个人共同开发完成的，为了使多个参与者都有权限操作远程仓库，就需要邀请其他项目参与者成为当前仓库的成员。

![1559580505858](img/图片12.png)

## 3. Git常用命令

### 3.1 环境配置

当安装Git后首先要做的事情是设置用户名称和email地址。这是非常重要的，因为每次Git提交都会使用该用户信息

设置用户信息 

   git config --global user.name “itcast”

   git config --global user.email “hello@itcast.cn”

查看配置信息

   git config --list

   git config user.name

通过上面的命令设置的信息会保存在~/.gitconfig文件中

### 3.2 获取Git仓库

要使用Git对我们的代码进行版本控制，首先需要获得Git仓库

获取Git仓库通常有两种方式：

  在本地初始化一个Git仓库

  从远程仓库克隆

#### 3.2.1在本地初始化一个Git仓库

执行步骤如下：

1. 在电脑的任意位置创建一个空目录（例如repo1）作为我们的本地Git仓库

2. 进入这个目录中，点击右键打开Git bash窗口

3. 执行命令git init

如果在当前目录中看到.git文件夹（此文件夹为隐藏文件夹）则说明Git仓库创建成功

![1559580617566](img/图片13.png)

#### 3.2.2从远程仓库克隆

可以通过Git提供的命令从远程仓库进行克隆，将远程仓库克隆到本地

命令形式为：git clone 远程Git仓库地址 

![1559580646080](img/图片14.png)

### 3.3工作目录、暂存区以及版本库概念

为了更好的学习Git，我们需要了解Git相关的一些概念，这些概念在后面的学习中会经常提到

版本库：前面看到的.git隐藏文件夹就是版本库，版本库中存储了很多配置信息、日志信息和文件版本信息等

工作目录（工作区）：包含.git文件夹的目录就是工作目录，主要用于存放开发的代码

暂存区：.git文件夹中有很多文件，其中有一个index文件就是暂存区，也可以叫做stage。暂存区是一个临时保存修改文件的地方

![1559580676137](img/图片15.png)

### 3.4 Git工作目录下文件的两种状态

Git工作目录下的文件存在两种状态：

  untracked 未跟踪（未被纳入版本控制）

  tracked 已跟踪（被纳入版本控制）

​        Unmodified 未修改状态

​        Modified 已修改状态

​        Staged 已暂存状态

这些文件的状态会随着我们执行Git的命令发生变化

### 3.5 本地仓库操作

git status 查看文件状态

![1559614899701](img/图片16.png)

也可以使用git status –s 使输出信息更加简洁

​                                           ![1559614973026](img/图片17.png)

git add 将未跟踪的文件加入暂存区

![1559615003252](img/图片18.png)

将新创建的文件加入暂存区后查看文件状态

![1559615033227](img/图片19.png)

git reset 将暂存区的文件取消暂存

![1559615050490](img/图片20.png)

将文件取消暂存后查看文件状态

​	![1559615064841](img/图片21.png)

git commit 将暂存区的文件修改提交到本地仓库

![1559615080939](img/图片22.png)

git rm 删除文件

![1559615094669](img/图片23.png)

删除文件后查看文件状态

                                                ![1559615111361](img/图片24.png)

上面删除的只是工作区的文件，需要提交到本地仓库

![1559615137062](img/图片25.png)

#### 将文件添加至忽略列表

一般我们总会有些文件无需纳入Git 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以在工作目录中创建一个名为 .gitignore 的文件（文件名称固定），列出要忽略的文件模式。下面是一个示例：（Windows下无法创建名称为 .gitignore 的文件，用Linux命令：touch .gitignore来创建）

```
# no .a files
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO ：只忽略当前目录下的TODO文件，而不是子目录/TODO
/TODO
# ignore all files in the build/ directory ：忽略build/目录中的所有文件
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```

git log 查看日志记录

​                                 ![1559615190571](img/图片26.png)

### 3.6 远程仓库操作

前面执行的命令操作都是针对的本地仓库，本章节我们会学习关于远程仓库的一些操作，具体包括：

####   3.6.1查看远程仓库

如果想查看已经配置的远程仓库服务器，可以运行 git remote 命令。 它会列出指定的每一个远程服务器的简写。 如果已经克隆了远程仓库，那么至少应该能看到 origin ，这是 Git 克隆的仓库服务器的默认名字

![1559617010082](img/图片27.png)

####   3.6.2 添加远程仓库

运行 git remote add <shortname> <url> 添加一个新的远程 Git 仓库，同时指定一个可以引用的简写

​                              ![1559617027057](img/图片28.png)

####   3.6.3 从远程仓库克隆

如果你想获得一份已经存在了的 Git 仓库的拷贝，这时就要用到 git clone 命令。 Git 克隆的是该 Git 仓库服务器上的几乎所有数据（包括日志信息、历史记录等），而不仅仅是复制工作所需要的文件。 当你执行 git clone 命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来。

克隆仓库的命令格式是 git clone [url] 

![1559617051229](img/图片29.png)

####   3.6.4 移除无效的远程仓库

如果因为一些原因想要移除一个远程仓库 ，可以使用 git remote rm

![1559617071094](img/图片30.png)

注意：此命令只是从本地移除远程仓库的记录，并不会真正影响到远程仓库

####   3.6.5 从远程仓库中抓取与拉取 

git fetch 是从远程仓库获取最新版本到本地仓库，不会自动merge

![1559617112262](img/图片31.png)

git pull 是从远程仓库获取最新版本并merge到本地仓库

![1559617127844](img/32.png)

注意：如果当前本地仓库不是从远程仓库克隆，而是本地创建的仓库，并且仓库中存在文件，此时再从远程仓库拉取文件的时候会报错（fatal: refusing to merge unrelated histories ），解决此问题可以在git pull命令后加入参数--allow-unrelated-histories

####   3.6.6 推送到远程仓库 

当你想分享你的代码时，可以将其推送到远程仓库。 命令形式：git git push [remote-name][branch-name]

![1559617154309](../../../AppData/Roaming/Typora/typora-user-images/1559617154309.png)

### 3.7 Git分支

几乎所有的版本控制系统都以某种形式支持分支。 使用分支意味着你可以把你的工作从开发主线上分离开来，以免影响开发主线。Git 的master分支并不是一个特殊分支。 它跟其它分支没有区别。 之所以几乎每一个仓库都有 master 分支，是因为git init 命令默认创建它，并且大多数人都懒得去改动它。

在本章节我们会学习到关于分支的相关命令，具体如下：

#### 3.7.1 查看分支 

\# 列出所有本地分支

$ git branch

\# 列出所有远程分支

$ git branch -r

\# 列出所有本地分支和远程分支

$ git branch -a

![1559617419855](img/图片33.png)

#### 3.7.2 创建分支

![1559617439442](img/图片34.png)

#### 3.7.3 切换分支 

![1559617458282](img/图片35.png)

​	

#### 3.7.4 推送至远程仓库分支 

![1559617505369](img/图片36.png)

#### 3.7.5 合并分支 

![1559617538380](img/图片37.png)

有时候合并操作不会如此顺利。 如果你在两个不同的分支中，对同一个文件的同一个部分进行了不同的修改，Git 就没办法合并它们，同时会提示文件冲突。此时需要我们打开冲突的文件并修复冲突内容，最后执行git add命令来标识冲突已解决

![1559617557838](img/图片38.png)

#### 3.7.5 删除分支

![1559617599269](img/图片39.png)

如果要删除的分支中进行了一些开发动作，此时执行上面的删除命令并不会删除分支，如果坚持要删除此分支，可以将命令中的-d参数改为-D

![1559617620953](img/图片40.png)

注：如果要删除远程仓库中的分支，可以使用命令git push
origin –d branchName

### 3.8 Git标签

像其他版本控制系统（VCS）一样，Git 可以给历史中的某一个提交打上标签，以示重要。 比较有代表性的是人们会使用这个功能来标记发布结点（v1.0 、v1.2等）。标签指的是某个分支某个特定时间点的状态。通过标签，可以很方便的切换到标记时的状态。

#### 列出已有的标签

```
git tag
查看tag信息：
git show [tagName]
```

#### 创建新标签

```
git tag [tagName]
```

![image-20210808173118942](https://gitee.com/panqiyi/pqimg/raw/master/20210808173119.png)

#### 将标签推送至远程仓库

```
git push [remote] [tag]
```

![image-20210808173149310](https://gitee.com/panqiyi/pqimg/raw/master/20210808173149.png)

![image-20210808173209642](https://gitee.com/panqiyi/pqimg/raw/master/20210808173209.png)

#### 检出标签

新建一个标签，内容为对应指定的tag（版本），然后可在此基础上继续开发。

```
git checkout -b 新标签名 tag版本
```

![image-20210808175115304](https://gitee.com/panqiyi/pqimg/raw/master/20210808175115.png)

####  删除标签

删除本地标签

```
git tag -d 标签名
```

![image-20210808180605079](https://gitee.com/panqiyi/pqimg/raw/master/20210808180605.png)

删除远程标签

```
git push origin :refs/tags/标签名
```

![image-20210808180626869](https://gitee.com/panqiyi/pqimg/raw/master/20210808180626.png)

![image-20210808180641314](https://gitee.com/panqiyi/pqimg/raw/master/20210808180641.png)

### 3.9 TortoiseGit 可视工具

看ppt。里面有

#### 修改对应的git账号密码

账号密码变化之后，再使用TortoiseGit操作git就会提示没有权限，如push等操作就不行了。

```
1、控制面板-->搜索 凭据管理器
2、点击 “Windows凭据”
3、点击选择 普通凭据中的要修改密码的git地址
4、选择 编辑保存即可
```



## 4. 在IDEA中使用Git 

### 4.1 在IDEA中配置Git 

安装好IntelliJ IDEA后，如果Git安装在默认路径下，那么idea会自动找到git的位置，如果更改了Git的安装位置则需要手动配置下Git的路径。

选择File→Settings打开设置窗口，找到Version Control下的git选项：

![1559619887418](img/图片41.png)

选择git的安装目录后可以点击“Test”按钮测试是否正确配置

​                       ![1559619915169](img/图片42.png)

### 4.2 在IDEA中使用Git

#### 4.2.1在IDEA中创建工程并将工程添加至Git 

![1559619986255](../../../AppData/Roaming/Typora/typora-user-images/1559619986255.png)

![1559620003251](img/图片44.png)

​                                  将项目添加至Git管理后，可以从IDEA的工具栏上看到Git操作的按钮

#### 4.2.2 将文件添加到暂存区

![1559620213702](img/图片45.png)

#### 4.2.3 提交文件 

![1559620242587](img/图片46.png)

#### 4.2.4 将代码推送到远程仓库 

![1559620258317](img/图片47.png)

#### 4.2.5 从远程仓库克隆工程到本地

![1559620271237](img/图片48.png)

#### 4.2.6 从远程拉取代码

![1559620286937](img/图片49.png)

#### 4.2.7 版本对比

![1559620300302](img/图片50.png)

#### 4.2.8 创建分支 

![1559620312520](img/图片51.png)

#### 4.2.9 切换分支

![1559620325257](img/图片52.png)

#### 4.2.10 分支合并

![1559620338050](img/图片53.png)

### github(现只能用令牌登录)

github（Git）使用 9个步骤：

```
1.创建项目，初始化项目，并设置项目账号
	①创建项目  D:\workspaceidea\java201021BJ\github1021
	②初始化本地库  git init  (在项目当前目录下，执行命令)
		生成.git文件夹，它就是本地库。注意，隐含文件夹。
	②设置项目账号，如果不设置采用全局账号
		全局账号：~/.gitconfig
		局部账号：.git/config
			git config user.name "zhangsanatguigu"
			git config user.email "dev111_atguigu@163.com"
		全局和局部同时存在，局部生效。没有配置局部，全局生效。
		
2.开发代码，并且进行提交操作
	git add .
	git commit -m "xxx"
		
3.注册号github账号，并在github上创建远程库

	创建远程库会生成两个url，客户端可以通过这两个url远程访问远程库
	https://github.com/zhangsanatguigu/github1021.git
	git@github.com:zhangsanatguigu/github1021.git
	
4.映射远程库地址，给url定义别名，简化操作，push本地库代码到远程库上
	git remote add origin https://github.com/zhangsanatguigu/github1021.git
	git push origin master
		需要输入github账号和密码
--------------------------------------------------------------------------------
5.克隆别人仓库
	git clone https://github.com/zhangsanatguigu/github1021.git github1021
	
	指定克隆仓库路径 以及 克隆到本地项目自定义名称。
	可以克隆提交者配置的url映射。但是不能克隆提交者的账号(.git/config)。

6.配置账号，不用再初始化仓库了，clone就初始化好了这个仓库
	
			局部账号：.git/config
			git config user.name "lisiatguigu"
			git config user.email "dev222_atguigu@163.com"

7.修改代码并提交
	git add 
	git commit -m ""

8.push代码到远程库，需要建立合作伙伴关系，否则，不允许push
	①演示不是合作伙伴关系会怎样，提交时需要输入丽思的账号和密码。但是库拥有者是张三，所以无权访问。

		$ git push origin master
		remote: Permission to zhangsanatguigu/github1021.git denied to lisiatguigu.
		fatal: unable to access 'https://github.com/zhangsanatguigu/github1021.git/': The requested URL returned error: 403
	①演示建立合作伙伴关系（张三向丽思发起合作伙伴邀请，丽思需要登录邮箱以及github网站，打开邮箱邀请函，并同意）
		$ git push origin master
		Enumerating objects: 5, done.
		Counting objects: 100% (5/5), done.
		Delta compression using up to 12 threads
		Compressing objects: 100% (2/2), done.
		Writing objects: 100% (3/3), 312 bytes | 156.00 KiB/s, done.
		Total 3 (delta 0), reused 0 (delta 0)
		To https://github.com/zhangsanatguigu/github1021.git
		   cc28276..d240bb8  master -> master

9.张三需要更新丽思远程库代码到本地库
	git pull origin master
```

github新建仓库时：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926194526.png" alt="image-20210926194526134" style="zoom:80%;" />

**注意：github从2021.08.13开始就不支持账号密码方式提交代码，可以使用令牌（access Token）验证**

##### 新增令牌步骤：

1、

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926195121.png" alt="image-20210926195121523" style="zoom:67%;" />

2、

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20210926195218598.png" alt="image-20210926195218598" style="zoom:67%;" />

3、**点击Personal access tokens(个人访问令牌)，**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926195352.png" alt="image-20210926195352404" style="zoom:67%;" />

4、令牌名称

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926195746.png" alt="image-20210926195746198" style="zoom:67%;" />

5、令牌有效期与权限设置

```
    Select scopes
选择要授予此令牌token的范围或权限。
要使用token从命令行访问仓库，请选择repo。
要使用token从命令行删除仓库，请选择delete_repo。
其他根据需要进行勾选。
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926195952.png" alt="image-20210926195952302" style="zoom:67%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926200036.png" alt="image-20210926200035844" style="zoom:67%;" />

复制令牌收藏好，因为刷新页面后就没有了

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20210926200216905.png" alt="image-20210926200216905" style="zoom:67%;" />

6、

```
# 移除原来的远程链接
git remote remove origin
# 查看git的远程链接
git remote -v
# 重新新增git远程链接
git remote add origin https://你的令牌@github.com/用户名/仓库名.git
如：https://ghp_yF2cLt1MK2YEmQxQGB@github.com/panqiyi/githubTest.git
```

登录时：密码用令牌，有时候网络问题不成功。

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926201631.png" alt="image-20210926201631507" style="zoom:67%;" />

idea用令牌登录

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926205058.png" alt="image-20210926205057646" style="zoom:67%;" />

##### github邀请开发者

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926222907.png" alt="image-20210926222907791" style="zoom: 67%;" />

给对方邮箱发送邀请函，对方点击邀请函同意(前提登录了github)即可参与开发你的仓库

##### Fork

将仓库复制一份给另一个人 (不属于你的团队) 开发

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926225804.png" alt="image-20210926225804270" style="zoom:67%;" />

步骤：

`1、让对方在github中搜索你的 '用户名/仓库' 如：panqiyi/ssmnp`

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926230253.png" alt="image-20210926230253857" style="zoom:67%;" />

`2、点击右上角Fork`

![image-20210926230357184](https://gitee.com/panqiyi/pqimg/raw/master/20210926230357.png)

`3、复制仓库地址，可以将仓库克隆到你的本地进行开发`

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210926230541.png" alt="image-20210926230541108" style="zoom:67%;" />

**看尚硅谷git课件。**