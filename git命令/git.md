### 单文件夹提交
```shell
//仓库初始化
git init 
//将文件提交到暂存区
git add .
//提交与提交信息
git commit -m "xxxx"
//与远程仓库建立连接
git remote add origin xxxxxx
//推送到master分支
git push origin master
```
### 多文件提交到同一个仓库的不同分支
#### 文件一(主文件，此时已经完成初始化项目等工作)
```shell
//仓库初始化
git init 
//将文件提交到暂存区
git add .
//提交与提交信息
git commit -m "xxxx"
//与远程仓库建立连接
git remote add origin xxxxxx
//查看所有分支以及当前分支
git branch -av
//创建新分支new_branch
git checkout -b new_branch
```
#### 文件二(需要合并的“外”文件)
```shell
//仓库初始化
git init 
//将文件提交到暂存区
git add .
//提交与提交信息
git commit -m "xxxx"
//与远程仓库建立连接
git remote add origin xxxxxx
//查看所有分支以及当前分支
git branch -av
//创建新分支new_branch
git checkout -b new_branch
//切换到目标分支
git checkout new_branch
//进行推送
git push origin new_branch

```