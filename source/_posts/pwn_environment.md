---
title: 安装完ubuntu虚拟机之后要做的事
categories: [Memo]
tags: [ctf,tool]
---

#### 写在最前

因为我的虚拟机隔三差就会因为我的手残操作阵亡一次，为了不用每次重装都要搜过程，我决定直接写下来QWQ。
前置背景是MacBook pro， ubuntu是18.04.5。毕竟万一哪天真的有人搜到做参考呢（我怕不是在做梦）

<!--more-->

#### 安装VMware tools

我装这个是为了实现自由的复制粘贴
装完ubuntu之后，重启开机，上面的工具栏虚拟机->安装VMware tools，桌面会自动出现一个光盘💿的图标，双击打开把里面的压缩包拖出来，双击解压（这是最适合我自己方式，大佬请选择自己喜欢的解压方式）
切换到刚才解压得到的文件夹
```sh
$ cd vmware-tools-distrib/
$ sudo ./vmware-install.pl  #如果你直接执行没什么毛病的话就不用sudo
```
开始执行之后第一条默认的选项是no，除了这个要手动输入y，其他的疯狂回车即可。
成功后看到的内容大概是这样的
```
You must restart your X session before any mouse or graphics changes take 
effect.

To enable advanced X features (e.g., guest resolution fit, drag and drop, and 
file and text copy/paste), you will need to do one (or more) of the following:
1. Manually start /usr/bin/vmware-user
2. Log out and log back into your desktop session
3. Restart your X session.

Enjoy,

--the VMware team

$ 
```
重启，此时它就可以自由实现复制粘贴～

#### 更换镜像源
如果你在国外，就跳过这一步。
首先确定你的虚拟机联网了（别问我为啥要写这句话），接下来的操作就很简单了。

##### 备份原始源文件source.list

```sh
$ sudo mv /etc/apt/sources.list /etc/apt/sourses.list.backup
```

##### 修改source.list

```sh
# 修改文件权限，使其可以编辑
$ sudo chmod 777 /etc/apt/sources.list
# 打开source.list文件
$ sudo gedit /etc/apt/sources.list
```
修改为清华源（针对ubuntu 18.04版本的），内容如下：
```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```
当然如果你喜欢的话你也可以换成阿里源、163源、中科大源什么的，一定要记得对应自己ubuntu的版本！！！

换好之后更新一下源列表
```sh
$ sudo apt update
$ sudo apt upgrade
```
更新之后清理垃圾
```sh
$ sudo apt autoremove
```

#### 安装vim
一个文本编辑器
```sh
$ sudo apt install vim
```

#### 安装git
git clone的时候经常会用到这玩意
```sh
$ sudo apt install git

#如果你要写C/C++，再装个这个
$ sudo apt-get install build-essential
```
但我没有配置git，需要用的话自行百度吧

#### 安装pwntools
先安装依赖环境
```sh
# 安装capstone
$ sudo git clone https://github.com/aquynh/capstone
$ cd capstone
$ sudo make
$ sudo make install

# 安装setuptools
$ sudo apt-get install python-pip
$ sudo pip install setuptools
$ pip list # 查看是否成功

# 安装pwntools
$ sudo git clone https://github.com/Gallopsled/pwntools
$ cd pwntools
$ sudo python setup.py install
```
安装好之后，测试一下
```python
import pwn
```
没有报错即可

#### 安装peda
```sh
$ sudo git clone https://github.com/longld/peda.git ~/peda
$ sudo chmod 777 ~/.gdbinit
$ sudo echo "source ~/peda/peda.py" >> ~/.gdbinit 
```
运行一下gdb，成功的话提示符会变成红色的

