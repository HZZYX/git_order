# GIT 快速掌握 



# 一. Git



## 1.1 Git 中的三个区域

​	使用 Git 管理的项目，拥有三个区域，分别是工作区、暂存区、Git仓库

**工作区：**

​	语义化讲就是：在Visual Studio Code编辑代码

**暂存区：**

​	已完成的工作的临时存放区域，等待被提交（ 已经 git add 文件名 ）

**Git 仓库：**

​	将写好的代码提交到本地仓库（ 已经 git commit -m '本次提交的描述' 文件名 ）

**经历过上面三个区域后，最终通过（ 已经  git push 仓库别名/远程仓库地址 提交分支 ）**



## 1.2 Git 中的5+1种状态

​	1. 未被Git管理 Untracked

​		未跟踪，不被 Git 所管理的文件

​	2. 未修改 Unmodified

​		工作区中文件的内容和Git仓库中文件的内容保持一致	

​	3. 已修改 modified

​		表示修改了文件,工作区中的文件和内容和Git仓库中文件的内容不一致，但还没将修改的结果放到暂存区

​	4. 已暂存 staged

​		表示对已修改文件的当前版本做了标记，工作区中被修改的文件已被放到暂存区，准备将修改后的文件保存到Git仓库中，使之包含在下次提交的列中 （ 已经 git add 文件名 ）

​	5. 已提交 committed

​		表示文件已经安全地保存在本地的 Git 仓库中 （ 已经 git commit -m '本次提交的描述' 文件名 ）

​	**6. 已上传至远程库**

​		**表示本地文件已经放到了远程仓库中 （ 已经 git push 仓库别名/远程仓库地址 分支名 ）**



# 二. 安装Git 



​	下载地址：https://git-scm.com/downloads 

​	傻瓜式安装：一直点next就好



## 2.1 配置用户信息

​	安装完 Git 之后，要做的第一件事就是设置自己的用户名和邮件地址。因为通过 Git 对项目进行版本管理的时候，Git 需要使用这些基本信息，**来记录是谁对项目进行了操作**

```git
# 设置用户的名称 （昵称）
git config --global user.name "小何"
# 设置邮箱
git config --global user.email '2480539456@qq.com'
```

注意：如果使用了 --global 选项，那么该命令只需要运行一次，即可永久生效。

注意：这里设置用户签名和将来登录 GitHub（或其他代码托管中心）的账号没有任何关系

**步骤：**

​	1.随便在哪里鼠标右键，找到 Git Bash Here。

​	2.输入上面的两行代码。



## 2.2 Git 的全局配置文件

​	通过git config --global user.name 和 git config --global user.email 配置的用户名和邮箱地址，会被写入到 C:Users/用户/.gitconfig 文件中。这个文件是 Git的全局配置文件。配置一次即可永久生效。



## 2.3 检查配置信息

​	除了使用记事本查看全局的配置信息之外，还可以运行如下终端命令，快速的查看 Git 的全局配置信息：

```git
# 查看所有全局配置
git config --list --global

#查看指定的全局配置项
git config usre.name
git config user.email
```



# 三. Git 基本操作



## 3.1 在现有目录中初始化仓库

​	如果自己有一个尚未进行版本控制的项目目录，想要用 Git 来控制它，需要执行如下两个步骤：

​		1.在项目目录中，通过鼠标右键打开 “Git Bash”

​		2.执行 git init 命令将当前的目录转化为 Git 仓库

```git
# 初始化仓库
git init
```

​	git init 命令会创建一个名为 .git的隐藏目录，这个 .git 目录就是当前的项目的 Git 仓库，里面包含了初始化的必要文件这些文件是 Git 仓库的必要组成部分。



## 3.2 检查文件的状态

​	可以使用 git status 命令查看文件处于什么状态

```git
git status
```

![image-20220611170732238](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220611170732238.png)

​	在状态报告中可以看到新建的index.html 文件出现在 Untracked files （未被跟踪的文件）下面。未跟踪的文件意味着 Git 在之前的快照（提交）中没有这些文件：Git不会自动将之纳入跟踪范围i，除非明确地告诉它：我需要使用 Git 跟踪管理该文件（ git add 文件名 ）

**以精简的方式显示文件状态：**

​		使用 git status 输出的状态报告很详细，但有些繁琐。如果希望以精简的方式显示文件的状态，可以使用如下：

```git
# 两条代码完全等价 其中 -s 是 --short 的简写形式：
git status -s

git status --short
```

未被跟踪文件前面有红色的 ?? 标记

![image-20220611171750462](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220611171750462.png)

```linux
linux命令

vim hello.txt 创建或者打开hello.txt文件

按i 进入插入模式，从目前光标处插入

按esc退出编辑模式返回到一般模式

:wq 保存文件并退出

yy 复制  pp粘粘

ll 查看当前目录

cat hello.txt   //查看hello.txt文件

tail -n 1 hello.txt    //查看文件末尾的第一行
```



## 3.3 将文件添加到暂存区 - git add ( 跟踪新文件 )

使用命令 git add 开始跟踪一个文件。所以，要跟踪index.html文件，运行如下的命令即可：

```
# 将文件添加到暂存区
git add index.html

# 只从git仓库中移除 index.css 但保留工作区中的 index.css文件
git rm --cached index.css

# 从git仓库和工作区中同时移除index.js文件
git rm -f index.js
```



## 3.4 提交更新 （ commit - 提交 ）

​		现在暂存区中有一个index.html文件等待被提交到 GIT仓库中进行保存，可以执行commit命令进行提交，其中-m选项后面是把本次的提交消息，用来对提交的内容做进一步的描述：

```git
git commit -m "描述信息" 文件名

# 查看引用日志信息
git reflog
包含：版本号的前7位+当前指针指向的分支+版本描述

# 查看将详细日志命令
git log
# 按时间先后顺序列出所有提交历史，最近的提交放在最上面
包含：完整版版本号+谁提交这个版本+当前指针指向的分支+版本描述

# 只会展示最新的两条提交历史，数组可以按需进行修改
git log -2
```



## 3.5 对已提交的文件进行修改

​		当我们修改了工作区中index.html的内容之后，再次运行 git status 和 git status -s 命令，会看到如下的内容：

![image-20220611174751852](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220611174751852.png)

​		文件index.html出现在 Changes not staged for commit 这行下面，说明**已跟踪文件的内容发生了本话，但还没有放到暂存区。**

​		注意：修改过的、没有放入暂存区的文件前面有红色的**M**标记

​		当文件发生修改时，需要再次运行 git add 命令，这个命令是个多功能命令，主要有如下3个功能：

 			1. 可以用它开始跟踪新文件。
 			1. 把已跟踪的、且已修改的文件放到暂存区
 			1. 把有冲突的文件标记为已解决状态



```git
# 对已提交的文件进行修改后，需要再次暂存和提交本地库
git add index.html //把已修改的文件放到暂存区
git commit -m '修改了index.html' index.html
```



## 3.6 代码回滚 （ 撤销对文件的修改 ）

​		撤销操作的本质：用 Git 仓库中保存的文件，覆盖工作区中指定的文件。

​		撤销对文件的修改指的是：把工作区中对应文件的修改，还原成Git仓库中所保存的版本。

​		操作的结果：所有的修改会丢失，且去无法恢复！危险性比较高，请慎重操作！

```git
# 一般不用

# git checkout -- 要回滚的文件名 （注意空格！！！） 
git checkout -- index.html
```

![image-20220611181337966](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220611181337966.png)



# 四. Git 基本操作



## 4.1 向暂存区中一次性添加多个文件

​		如果需要被暂存的文件个数比较多，可以使用如下命令，一次性将所有的新增和修改过的文件加入暂存区：

```git
git add .

# 今后在项目开发中，会经常使用这个命令，新增和修改过后的文件加入暂存区。

# 如需要从暂存区中移除对应的文件，可以使用如下的命令
git reset HEAD 需要移除的文件名
```

![image-20220611182148355](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220611182148355.png)



## 4.2 跳过使用暂存区域

​			Git提供了一个跳过使用暂存区域的方法，只要在·提交的时候，给git commit 加上 -a选项，Git 就会自动把***所有已经跟踪过的文件***暂存起来一并提交，从而跳过git add 步骤

```git
git commit -a -m '描述信息'
```



## 4.3 忽略文件 （会认就行 - 基本上一个项目只会配置非常少的忽略设置）

1. 以#开头的是注释
2. 以/结尾的是目录
3. 以/开头防止递归
4. 以！开头表示取反
5. 可以使用glob模式进行文件和文件夹的匹配（glob指简化了的正则表达式）



## 4.4 glob模式

​		所谓的glob模式是指简化了的正则表达式：

  		1. 星号 * 匹配零个或多个任意字符
  		2. [abc] 匹配任何一个列在方括号中的字符 （ 此案例匹配一个a或匹配一个b或匹配一个c ）
  		3. 问好 ? 只匹配一个任意字符
  		4. 在方括号中使用短划线分割两个字符，表示所有在这个两个字符范围内的都可以匹配（ 比如：[0-9] )
  		5. 所有0到9的数字
  		6. 两个星号 ** 表示匹配任意中间目录 （ 比如：a/**/z 可以匹配 a/z、a/b/z或a/b/c/z等 ）

```git
# 忽略 index.css 这个文件
index.css

# 忽略所有 .html 文件
*.html

# 除所有的lib.html，及时在前面忽略过 .html文件
!lib.html

# 只忽略当前目录下的 TODO 文件，而不会忽略subdir/TODO
/TODO

# 忽略任何目录下名为build的文件夹
build/

# 忽略doc/ 目录以及其所有子目录下的.pdf文件
doc/**/*.pdf


```

 

## 4.5 回退到指定的版本

```git
# 使用 git reset --hard 命令指定回退的版本号 即可回退到指定版本
git reset --hard 版本号
```



## 4.6  分支查看、创建、切换、合并

```
# 查看分支
git branch -v

#创建分支
git branch 新建分支名

# 切换分支
git checkout 分支名

# 把指定分支合并到当前分支上
git merge 分支名
```



## 4.7 合并分支冲突

​		合并分支时，两个分支同一个文件的同一个位置有两套或多套完全不同的修改，Git无法替我们决定使用哪一个，必须人为决定新代码的内容

​		当我们使用 git merge 分支名，将指定分支合并到当前分支上，出现合并分支冲入时，Git会报如下错误：

意思是：说你这个自动合并失败，它不敢帮咱们自动合并，因为你这一块有一个代码合并冲突，在这个hello.txt里边

<img src="file:///C:\Users\24805\Documents\Tencent Files\2480539456\Image\C2C\1554BB34806028430855D1F09E9F75F3.png" alt="img" style="zoom: 50%;" />

```git
# 此时需要我们自己手动合并代码，手动打开这个文件

vim hello.txt  //打开hello.txt文件

按 i 进行手动合并代码
esc+:wq保存并退出

git add hello.txt  //添加暂存区

# 注意：此时使用 git commit 命令提交本地库，不能带文件名
# 如果带上文件名，它会报错：它不知道你是哪一个hello.txt
git commit -m '合并冲突解决'

# 此时就合并成功了，怎么证明成功呢？咱们这个master已经不再是master|MERGING

```



# 五. 开源项目托管平台

​		专门用于免费存放开源项目源代码的网站，叫做开源项目托管平台。目前世界上比较出名的开源项目平台。

主要有一下3个：

1. Github （ 全球最牛的开源项目托管平台，没有之一 ） 自己用
2. Gitlab （ 对代码私有性支持较好，因此企业用户较多 ）  上班用
3. Gitee （又叫做码云，是国产的开源项目托管平台。访问速度快、纯中文界面、使用友好 ）不用

## 5.1 远程仓库的两种访问方式

​	Github上的远程仓库，有两种访问方式，分别是HTTPS和SSH。它们的区别是：

  1. HTTPS：零配置；但是每次访问仓库时，需要重复输入 Github的账号和密码才能访问成功；

  2. SSH：需要进行额外的配置；但是配置成功后，每次访问仓库时，不需要重复输入Github的账号和密码

     注意：在实际开发中，推荐使用SSH的方式访问远程库。

     ```git
     # 本地没有现成的 Git 仓库
     
     git init  // 初始化仓库
     git add README.md  // 暂存README.md
     git commit -m "first commit"
     git remote add origin https://xxx.git.xx.git 
     // 将本地仓库和远程仓库进行关联，并把远程仓库命名为 origin
     git push -u origin master
     // 将本地仓库中的内容推送到远程的origin仓库中master分支
     
     
     
     # 本地有现成的 Git 仓库
     git remote add origin https://gitxxxx.git  
     // 将本地仓库和远程仓库进行关联，并把远程仓库命名为origin
     git push -u origin master
     // 将本地仓库中的内容推送到远程库的 origin 仓库中
     
     # 克隆远程仓库
     git clone 远程仓库的地址
     ```
     
     
     
     ## 5.2 Git 的push操作 （ 推送 - 也就是更新远程仓库 ）

```
# 1. 添加暂存区
git add .

# 2. 提交更新
git commit -m "2 commit"

# 3. 推送到云顿
git push
```



## 5.3 SSH Key

1. SSH Key 的作用：实现本地仓库和 Github 之间免登录的加密数据传输。
2. SSH Key 的好处：免登录身份认知、数据加密传输。
3. SSH Key 由两部分组成，分别是：
   			1. id rsa （ 私钥文件，存放于客户端的电脑中即可 ）
      			1. id rsa.pub （ 公钥文件，需要配置到 Github 中 ）



## 5.6 生成 SSH Key

1. 打开 Git Bash

2. 粘粘如下命令，并将 your_email@example.com 替换为注册 Github账号时填写的邮箱：

   ```git
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   
   # ssh-keygen 生成SSH免密登录协议
   # -t 指定用那种加密算法生成
   # rsa 著名的非丢之类加密协议
   # -C 描述 "your_email@example.com" 说明我们当前这个SSH Key（免密登录协议）是专门为这个邮箱服务的
   ```

3.  连续敲击3次回车，即可在 c:\users\用户文件夹\.ssh 目录中生成 id_rsa 和 id_rsa.pub 两个文件

![image-20220612091928640](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220612091928640.png)



## 5.7 配置SSH Key

1. 使用记事本打开 id_rsa.pub 文件，复制里面的文本内容

2. 在浏览器中登录 Github，点击头像 ->Settings->SSH and GPG Keys -> New SSH Key

   ![image-20220612094031976](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220612094031976.png)

3. 将 id_rsa.pub 文件中的内容，粘粘到key对应的文本框中

4. 在Title 文本框中任意填写一个名称，来标识这个 Key 从何而来

   ![image-20220612094213006](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220612094213006.png)



### 5.71 检测 Github 的SSH Key是否配置成功

1. 打开 Git Bash，输入如下的命令并回车执行

   ```git
   ssh -T git@github.com
   ```

2. 上述的命令执行成功之后，可能会看到如下的提示消息：

   ![image-20220612094545119](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220612094545119.png)

3. 输入yes之后，如果能看到类似于下面的提示消息，证明 SSH Key已经配置成功了：

   ![image-20220612094632359](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220612094632359.png)

```git
# 基于SSH 将本地仓库上传到 Github
git push -u origin main

# -u 表示第一次吧本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u 参数
git push -u 远程仓库的别名 本地分支名称:远程分支名称

# 实际案例
$git push -u origin payment:pay

#如果希望远程分支的名称和蹦迪分支名称保持一致，可以对命令进行简化
$git push -u origin payment
```



## 5.8 查看远程仓库分支

```git
git remote show 远程仓库名称
```

![image-20220612100003471](C:\Users\24805\AppData\Roaming\Typora\typora-user-images\image-20220612100003471.png)

## 5.9 跟踪分支

跟踪分支指的是：从远程仓库中，把远程分支下载到本地仓库中。需要运行的命令如下：

```
# 从远程仓库，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同
$git checkout 远程分支的名称
$git checkout pay

# 从远程仓库，把对应的远程分支下载到本地仓库，并把下载的本地分支重新命名
$git checkout -b 本地分支名称 远程仓库名称/远程分支名称
$git checkout -b payment origin/pay
# 将远程库origin的pay分支下载到本地，并重名为 payment
```

![image-20220518222046819](D:\项目\git\day02\images\image-20220518222046819.png)

##  5.10 拉取(pull)远程分支的最新的代码(★★★)

可以使用如下的命令，把远程分支最新的代码下载到本地对应的分支中：

```
git pull
```

![image-20220518222229265](D:\项目\git\day02\images\image-20220518222229265.png)

**龟龟怎么做呢？**

步骤：

1. 右键`tortoisegit` => 拉取

   ![image-20220518222319308](D:\项目\git\day02\images\image-20220518222319308.png)

## 5.11 删除远程分支

```git
# 删除远程仓库中，指定名称的远程分支
$git push 远程仓库名称 --delete 远程分支名称
$git push origin --delete pay
# 删除 origin 远程库的pay分支
```

![image-20220518223030712](D:\项目\git\day02\images\image-20220518223030712.png)





