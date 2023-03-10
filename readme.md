# 在Windows上安装Git
  1. 在git官网中下载git安装程序 下载地址：https://git-scm.com/downloads
  2. 安装成功后可以在打开Git Bash，在命令行中设置你的开发者签名
    git config --global user.name 你的名字
    git config --global user.email 你的邮箱

# 创建本地仓库
  1.创建一个文件夹（例：learngit），并在命令行中使用指令访问该文件夹
    cd learngit
  2.通过git 命令把这个文件目录变成Git仓库
    git init
注意：git仓库创建完成后目录下多了一个.git的文件（隐藏文件），这个文件是Git用来跟踪管理版本库的，不要改动。

# 在本地仓库添加文件
  1. 如首先在git仓库中创建一个readme.md文件
  2. 使用git命令git add把文件添加到仓库暂存区：
    git add readme.md
    指令 git add [file1] [file2] ... 添加一个或多个文件
    指令 git add . 添加新文件和被修改文件，不包括被删除文件
    指令 git add -u 添加被修改和被删除文件，不包括新文件
    指令 git add -A 添加所有变化文件

  3. 使用git命令 git commit -m <message> 把文件提交到仓库 (message的内容是你执行的欣慰可以是中文)
    git commit -m "wrote a readme file"

# 查看仓库当前的状态 git status
  git status 可以查看那些文件发生了改变，但是如果你想查看具体修改了什么内容可以使用git diff指令
# 查看具体修改什么内容 git diff

# 删除文件
    当在工作区删除了文件，导致工作区和版本库不一致了
    1.那就用命令git rm <file> 或 （git add <file>/git add -u/ git add -A）将删除操作添加至暂存区，并且使用git commit提交到版本仓库：
    git rm a.js ：从暂存区中删除a.js该文件
    git commit -m "delete a.js"  提交至仓库

    2.另一种情况是删错了，放弃工作目录中的更改：
        git checkout -- a.js   这样在工作区删除的a.js文件就会恢复  (旧版本命令)
        git restore a.js  同样效果 (新版本命令)
注意：
git checkout -- <file>命令中的 -- 很重要，没有–，就变成了 切换到另一个分支 的命令，我们在后面的分支管理中会再次讲解git checkout命令。
在git 2.23.0 中引入了两个新的命令 switch （切换分支）和 restore（撤销修改） 用来取代checkout


# 撤销添加到暂存区操作
       git reset HEAD <file>
       git restore --staged <file>  新版本 
可以把暂存区的修改撤销掉，重新放回工作区：

# 回退版本
    git log 指令，可以查看用户在当前仓库中所有commit提交日志
    git log --pretty=oneline  让log日志一行输出
    git reset --hard HEAD^ 使用版本回退时Git必须要知道回退到那个版本，其中HEAD表示当前版本,HEAD^表示上一个版本,HEAD^^表示上上一个版本以此类推。
    git reset  --hard HEAD~10 如果要回退的版本较早，使用HEAD^的方法比较繁琐可以使用HEAD~数字方法回退  回退到当前版本前第十个版本
    git reset --hard sdff2 Git可以通过指定版本号，回退到指定版本。使用指定版本号回退版本时无需将版本号写完整，写前几位能跟其他版本号区分开就可以
    如果在开发中如果开发人员不小心回退版本多了，可以使用
    git reflog指令查看所有操作记录，并查找到想到的版本号，通过reset方法回到指定版本

# 分支管理
    git checkout -b dev
    # git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
    git branch dev
    git checkout dev

    # git 新版本使用switch 进行分支切换
    git switch dev 切换分支
    git switch -c dev 创建并切换至分支

    git branch命令查看当前分支

dev分支的工作完成，我们就可以切换回master分支：git switch  master
使用merge把dev分支的工作成果合并到master分支上： git merge dev
合并完分支后，甚至可以删除dev分支： git branch -d dev

# 解决冲突 没有新的命令

使用Github
介绍：Github是一个基于git的代码托管平台，付费用户可以建私人仓库，我们一般的免费用户只能使用公共仓库。只要注册一个GitHub账号，就可以免费获得Git远程仓库。目前GitHub已是：

一个拥有143万开发者的社区。其中不乏Linux发明者Torvalds这样的顶级黑客，以及Rails创始人DHH这样的年轻极客。
这个星球上最流行的开源托管服务。目前已托管431万git项目，不仅越来越多知名开源项目迁入GitHub，比如Ruby on Rails、jQuery、Ruby、Erlang/OTP；近三年流行的开源库往往在GitHub首发，例如：BootStrap、Node.js、CoffeScript等。
alexa全球排名414的网站。
注册账户以及创建仓库
注册：要想使用github第一步当然是注册github账号了， github官网地址。

配置：

首先在本地创建ssh key；
$ ssh-keygen -t rsa -C "your_email@youremail.com"



后面的your_email@youremail.com改为你在github上注册的邮箱，之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。
成功后可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，id_rsa是SSH Key的私钥，不能泄露出去，id_rsa.pub是SSH Key的公钥，可以放心地告诉任何人。

登陆GitHub，进入 Account Settings（账户配置），左边选择SSH Keys，Add SSH Key,title随便填，在Key文本框里粘贴id_rsa.pub文件的内容。
点“Add Key”，你就将Key添加到项目中了：
配置ssh
给GitHub账户上配置SSH Key的作用是，让GitHub识别出推送的提交是你设置SSH key设备推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有指定设备才能推送。

创建仓库：

登陆GitHub，在页面上找到“Create a new repo”按钮，创建一个新的仓库：
Inked创建项目_LI.jpg
在Repository name填入仓库名字，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：
空项目.png
在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。
我们根据GitHub的提示，在本地的learngit仓库下运行命令：
git remote add origin git@github.com:username/仓库地址.git



注意：请将上面的 github.com:username/仓库地址.git url替换成你自己的仓库地址

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的。

下一步，使用git push命令把本地库的内容推送到远程，实际上是把本地分支推送到远程分支。
git push -u origin 本地分支名:远程分支名

Counting objects: 20, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
Total 20 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:github.com:username/仓库地址.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.


从现在起，只要本地作了提交，就可以通过命令把本地master分支的最新修改推送至GitHub，
git push origin 本地分支名:远程分支名


注意：若本地分支名与远程分支名相同可以git push origin 分支名

SSH警告
当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?


这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

Warning: Permanently added 'github.com' (RSA) to the list of known hosts.



这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。

从远程库克隆
介绍：有时我们开发中先从远程仓库中将仓库克隆到本地进行开发，需要使用命令git clone从远程仓库克隆一个本地库

 git clone git@github.com:username/仓库地址.git



注意：克隆的本地仓库，开发后修改远程库，还需要使用git remote add 关联远程仓库。使用git push将本地仓库推送到远程。