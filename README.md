# yzxwn.github.io

### 地址
https://yzxwn.github.io

### 描述
对前端学习的一些技术和知识点总结

### 步骤
1.创建git项目，名称为“用户名.github.io”<br/>
2.本地下载git项目
```js
//不提交.idea文件
git rm -r --cached .idea
在.gitignore文件中添加.idea

```
3.配置gitbook
```
1、下载gitbook：npm i gitbook-cli -g
2、初始化：gitbook init
3、配置SUMMARY.md文件
4、报错：将.gitbook\versions\3.2.3\lib\output\website\copyPluginAssets.js文件112行confirm设为false
```
4.修改package.json文件
```js
"bookIns": "gitbook install",
"bookBuild": "gitbook build && xcopy/Y _book /e", //拷贝_book文件夹下的所有文件到根目录
"bookStart": "gitbook serve" //在本地4000端口启动
```
