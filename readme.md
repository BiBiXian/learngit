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