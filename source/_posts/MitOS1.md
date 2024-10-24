---
title: 6.S081 Lab: Xv6 and Unix utilities
categories: [CS Basis]
tags: [MIT,OS,xv6]
---

#### 配置6.S081的实验环境
这个环境我是在mac本机上装的，最新的mac系统也支持gdb调试，所以我直接整到本机了～，只要你的homebrew安装的没问题，按照官方教程是可以装成的～

<!--more-->

```sh
# 过程贼长，建议找个网好的地方
$ xcode-select --install
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" # 安装homebrew，如果你装过了，更新一下即可
$ brew tap riscv/riscv #我装这一步的时候报错了，在github下载之后手动解压到指定目录也是一样的
$ brew install riscv-tools
$ PATH=$PATH:/usr/local/opt/riscv-gnu-toolchain/bin
$ brew install qemu
```
检测安装有没有成功
```sh
$ riscv64-unknown-elf-gcc --version
$ qemu-system-riscv64 --version
```
```sh
# 下载对应的xv6
$ git clone git://github.com/mit-pdos/xv6-riscv.git
# 下载xv6对应的书 
$ git clone git://github.com/mit-pdos/xv6-riscv-book.git
```
如果都成功了，即可开始实验
```sh
$ cd xv6-riscv
$ sudo make qemu  # 这种启动方式是直接进入xv6的

# 也可以通过gdb观测xv6启动过程
$ cd xv6-riscv
$ sudo make qemu-gdb
# 在命令行提示之后，打开另一个窗口启动gdb
```

附上homebrew的安装和卸载脚本，贼好用QAQ
```sh
# 安装脚本（自动选择源）
$ /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
# 卸载脚本
$ /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/HomebrewUninstall.sh)"
```

### Boot xv6
先下载xv6对应的实验环境，git我自己用的不是很熟，所以卡了一会（事实上是我并不聪明）
```sh
$ sudo git clone git://g.csail.mit.edu/xv6-labs-2020

$ cd xv6-labs-2020

$ git checkout util
$ make qemu
```
这里我的riscv-gnu-toolchain遇到了点问题，brew直接装的识别不了一些指令，然后网络环境又特别垃圾，所以下述是对我而言有用的安装方法，如果网好就不用这样分模块下载！！
```sh
$ git clone https://github.com/riscv/riscv-gnu-toolchain
$ cd riscv-gnu-toolchain
$ git clone --recursive https://github.com/riscv/riscv-qemu.git
$ git clone --recursive https://github.com/riscv/riscv-newlib.git
$ git clone --recursive https://github.com/riscv/riscv-binutils-gdb.git
$ git clone --recursive https://github.com/riscv/riscv-dejagnu.git
$ git clone --recursive https://github.com/riscv/riscv-glibc.git
$ git clone --recursive https://github.com/riscv/riscv-gcc.git
```
然后进行一下操作避免编译出错（我不知道为什么，但确实有用）
```sh
$ cd riscv-qemu
$ cp -a * ../qemu
$ cd riscv-binutils-gdb
$ cp -a * ../riscv-gdb
$ cp -a * ../riscv-binutils
```
接着，
```sh
$ vim ~/.bashrc
```
```sh
# 我自己的文件里内容是这样的，因为我也不知道具体是哪行有效果
PATH=$PATH:/usr/local/opt/riscv-gnu-toolchain/bin
export  RISCV="/home/kaguo/riscv/riscv-tools/riscv-gnu-toolchain"
export PATH=$PATH:$RISCV/bin
```
然后
```sh
$ source ~/.bashrc
```
安装依赖项
```sh
$ brew install python3 gawk gnu-sed gmp mpfr libmpc isl zlib expat
```
用下面的命令开始编译riscv gun tool chain
```sh
$ ./configure --prefix=$RISCV
$ make
```

说回这个实验，记录自己的实验结果
```
xv6 kernel is booting

hart 1 starting
hart 2 starting
init: starting sh
$ 
# 此时xv6成功运行

$ ls
.              1 1 1024
..             1 1 1024
README         2 2 2059
xargstest.sh   2 3 93
cat            2 4 24048
echo           2 5 22872
forktest       2 6 13216
grep           2 7 27384
init           2 8 23968
kill           2 9 22848
ln             2 10 22792
ls             2 11 26280
mkdir          2 12 22952
rm             2 13 22936
sh             2 14 41824
stressfs       2 15 23952
usertests      2 16 147576
grind          2 17 38064
wc             2 18 25184
zombie         2 19 22344
console        3 20 0

# 输入ctrl+p，显示当前正在运行的进程
$
1 sleep  init
2 sleep  sh
```
To quit qemu type: `Ctrl-a x`.

### Grading and hand-in procedure
运行`make grade`可以测试实验结果的成绩，运行`make handin`提交实验终稿

#### sleep（easy）

