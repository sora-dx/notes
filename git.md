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
- git fetch origin xxx:xxx 拉取远程仓库xxx分支到本地仓库xxx分支（如果本地xxx分支不存在，会自动创建）
- git checkout xxx 切换到xxx分支
