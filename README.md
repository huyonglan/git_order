# git_order
记录一些git命令行常用命令

  ● HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
  ● 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
  ● 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
# learn-git
一.git的一些常用命令汇总
1.git config --global user.name 
  git config --global user.email
  --global参数，表示你这台机器上所有的Git仓库都会默认使用这个配置
2.git init把某个目录变成Git可以管理的仓库
3.git add把文件添加到仓库
4.git commit -m "" 把文件提交到仓库
5.git status时刻掌握仓库（工作区）当前的状态
6.git diff 查看修改了什么内容(比较工作区和版本库内容的不同，如果修改了文件，但是没git add文件直接commit是不会把修改的文件放到版本库中的，因此diff的时候会发现不同，但是如果git add把修改的文件放到版本库中的暂存区了，那么git diff是不会发现不同的，也就是没有输出）
7.HEAD指向的版本就是的当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id(回退的话可用git reset --hard HEAD^^^^(or HEAD~4)
8.git log可以查看提交历史，以便确定要回退到哪个版本
9.要重返未来，用git reflog命令历史，以便确定要回到未来的哪个版本
10.git checkout --   file 丢弃工作区的修改
有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。

11.场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库

git checkout -- file其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以一键还原

another：
由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：
第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
$ ssh-keygen -t rsa -C "youremail@example.com"

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：
[图片]
点“Add Key”，你就应该看到已经添加的Key：
[图片]
为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。
当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

12.git remote add origin git@server-name:path/repo-name.git 关联一个远程库
例如： git remote add origin git@github.com:huyonglan/anolearngit.git

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

13.git clone  git@github.com:huyonglan/gitskills.git
(远程仓库地址） 克隆一个仓库

14.
git branch 查看分支
git branch <name> 创建分支
git checkout <name> 切换分支
git checkout -b <name> 创建并切换分支
git merge <name> 合并某分支到当前分支
git branch -d<name> 删除分支

15.git log --graph查看分支合并图
