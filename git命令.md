```git
# 设置用户的名称 （昵称）
git config --global user.name "小何"
# 设置邮箱
git config --global user.email '2480539456@qq.com'
# 查看所有全局配置
git config --list --global
#查看指定的全局配置项
git config usre.name
git config user.email



# 初始化仓库
git init



# 查看文件状态
git status
# 两条代码完全等价 其中 -s 是 --short 的简写形式：
git status -s
git status --short



# 将文件添加到暂存区
git add index.html
# 只从git仓库中移除 index.css 但保留工作区中的 index.css文件
git rm --cached index.css
# 从git仓库和工作区中同时移除index.js文件
git rm -f index.js




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
# 使用 git reset --hard 命令指定回退的版本号 即可回退到指定版本
git reset --hard 版本号



# 今后在项目开发中，会经常使用这个命令，新增和修改过后的文件加入暂存区。
git add .
# 如需要从暂存区中移除对应的文件，可以使用如下的命令
git reset HEAD 需要移除的文件名
# 给git commit 加上 -a选项，Git就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过git add 步骤
git commit -a -m '描述信息'




# 查看分支
git branch -v
#创建分支
git branch 新建分支名
# 切换分支
git checkout 分支名
# 把指定分支合并到当前分支上
git merge 分支名



# 合并冲突时，此时需要我们自己手动合并代码，手动打开这个文件
vim hello.txt  //打开hello.txt文件
按 i 进行手动合并代码
esc+:wq保存并退出
git add hello.txt  //添加暂存区
# 注意：此时使用 git commit 命令提交本地库，不能带文件名
# 如果带上文件名，它会报错：它不知道你是哪一个hello.txt
git commit -m '合并冲突解决'
# 此时就合并成功了，怎么证明成功呢？咱们这个master已经不再是master|MERGING



# 本地没有现成的 Git 仓库
git init  // 初始化仓库
git add README.md  // 暂存README.md
git commit -m "first commit"
git remote add origin https://xxx.git.xx.git 
// 将本地仓库和远程仓库进行关联，并把远程仓库命名为 origin
git push -u origin master
// 将本地仓库中的内容推送到远程的origin仓库中master分支
# 查看远程仓库别名
git remote -v




# 本地有现成的 Git 仓库
git remote add origin https://gitxxxx.git  
// 将本地仓库和远程仓库进行关联，并把远程仓库命名为origin
git push -u origin master
// 将本地仓库中的内容推送到远程库的 origin 仓库中



# 克隆远程仓库
git clone 远程仓库的地址
# 推送到云顿
git push
# 拉取代码
git pull



# 生成 SSH Key
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# ssh-keygen 生成SSH免密登录协议
# -t 指定用那种加密算法生成
# rsa 著名的非丢之类加密协议
# -C 描述 "your_email@example.com" 说明我们当前这个SSH Key（免密登录协议）是专门为这个邮箱服务的
# 检测 Github 的SSH Key是否配置成功
ssh -T git@github.com
# 基于SSH 将本地仓库上传到 Github
git push -u origin main
# -u 表示第一次吧本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u 参数
git push -u 远程仓库的别名 本地分支名称:远程分支名称
# 实际案例
$git push -u origin payment:pay
#如果希望远程分支的名称和蹦迪分支名称保持一致，可以对命令进行简化
$git push -u origin  




# 查看远程仓库分支
git remote show 远程仓库地址/别名
# 从远程仓库，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同
$git checkout 远程分支的名称
$git checkout pay
# 从远程仓库，把对应的远程分支下载到本地仓库，并把下载的本地分支重新命名
$git checkout -b 本地分支名称 远程仓库名称/远程分支名称
$git checkout -b payment origin/pay
# 将远程库origin的pay分支下载到本地，并重名为 payment




# 删除远程仓库中，指定名称的远程分支
$git push 远程仓库地址/别名 --delete 远程分支名称
$git push origin --delete pay
# 删除 origin 远程库的pay分支
```

