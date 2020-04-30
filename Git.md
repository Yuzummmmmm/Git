Git
===========
![image](https://note.youdao.com/yws/public/resource/7728b88bc0d40f32152896cd50f134e9/xmlnote/WEBRESOURCE4dc29009d6f92ba80307501f6f94e75d/754)


    工作区 → git add → 版本库（暂存区）→ git commit → 版本库
Git基础命令
-----------
把当前目录设为Git仓库↓

    git init
***
把文件添加到暂存区↓ 

    git add <文件名> //后面可加多个文件
    git add readme.txt
***
撤销对文件的修改↓
>*restore：恢复*

    git restore <文件名> //撤销对工作区文件的修改
    git restore --staged <文件名> //取消暂存区的修改


***
把文件从暂存区提交到版本库↓  
>*commit：（公开地）表示意见*  
>commit提交的是add提交到暂存区的文件，而不是工作区的文件

    git commit -m <message>
    git commit -m "添加新版本说明"
***
删除文件↓
>*rm =? remove：移出；删除*

    git rm <文件名>
    git rm -f <文件名> //强制删除 已提交到暂存区时可用
    git rm --cached <文件名> //从暂存区删除

***
回退版本↓
>*ref：参考*

    git log //查看提交历史，获得commit_id，用于回退指定版本
    git reflog //查看键入命令历史，用于回到新版本
    git reset --hard commit_id //回退到指定版本
    git log --graph //获得分支合并图

***
查看仓库当前状态↓  
>*status：状态*  
>查看工作区是否有修改或提交

    git status
***
查看内容差异↓
>*diff == difference：差异；不同*  

    git diff <文件名> //查看文件差异
    git diff --cached //查看暂存区和仓库的差异
    git diff HEAD //查看工作区和仓库的差异

远程仓库 (GitHub)
----------
创建SSH Key↓

    ssh-keygen -t rsa -C "邮箱"
弹出提示使用默认值即可，创建成功后可以在用户主目录里找到隐藏文件夹```.shh```，内包含私钥```id_rsa```和公钥```id_rsa.pub```  
GitHub内打开Add SSH Key，把公钥的内容粘贴到Key里即可推送项目到GitHub中
>Windows的用户主目录就是cmd/终端打开时显示的位置

    cd ~ //进入用户主目录
    pwd //获取当前路径
***
关联一个远程库↓  
>在想要关联的项目仓库目录下执行以下命令

    git remote add origin git@github.com:Yuzummmmmm/gitskills.git 
    //后面为项目远程仓库地址
    
推送内容到远程库↓

    git push -u origin master //第一次推送master分支的所有内容
    git push origin master //推送最新修改
***
克隆远程库的项目↓  
>把远程库的项目克隆到当前目录中  
>可以使用```ssh```协议或者```https```协议  
>Git支持多种协议，但```ssh```最快

    git clone git@github.com:Yuzummmmmm/gitskills.git
    git clone https://github.com/Yuzummmmmm/gitskills.git
    
分支管理
--------
>*branch == 分支*  
>*-d =? delete*  
>*-c =? create*

    git branch //查看当前分支
    git branch <分支名> //创建一个分支
    git branch -d <分支名> //删除一个分支
    git switch <分支名> //切换到该分支
    git switch -c <分支名> //创建并切换到该分支
    <!--git checkout <分支名> //切换到该分支-->
    <!--git checkout -b <分支名> //创建并切换到这个分支-->
    git merge <分支名> //合并该分支到当前分支
***
分支管理策略  
通常合并分支时，如果可能，Git会用```Fast forward```(快进)模式，但在这种模式下，删除分支后，不会保存分支信息。  
如果要强制禁用```Fast forward```模式，Git会在合并时生成一个commit（```-m```），这样就可以从分支历史里看到分支信息。
>```--no-ff == no Fast forward```

    git merge --no-ff -m <message> <分支名>
这样就可以在删除分支以后也可以看到分支信息了
***
Bug分支  
当在开发途中，不得不中断当前工作来修复bug时，可以使用```stash```来保存工作区的改动

    git stash //暂时把工作区储存起来
现在使用```git status```查看状态时，工作区是干净的  
当bug修复完成时，可以查看储存列表重新调出工作区

    git stash list //查看所有储存到stash的工作区
    git stash apply stash@{n} //恢复选中的工作区，但不删除储存到stash的工作区
    git stash pop stash@{n} //恢复选择的工作区并删除储存在stash的工作区
若想把修复的bug同步到另一个分支中  

    git cherry-pick <commit_id> //使用合并时的commit，再给当前分支再合并一次