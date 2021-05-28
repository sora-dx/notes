# GitHub基础使用

## 介绍

GitHub 是一个 Git 仓库管理 网站。可以创建远程中心仓库，为多人合作开发提供便利。

## 使用流程

GitHub 远程仓库使用流程较为简单，主要有以下几种场景：

### 本地有仓库,远程没有仓库

1. 注册并激活账号

2. 创建 GitHub 中心仓库

   

3. 获取仓库的地址

   

4. 本地配置远程仓库的地址

   ```shell
   git remote add origin https://github.com/nowLetsgo/test.git
       //remote 添加一个远程仓库的url的别名
       //add  添加
       //origin 远端仓库的别名（git remote -v 可以查看仓库所有的别名）
       //https://github.com/nowLetsgo/test.git    仓库地址
       //git remote可以添加删除重命名等操作（使用 git remote -h查看）
   ```

5. 本地提交（确认代码已经提交到本地仓库）

6. 将本地仓库某个分内容推送到远程仓库

   ```shell
   git push -u origin master
       //
       push 推送
       -u   关联, 加上以后,后续提交时可以直接使用 git push
       origin 远端仓库的别名
       master 本地仓库的分支
   
   ```

### 本地没有仓库,远程有仓库

1. 注册并激活账号

2. 克隆仓库

   ```shell
   git clone https://github.com/nowLetsgo/test.git [name]
   //name 是对仓库名字的修改
   ```

3. 增加和修改代码

4. 拉取本地没有的分支

   ```js
   git fetch origin dev:dev
   ```

5. 本地提交

   ```shell
   git add .
   git commit -m 'message'
   ```

6. 推送到远程

   ```shell
   git push
   ```

> 克隆代码之后， 本地仓库会默认有一个远程地址的配置， 名字为 origin



# 协作流程

## 入职第一天

- 得到 Git 远程仓库的地址和账号密码

- 将代码克隆到本地（地址换成自己的）

  ```shell
  git clone https://github.com/XXXXXXX/test.git
  ```

- 切换分支

  ```
  git checkout -b XXXXXX
  ```

- 开发代码

- 本地提交

  ```shell
  git add -A
  git commit -m '注释内容'
  ```

- 合并分支

  ```shell
  git checkout master
  git merge XXXXXX
  ```

- 更新本地代码

  ```shell
  git pull
  //或者使用下面两行代码
  git fetch 
  git merge origin/master
  ```

- 提交代码

  ```shell
  git push 
  ```

## 第二天工作流程

1. 更新代码 (git pull)
2. 切换分支
3. 开发功能
4. 提交
5. 合并分支
6. 更新代码
7. 提交代码

#### 冲突解决

同分支冲突一样的处理，将代码调整成最终的样式，提交代码即可。

# 免密登录

1. 创建非对称加密对

   ```sh
   1. ssh-keygen -t rsa -C "xxx@xxx.com"
   
   2.  按三下回车生成秘钥
   ```

2. 文件默认存储在家目录（c:/用户/用户名/.ssh）的 .ssh 文件夹中。

   - id_rsa 私钥
   - id_rsa.pub 公钥

3. 将公钥（.pub）文件内容配置到账号的秘钥中

   - 首页 -> 右上角头像-> settings -> SSH and GPG keys -> new SSH Key

4. 克隆代码时，选择 ssh 模式进行克隆 （地址 在仓库首页 绿色 克隆的位置 选择 use ssh）

   ```shell
   git clone git@github.com/xiaohigh/team-repo-1.git 
   ```

   