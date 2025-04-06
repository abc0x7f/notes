# 准备工作
## Git安装
## 生成SSH-KEY
```bash
ssh-keygen -t rsa -C "EMAIL"
# generate ssh-key in file C:\USERS\{USERNAME}\.ssh\id_rsa by default
```
id_rsa.pub 公钥
id_rsa 私钥
## 绑定SSH-KEY至github
1. github.com
2. Settings
3. SSH and GPG keys
4. New SSH key
5. Add SSH key
验证绑定是否成功:
```bash
ssh -T git@github.com
```
```
You've successfully authenticated, but ...
```
## 绑定github账号至Git
```bash
git config --global user.name "USERNAME"
git config --global user.email "EMAIL"
# "EMAIL" must be the same as the email on github.com
```
# Git命令
## 基础命令
```bash
git init
# 初始化库
git pull origin main
# 从远程主分支拉取至本地主分支
git push origin main
# 将本地主分支推送至远程主分支
git add FILENAME
# 将文件FILENAME加入跟踪列表
git commit -m "NOTATION"
# 将修改提交至分支并注释
git diff FILENAME
# 跟踪文件变化
git reset --hard HEAD^
# 将版本回退至一次提交前
git reset --hard HEAD^^
# 将版本回退至两次提交前
git reset --hard HEAD~100
# 将版本回退至100次提交前
git reflog
# 显示历史版本号(包括从某版本往回退后该版本的版本号)
git reset --hard RELEASE
# 将版本回退至该版本号
```
## 工作区与暂存区
工作区: **文件管理器**中的目录和文件.
版本区: 隐藏文件夹.git包含的版本信息,版本区又包含**暂存区**,还有自动创建的分支main,以及指向main的一个指针HEAD.
git add 实际上就是将文件添加到暂存区;
git commit 是将暂存区的所有内容提交到当前分支.
## 撤销修改与删除文件
```bash
git reset --hard HEAD^
# 还原为上一版本

git status
# 查看当前状态
git checkout -- FILENAME
# 将工作区的FILENMAME文件还原为暂存区的该文件
```
```bash
git add a.txt
git commit -m ""
# 将a.txt的修改提交至版本库
rm a.txt
# 删除a.txt
git checkout -- a.txt
# 从版本库恢复a.txt
```
# github与Git
```bash
git remote add origin https://github.com/abc0x7f/example.git
# 将本地仓库与之关联
git push -u origin main
# 第一次推送并与远程main分支关联
git push origin main
# 以后的推送
git clone https://github.com/abc0x7f/example
# 克隆远程仓库至本地
```
# 创建与合并分支
## 创建分支
```bash
git checkout -b dev
# 创建并切换分支,-b表示切换,等于如下两条命令
git branch dev
git checkout dev

git branch
# 查看分支
```
## 合并分支
假设当前处于dev分支,需要将dev分支合并至main
```bash
git checkout main
# 切换至main分支
git merge dev
# 将dev分支合并至main
git branch -d dev
#删除dev分支
```
```bash
git merge --no-ff -m "NOTAION" dev
#禁用fastforward模式,删除分支后仍会保留分支信息
```
分支策略:首先main主分支一般情况下不允许直接提交,而是提交至dev分支,dev分支代码稳定后可以合并到主分支main上来.
## Git储存
当前分支开发到一半无法提交,又要修改原分支的bug.
```bash
git stash
# 将当前工作状态存储起来
git checkout -b 404
# 创建并切换临时debug分支
git checkout main
git merge --no-ff 404
# 合并临时分支至主分支
git branch -d 404
```
```bash
git stash list
# 查看储存区信息
git stash apply
# 不删除stash内容并恢复
git stash pop
# 删除stash内容并恢复
```
# 远程库
当你从远程库克隆时候,实际上Git自动把本地的main分支和远程的main分支对应起来了,并且远程库的默认名称是**origin**.
```bash
git remote
# 查看远程库信息
# 返回: origin
git remote -v
# 详细查看远程库信息
```
## 推送分支
```bash
git push origin main
```
Git会把该分支推送到远程库**对应的**远程分支上.
## 抓取分支
当我要推送的本地库和远程库有冲突时(远程库被他人修改):
```bash
git branch --set-upstream dev origin/dev
# 将远程库的dev分支与本地dev分支链接
git pull
# 从远程仓库拉取
# 如果报错按提示修改本地仓库文件使保持一致即可
git add .
git commit -m "NOTATION"
git push origin main
```