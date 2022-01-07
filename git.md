# git

## 新建本地仓库，将本地仓库代码推送远程仓库去
1. 新建本地仓库
    create-react-app xxx
    创建react脚手架仓库代码，并初始化git仓库，进行一次版本控制

2. 新建远程仓库
    github访问速度太慢，使用gitee（码云）

3. 将本地仓库代码推送到远程仓库去
- git remote add origin xxx
- git push -u origin master

4. 新建开发分支，并推送到远程仓库去
- git checkout -b xxx  新建并切换到xxx分支
- git push origin xxx

## 拉取别人远程仓库代码
1. 克隆仓库
git clone xxx
注意：
- 使用https方式
- 克隆下来只有master分支代码

2. 拉取其他分支代码
- git fetch  origin xxx:xxx 拉取远程仓库xxx分支到本地仓库xxx分支（如果本地xxx分支不存在，会自动创建）
- git checkout xxx 切换到xxx分支

4.远程仓库更新拉取代码

方式一

-查看远程仓库

​	$ git remote -v

-从远程获取最新版本到本地

​	$ git fetch origin master 

​		从远程的origin仓库的master分支下载代码到本地的origin master

-比较本地的仓库和远程参考的区别

​	$ git log -p master… origin/master
​		su@SUCHANGLI /e/eoe_client/android-app (master)
​		因为我的本地仓库和远程仓库代码相同所以没有其他任何信息

-把远程下载下来的代码合并到本地仓库，远程的和本地的合并

 	$ git merge origin/master

远程代码下载到本地新建分支；对比区别后在合并）



 **git fetch** 和 **git merge FETCH_HEAD** 的简写。 命令格式如下：

**git pull**

****

方式二 （远程代码下载到本地新建分支；对比区别后在合并）

1.查看远程分支，和上面的第一步相同

2.从远程获取最新版本到本地

$ git fetch origin master:temp
From https://github.com/com360/android-app

- [new branch] master -> temp
  su@SUCHANGLI /e/eoe_client/android-app (master)
  git fetch origin master:temp 这句命令的意思是：从远程的origin仓库的master分支下载到本地并新建一个分支temp

比较本地的仓库和远程参考的区别
$ git diff temp
su@SUCHANGLI /e/eoe_client/android-app (master)
命令的意思是：比较master分支和temp分支的不同
由于我的没有区别就没有显示其他信息

1. 合并temp分支到master分支

$ git merge temp
Already up-to-date.
su@SUCHANGLI /e/eoe_client/android-app (master)
由于没有区别，所以显示Already up-to-date.
合并的时候可能会出现冲突，有时间了再把如何处理冲突写一篇博客补充上。

5.如果不想要temp分支了，可以删除此分支

$ git branch -d temp
Deleted branch temp (was d6d48cc).
su@SUCHANGLI /e/eoe_client/android-app (master)
如果该分支没有合并到主分支会报错，可以用以下命令强制删除git branch -D <分支名>

