---
title: centos 6.3 python 2.6版本升级到2.7
date: 2017-08-14 00:00:00
categories: python,linux
tags:
 - linux
 - python
---

centos 操作系统6.3 python版本由2.6升级到2.7

 <!-- more -->

## 操作流程

1. **查看当前python版本**
python  -V

2. **下载Python-2.7.3**
wget http://python.org/ftp/python/2.7.3/Python-2.7.3.tar.bz2
（备注：如果不能下载，可直接在浏览器输入上面地址，下载好以后，上传到机器即可）

3. **更改工作目录**
cd Python-2.7.3

4. **安装**
./configure
make all
make install

5. **查看安装后的版本信息**
/usr/local/bin/python2.7 -V

6. **建立软连接，使系统默认的 python指向 python2.7**
mv /usr/bin/python /usr/bin/python2.6.6 #移除原有的2.6
ln -s /usr/local/bin/python2.7 /usr/bin/python

7. **重新检验Python 版本**
python -V

8. **解决系统 Python 软链接指向 Python2.7 版本后，因为yum是不兼容 Python 2.7的，所以yum不能正常工作，我们需要指定 yum 的Python版本**
vi /usr/bin/yum
将文件头部的 #!/usr/bin/python 改为 #!/usr/bin/python2.6.6