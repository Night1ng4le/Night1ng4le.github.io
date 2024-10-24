---
title: Internet Protocol
categories: [Network]
tags: [BaseCS,Backend]
---

各种协议备忘

<!--more-->

#### 动态主机配置协议（DHCP，Dynamic Host Configuration Protocol）

计算机通信时，DHCP给计算机分配一个IP地址，并通过协议告知用户其IP。用户计算机通过UDP使用该协议和DHCP Server通信，该服务器跟踪网络中的计算机及其IP地址。

#### 域名系统协议(DNS，Domain Name System Protocol)

当用户在网络浏览器中访问一个网站时，例如meta.com，计算机需要一种方法来知道与哪个IP地址进行通信。用户计算机通过域名相关的DNS服务器进行检查，然后返回正确的IP地址。

#### 互联网信息访问协议(IMAP，Internet Message Access Protocol)

用户设备通过IMAP来下载电子邮件，并在存储的电子邮件的服务器上管理自己的邮箱。

#### 简单邮件传输协议（SMTP，Simple Mail Transfer Protocol）

现在电子邮件已经在设备上，需要一种方法来发送电子邮件。使用SMTP。它允许电子邮件客户端通过SMTP服务器提交电子邮件进行发送。也可以用它来接收来自电子邮件客户端的电子邮件，但更常用IMAP。

#### 邮政协议(POP，Post Office Protocol)
邮政协议（POP）是一个较早的协议，用于下载电子邮件到电子邮件客户端。POP和IMAP的主要区别是，POP会在邮件下载到本地设备后删除服务器上的邮件。虽然它不再普遍用于电子邮件客户端，但开发人员经常使用它来实现电子邮件自动化，因为它是一个比IMAP更直接的协议。

#### 文件传输协议（FTP，File Transfer Protocol）
当在互联网上运行你的网站和网络应用程序时，需要一种方法将文件从你的本地计算机传输到它们要运行的服务器上，通常使用标准协议是FTP。FTP允许用户在服务器上列出、发送、接收和删除文件。服务器必须运行一个FTP服务器，本地机器需要运行一个FTP客户端。

#### SSH协议（SSH，Secure Shell Protocol）
当你开始使用服务器时，你还需要一种方法来登录并与计算机进行远程交互。最常见的方法是使用SSH协议。使用SSH客户端允许你连接到服务器上运行的SSH服务器，在远程计算机上执行命令。所有通过SSH发送的数据都是加密的。

#### SSH文件传输协议（SFTP，SSH File Transfer Protocol）
使用文件传输协议时，数据的传输是不安全的，有可能被第三方截获。为了解决这个问题，可以使用SSH文件传输协议，这可以确保数据安全传输。大多数FTP客户端也支持SFTP协议。


