## github 博客project部署[centos8]
### 0.环境准备
#### nodejs 二进制安装包安装步骤
```
cd /home/lilinjing/software
wget https://npm.taobao.org/mirrors/node/v8.9.3/node-v8.9.3-linux-x64.tar.xz #可以自己配置下载的版本
tar xf node-v8.9.3-linux-x64.tar.xz 
ln -snf node-v8.9.3 nodejs
sudo su - 
ln -s /home/lilinjing/software/nodejs/bin/node  /usr/local/bin/node
ln -s /home/lilinjing/softwarenodejs/bin/npm   /usr/local/bin/npm
# 查看node 版本
node -v
```
#### hexo安装
```
npm install hexo-cli
# 如果没有自己的代码，可以执行init，生成一个属于自己的项目，如果已经有自己的代码，这步可以跳过
hexo init # 这里需要在一个空文件夹中执行，会生成一个新的项目
```

### 1.下载myblog 代码
```
git clone git@github.com:Llinjing/myblog.git
```

### 2.本地调试
按照自己的需求修改代码，其中_config.yml中为主页面可以配置不同的主题，public为子页面
```
hexo s
  启动当前服务，本地访问：localhost:4000
```

### 3.发布本地项目到github
```
hexo g
  生成静态文件，这个在要发布项目的时候执行
hexo d
  项目发布到github
```
注：如果报deploy文件异常，将该文件删除即可

### 4.项发布以后，将自己的本地代码提交到git，以便后续修改更新
```
git add .  # 提交当前修改的文件
git commit -m ""
git push
```

### 5.访问博客
https://llinjing.github.io/
