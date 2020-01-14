# 我的Hugo博客
## 前言
由于Hexo博客的生成速度太慢了，所以我开始使用Hugo博客
## 写博客
当使用Hugo博客后，写文章的姿势

```
hugo new post/202001-xxxxxx.md
```
## 生成静态文件
使用`hugo`命名，就会在public生成博客页面
```
hugo
```

## 发布博客
进入public文件
```
cd public
```
常规git操作
```
git add .
git commit -m "blog"
git remote add origin https://github.com/Weirdchun/Weirdchun.github.io.git
git push -u origin master
```
## 使用脚本发布博客
### 新建`deploy.sh`文件
每次发布都得进行上面四步，太麻烦了，使用脚本代替！
1. 在MyBlog根站点新建一个文件命名`deploy.sh`,写入git操作代码
```
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo -t even # if using a theme, replace by `hugo -t <yourtheme>`

# Go To Public folder
cd public
# Add changes to git.
git add -A

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back
cd ..


```

### 双击`deploy.sh`文件
双击后将开始部署，但是得输入Github账号与密码后才会自动部署。
**Tip**:每次都得输入密码非常麻烦，我们需要Git免登录

打开Git Bash， 
1. 在C盘MINGW64 ~$ 模式下，touch创建文件 .git-credentials：
```
touch .git-credentials
```
2. 用vim编辑此文件，
```
vim .git-credentials
```
3. 输入内容格式
 ```
https://username:password@github.com
 ```
4. 最后执行
```
git config --global credential.helper store
```




