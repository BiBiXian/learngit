# 在Windows上安装Git
  1. 在git官网中下载git安装程序 下载地址：https://git-scm.com/downloads
  2. 安装成功后可以在打开Git Bash，在命令行中设置你的开发者签名
    git config --global user.name 你的名字
    git config --global user.email 你的邮箱

# 创建本地创库
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
  