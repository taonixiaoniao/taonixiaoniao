# 命令大全

###### 初始化本地仓库

```js
git init //在目录中创建新的 Git 仓库。
```

###### 克隆

```js
 git clone [url] //拷贝一个 Git 仓库到本地，让自己能够查看该项目，或者进行修改。
```

###### 提交到暂存区

```js
git add [file] //提交一个文件
git add [file1][file2]... // 提交多个文件
git add [dir] // 提交指定目录，包括子目录
git add . // 提交目录下所有文件
```

###### 查看仓库状态

```js
git status // 查看在上次提交之后是否对文件再次修改
git status -s // 获得简短的结果
```

###### 提交到本地仓库

```js
git commit -m '注释'  // 提交暂存区到本地仓库中
git commit [file1][file2] // 提交暂存区指定文件到本地仓库
git commit -a // 跳过add操作直接提交到本地仓库
```

###### 删除工作区文件

```js
git rm [file]  // 指定文件从暂存区和工作区中删除
```

如果删除之前修改过并且已经放到暂存区中，就需要强制删除

```js
git rm -f [file] // 强制删除
```

文件从暂存区域移除，但工作区保留：

```js
git rm --cached <file>
```

###### 移动文件

git mv 命令用于移动或重命名一个文件、目录或软连接

```js
git mv [file] [newfile] // 重命名
git mv -f [file] [newfile] // 强制重命名
```

###### 查看提交记录

```js
git log // 查看历史提交记录
git log --oneline // 简洁版本
git log --reverse --oneline // 逆向显示提交日志
git log --author=Linus --oneline -5 // 查看指定用户Git源码中Linus提交的部分
git log --oneline --before={3.weeks.ago} --after={2010-04-18} --no-merges
// 查看三周前且在四月十八日之后的所有提交 --no-merges 选项以隐藏合并提交
git blame <file> // 查看指定文件的修改记录
```



###### 设置用户信息

```js
git config --global user.name 'runoob' // 设置用户名
git config --global user.email test@runoob.com // 设置邮箱
```

###### 查看本地仓库已经存放的文件

```
git ls-files
```

###### 将远程仓库合并到本地

```
git pull origin master 
```

###### 与远程仓库建立连接

```js
git remote add origin [url]
```

###### 更改与远程仓库连接

```js
git remote set-url [url]
```



###### 查看本地仓库与远程仓库的连接

```
git remote -v
```

###### 将本地仓库文件推送至远程仓库

```js
git push -u origin master
git push -f origin master // 强制推送
```

###### 删除远程仓库

```js
git remote rm name // 删除远程仓库
```

###### 修改仓库名

```js
git remote rename old_name new_name  // 修改仓库名
```

###### 版本回退

```js
git reset HEAD^ //回退所有内容到上一个版本
	git reset HEAD^ hello.php //回退 hello.php 文件的版本到上一个版本
	git reset 052e //回退到指定版本
	git reset --soft HEAD~3 //回退到上上上个版本
	git reset --hard HEAD~3 //回退到上上上个版本
	git reset --hard bae128 //(提交信息的头部)回退到某个版本回退点之前的所有信息
	git reset --hard origin/master //将本地的状态回退到远程一样
	//HEAD(HEAD~0)表示当前版本
	//HEAD^(HEAD~1)上个版本
	//HEAD^^(HEAD~2)上上个版本
```

###### 找回丢失的提交记录

```
git reflog
```

###### 查找近期提交记录

```
git log --oneline
```

###### 切换分支

```js
git checkout -b <baanch name> //切换到一个分支，如果没有则创建这个分支
```

###### 合并分支

```js
git merge //合并分支，把测试分支合并到主分支
```

###### 关联上游项目

```
git remote add upstream
```

# 常见问题

###### git add 问题

`LF will be replaced by CRLF in `

需要提交的文件是在`windows`下生成的，`windows`中的换行符为 `CRLF `， 而在`linux`下的换行符为 LF ，解决方案

```js
git config --global core.auto crlf false
```

###### git push 问题

不小心在项目的子文件中git init，导致上传时该子文件会变成一个子模块，需要取消子文件的git初始化，先把该文件下的.git文件删除，然后执行以下命令

```js
git rm -rf --cached
```

就重新从`git add`开始上传文件
