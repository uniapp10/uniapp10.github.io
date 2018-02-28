---
title: 小白 Mac下使用 Apache 服务器
date: 2018-02-25 20:37:00
tags: Apache
---

作为小白入门软件开发中，涉及到网络部分时，内心就会产生很多迷惑。比如网络请求中采用的 http 和 ftp 协议，网络数据传输的七层模型，域名和 IP 需要对应时的解析等，理解起来都比较抽象。下面以配置 Mac 下的 Apache 服务器为目标，从实际开发人员的角度，针对小白用户，介绍一下网络请求的过程，以便于开发中遇到网络问题能够整体把握，逐步排查错误。

#### 什么是服务器？

顾名思义，服务器就是提供服务的机器。我们可以向服务器发送请求，获取服务。类比日常生活中的场景：将服务器比作银行，它可以提供兑换现金的服务。如果我们需要现金，就去柜台向银行业务员提出要求（发送请求），如果满足条件，我们就能得到想要的现金（获取服务）。

#### 一个完整的网络请求需要哪些过程？

我们在浏览器输入 `http://www.baidu.com` 的时候，就能获取百度首页。从具体实现上面，经历以下 3 个过程：

###### 1 解析域名，获取百度主机地址；

互联网上的任意一台主机都是以 IP 地址标识的，比如我们主机在局域网中的地址通常都是都是 `192.168.xxx.xxx` 的形式。通过 IP 地址，能够准确确定一台主机在互联网的位置，但是准确记忆多个 IP 地址却比较困难。聪明的科学家想出了用域名来作为 IP 地址的别名来帮助记忆，比如 `baidu.com` 比起 `138.168.0.1 ` 记忆的难度就会大大降低。

按照设计规则，解析域名的工作有专门的服务器完成，解析的过程由主机自动完成。但是为了加快解析速度，本地主机会将解析成功的域名和 IP 的对照关系缓存到本地。在我们输入域名发送请求时，主机会首先寻找本地缓存中与域名对应的 IP 地址。

######2 与百度主机建立连接；

解析百度域名为 IP 地址后，就能通过 IP 地址与百度主机建立连接，也就是我们经常听到的 TCP/IP 连接。

######3 通过协议获取服务；

建立连接后，百度对我们发送的首页请求做出响应，返回具体内容。在本机按照一定的规则解析后，就是我们看到的样子。

Mac 机器下，解析域名缓存的文件为 `/private/etc/hosts` ，打开文件，能看到 IP 和域名相信的对应关系：

```
216.58.200.192	android.com
216.58.200.192	www.android.com
216.58.200.192	a.android.com
216.58.200.192	connectivitycheck.android.com
216.58.200.192	d.android.com
...
```

我们可以按照自己的喜好，在该文件中手动添加或修改域名和 IP 的对应关系。

在浏览器中输入的内容除了 `baidu.com` 的域名外，还有 `http://www` 。其中 http 标识使用的协议，`www` 标识访问主机上的文件位置。

####Apache 服务器的优点？

Mac 电脑下自带了 Apache 服务器，可以通过它在我们本机模拟网络请求，对开发中的应用进行测试。结合 Apple 最求安全的理念，应该能够猜出 Apache 作为服务器的特点：稳定。而且 Mac 本身自带，使用起来免去了安装的麻烦。

####配置 Apache 服务器

Mac 中的 Apache 服务器默认处于关闭状态，它在本机的安装目录为 `/private/etc/apache2` 。

打开配置文件 `httpd.conf` ，去掉 `Include /private/etc/apache2/extra/httpd-vhosts.conf` 前的 # ， 启动虚拟机服务。

打开文件 `/private/etc/apache2/extra/httpd-vhosts.conf` ，可以看到默认打开了 80 端口。我们可以手动添加服务器监听端口，比如监听端口 8002， 添加如下代码：

```
<VirtualHost *:8002>
    ServerAdmin webmaster@dummy-host2.example.com
    DocumentRoot "具体目录"
    ServerName mysite
    ErrorLog "/private/var/log/apache2/dummy-host2.example.com-error_log"
    CustomLog "/private/var/log/apache2/dummy-host2.example.com-access_log" common
    <Directory />
                Options Indexes FollowSymLinks MultiViews
                AllowOverride None
                Order deny,allow
                Allow from all
    </Directory>
</VirtualHost>
```

如果出现无法修改文件的提示，参考下面的修改文件权限。

####修改文件权限

文件权限属于文件属性的一种，可以通过查看文件属性方式修改：双击文件 —>显示简介—>共享与权限，能够看到文件具体的读取权限详情，点击右下角的 🔐 按钮，输入开机密码后更改权限。

当然也可以通过命令行的方式修改。在终端输入更改文件的命令 `chmod u+w 文件路径`  就能修改文件为可读。对详细参数有兴趣的童鞋，可以参考 [Linux命令:修改文件权限命令chmod、chgrp、chown详解](http://www.cnblogs.com/Berryxiong/p/6193866.html) 。

####启动 Apache 服务器

在终端输入 `sudo apachectl restart` 重新启动 Apache 服务器，在浏览器地址栏输入 `http://127.0.0.1:8002` 就能看到我们设定好的 `具体目录` 下的文件详情。

根据前面讲述的原理，我们可以在` /private/etc/hosts` 文件中添加域名解析 `127.0.0.1	mysite` ，然后在浏览器地址栏输入`http://mysite:8002` 后能够看到同样的效果。

#### 总结

全文首先介绍了网络请求整体过程的实现原理，并且结合 Mac 电脑简单介绍了域名解析的过程。后面根据网络请求的原理，详细讲解了 Mac 电脑启动 Apache 服务器的过程。一步一步操作下来，实现步骤并不复杂。本文针对编程小白入门，省去了其中的域名解析的详细过程和请求数据的具体格式等内容，疑问之处欢迎留言交流。



