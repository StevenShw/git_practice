# git_practice

只是个用于教学的仓库罢了

# 1. 配置

git config --global user.name“yourname”

git config --global user.email“email@email.com”

git config --global --list

# 2. 初始化

git init

# 3. 创建本地分支 `<main>`

git add .                        // 添加现有文件

git commit -m "your comment"     // 提交文件，这个会自动创建master分支

git branch #列出分支

git branch test   //创建名为 test的分支

git branch -m main new_branch //修改名, 将"main"分支名改为“new_branch”

git branch -d testing #删除testing分支

git checkout testing #创建并切换到testing分支

git commit -m "chapter2" //

只为最新一次提交进行注释, 出现注释界面时按 i 进入修改模式；

//在第一行写注释，按ESC退出编辑模式，输出 :wq 保存注释并退出

git commit -am //--amend  可以不用单独git add

git status //查看自己写了哪些东西

# 4. 添加远程版本库

git remote add origin git@github.com:xxx.git

git remote -v                    // 查看远程分支

git fetch origin master:temp     // 从远程获取master到本地temp分支

git diff temp                    // 比较本地仓库与下载的temp分支

git merge temp                   // 合并temp分支到本地的master分支

git merge temp --allow-unrelated-histories //如果git merge合并的时候出现 //refusing to merge unrelated histories的错误，原因是两个仓库不同

git branch -d temp               // 删除分支

git pull origin <远程分支名>:<本地某个分支，比如刚建的main>   // 相当于fetch和merge

**如果遇到 error: The branch 'temp' is not fully merged.**

git merge temp  // 与当前分支合并， 先将“temp”分支上的最新提交合并到本地之后再删除 git branch -d temp

git rebase temp   // 会将temp分支上的所有历史修改也添加进来，这样方便回溯

git cherry-pick -x 48866f  //与merge不同，这个可以选择对应哈希值的commit合并到当前分支, 之后如果temp分支上的其余commit都无用，可以强制删除 git branch -D temp

# 5. 提交到 Github备份

git push <远程主机名> <本地分支名>:<远程分支名> # 例如 git push origin main:master

git push <远程主机名> <本地分支名> #将本地分支提交到远程仓库，如果远程没有该分支则创建

git push <远程主机名> :<远程分支名> #将本地空分支提交到远程仓库，即删除该远程仓库

git push -u origin <本地分支名> # 将本地分支与远程同名分支相关联

# 6. 仓库的删除

git remote rm name  # 删除远程仓库

git remote rename old_name new_name  # 仓库名可以进行重新命名

# 7. ssh-key问题

***遇到报错Please make sure you have the correct access rights and the repository exists.***

git config --global --list #先查看账户设置，没有设置的话新设置账户

git config --global user.name "yourname"  # Jasmineyangyangyang

git config --global user.email“your@email.com"  # 1021802264@qq.com

//删除.ssh文件夹（/Users/your_user_directory/.ssh）下的known_hosts(手动删除即可，不需要git）

ssh-keygen -t rsa -C "your@email.com"  #（请填你设置的邮箱地址） //在终端输入

//接着出现：

Generating public/private rsa key pair.

Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):

请直接按下回车

然后系统会自动在.ssh文件夹下生成两个文件，id_rsa和id_rsa.pub，用记事本打开id_rsa.pub复制全部内容

// 打开https://github.com/，登陆你的账户，进入设置, ->SSH and GPG keys->New SSH key [复制进去]->add SSH key

**检查：回到本地，在git中输入命令**

ssh -T git@github.com  #然后跳出一堆话，输入yes
