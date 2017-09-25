# blog_bak

我的博客的代码的备份

-----------------------------------------------------

## 项目的部署：

### 在已经安装了hexo的机器上，新建一个项目

* git clone git@github.com:Llinjing/myblog.git
* hexo s：启动当前服务，本地访问：localhost:4000
* hexo g：生成静态文件，这个在要发布项目的时候执行
* hexo d：项目发布到github
(执行以上命令即可)


### 在没有安装hexo的机器上，要先执行安装hexo的命令

```
npm install -g hexo
hexo init
```
然后下载该项目下的文件 <br />
在重新clone后，如果hexo服务本地无法访问，报WARN  No layout: index.html
解决：
查看themes文件夹下，是否有对应的主题文件夹
git clone https://github.com/MOxFIVE/hexo-theme-yelee.git themes/yelee

-----------------------------------------------------

## 项发布以后，备份项目的提交

```
git add . ：提交当前修改的文件
git commit -m ""
git push
```
-----------------------------------------------------



