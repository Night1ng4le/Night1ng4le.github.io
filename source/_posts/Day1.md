---
title: 365 - Day1：学习CTF Wiki栈溢出基础和ROP基础
categories: [Security]
tags: [CTF Wiki,Stack Overflow,ROP]
---

### 写在最前
[《365天获取玄武实验室的工作》](https://github.com/Vancir/365-days-get-xuanwulab-job)，推荐原版。

<!--more-->

### 栈溢出基础
#### Canary

#### 栈帧结构
![alt](https://pic3.zhimg.com/80/v2-c16e2bc9d6b8aecf1f1f891e12897c9a_1440w.jpg)


#### 栈溢出原理
[Stack Overflow Principle:](https://ctf-wiki.github.io/ctf-wiki/pwn/linux/stackoverflow/stackoverflow-basic-zh/)通过栈溢出覆盖掉函数栈帧的返回地址, 当函数返回时就会跳入攻击者覆写的地址继续执行代码.
栈溢出前提：
- 程序必须向栈上写入数据。
- 写入的数据大小没有被良好地控制。

> i. 确认溢出的长度可以到达栈帧返回地址
> ii. 确认没有开启Stack Canary
> iii. 确认覆写的地址所在的段具有**可执行权限**
> - 编译选项`-fno-stack-protector`用于关闭Stack Canary
> - 编译时需要加`-no-pie`确保不会生成位置无关文件，PIE（Position Independent Executable）
> - 关闭ASLR: `echo 0 > /proc/sys/kernel/randomize_va_space`
> - `-m32` - 生成32位程序
> - `gcc -v`查看默认PIE设置

关于ASLR：
- 0，关闭 ASLR，没有随机化。栈、堆、.so 的基地址每次都相同。
- 1，普通的 ASLR。栈基地址、mmap 基地址、.so 加载基地址都将被随机化，但是堆基地址没有随机化。
- 2，增强的 ASLR，在 1 的基础上，增加了堆基地址随机化。
修改命令`echo 0 > /proc/sys/kernel/randomize_va_space`

🌰：
```c++
#include <stdio.h>
#include <string.h>
void success() { puts("You Hava already controlled it."); }
void vulnerable() {
  char s[12];
  gets(s);
  puts(s);
  return;
}
int main(int argc, char **argv) {
  vulnerable();
  return 0;
}
```
这里`gets()`是一个危险函数，gets()以回车判断输入结束，不检验输入长度。

在这个例子中，目的是希望程序运行的时候可以跳到success函数执行。
丢入IDA反编译之后的结果是：
```c++
int vulnerable()
{
  char s; // [esp+4h] [ebp-14h]

  gets(&s);
  return puts(&s);
}
```
该字符串距离 ebp 的长度为 0x14（注意这里是16进制），所以对应的栈结构为：
```
               +-----------------+
               |     retaddr     |
               +-----------------+
               |     saved ebp   |
        ebp--->+-----------------+
               |                 |
               |                 |
               |                 |
               |                 |
               |                 |
               |                 |
  s,ebp-0x14-->+-----------------+
```
同时可以从IDA获取success函数的起始地址为“0x08048456”
```c++
.text:08048456 ; int __cdecl success()
.text:08048456                 public success
.text:08048456 success         proc near
.text:08048456
.text:08048456 var_4           = dword ptr -4
.text:08048456
.text:08048456 ; __unwind {
.text:08048456                 push    ebp
.text:08048457                 mov     ebp, esp
.text:08048459                 push    ebx
.text:0804845A                 sub     esp, 4
.text:0804845D                 call    __x86_get_pc_thunk_ax
.text:08048462                 add     eax, 1B9Eh
.text:08048467                 sub     esp, 0Ch
.text:0804846A                 lea     edx, (aYouHaveAlready - 804A000h)[eax] ; "You Have already controlled it."
.text:08048470                 push    edx             ; s
.text:08048471                 mov     ebx, eax
.text:08048473                 call    _puts
.text:08048478                 add     esp, 10h
.text:0804847B                 nop
.text:0804847C                 mov     ebx, [ebp+var_4]
.text:0804847F                 leave
.text:08048480                 retn
.text:08048480 ; } // starts at 8048456
.text:08048480 success         endp
```
注：IDA使用空格切换反汇编窗口的图形和文本。

因为gets函数不检查输入长度，所以输入的字符串可以设定为
```
0x14*'a'+'bbbb'+success_addr
```
此时新的栈结构为：
```
               +-----------------+
               |     0x08048456  |
               +-----------------+
               |      bbbb       |
        ebp--->+-----------------+
               |                 |
               |                 |
               |                 |  #这部分填充a
               |                 |
               |                 |
               |                 |
  s,ebp-0x14-->+-----------------+
```

