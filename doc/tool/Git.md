## Git

* **配置**
```js
//配置个人的用户名称和电子邮件地址
$ git config --global user.name "aaaaa"
$ git config --global user.email test@aaaaa.com
//设置Git默认使用的文本编辑器, 一般可能会是 Vi 或者 Vim。如果你有其他偏好，比如 Emacs 的话，可以重新设置
$ git config --global core.editor emacs
//在解决合并冲突时使用哪种差异分析工具。比如要改用 vimdiff 的话
$ git config --global merge.tool vimdiff
//查看配置信息
$ git config --list
http.postbuffer=2M
user.name=runoob
user.email=test@runoob.com
//直接查阅某个环境变量的设定，只要把特定的名字跟在后面即可
$ git config user.name
aaaaa
```
* **基本操作**
```js
//使用当前目录作为Git仓库，我们只需使它初始化
$ git init
//从现有 Git 仓库中拷贝项目到指定的目录
$ git clone <repo> <directory>
//查看项目的当前状态，"AM" 状态：这个文件在我们将它添加到缓存之后又有改动
$ git status -s
//显示已写入缓存与已修改但尚未写入缓存的改动的区别
$ git diff //尚未缓存的改动
$ git diff --cached //查看已缓存的改动
$ git diff HEAD //查看已缓存的与未缓存的所有改动
$ git diff --stat //显示摘要而非整个 diff
//添加文件到暂存区
$ git add .
//将缓存区内容添加到仓库中
$ git commit -m "描述"
$ git commit -am "描述" //跳过add命令
//取消已缓存add的内容
$ git reset HEAD 文件
//从 Git 中移除某个文件
$ git rm 文件
$ git rm -f 文件 //删除之前修改过并且已经放到暂存区
$ git rm --cached 文件 //把文件从暂存区域移除，但仍然希望保留在当前工作目录中
$ git rm –r * //进入某个目录中，执行此语句，会删除该目录下的所有文件和子目录
//移动或重命名一个文件、目录、软连接
$ git mv README  README.md
```
* **分支管理**
```js
//创建分支
$ git branch (branchname)
//列出分支
$ git branch
//删除分支
$ branch -d (branchname)
//切换分支
$ git checkout (branchname)
$ git checkout -b (branchname)  //创建并切换到新分支
//合并分支
$ git merge
//查看提交历史
$ git log --oneline
//标签
$ git tag -a v1.0
```