---
title: GithubPages + Hexo 搭建博客
date: 2018-02-05 21:22:00
tags: GithubPages
---



## GitHubPages是什么？

GitHubPages 是 GitHub 公司为 [github](https://github.com) 上的工程所提供的概览网页。如果将上传的一个工程比作一本书，那么 GitHubPages 可以看做书本的封面。有封面的目的很简单，就是为了使工程看起来更美观和更容易读懂。

比如，我把搭建本 Blog 网站的工程 fork 到自己的 github 网站  [uniapp10/hexo-theme-BlueLake](https://github.com/uniapp10/hexo-theme-BlueLake) ，打开后你会看到：

![ProjectPages](http://p3gaf3kiq.bkt.clouddn.com/ProjectPages0.png)



眼前的一堆代码，给人的第一感觉是抽象，继而令人迷茫。但是如果我给它加上 GitHubPages ，变成 [uniapp10/hexo-theme-BlueLake](http://unicoinapp.top/hexo-theme-BlueLake/) ，打开后就变成：



![ProjectPages](http://p3gaf3kiq.bkt.clouddn.com/GitHubPage2.png)



是不是瞬间有种耳目一新、如浴春风的快感？而且我在副标题中指出了该工程的简介——一个简单的、能够在不同设备运行的 、基于 hexo 框架的主题。

作为封面仅仅是 GitHubPages 的一种使用场景，使用它还可以为工程封面指定自定义域名。更重要的是可以创建自己的静态  Blog 网站，这才是文章的重点内容。基于 github 为程序猿服务的先天基因，简直不能太好用，下面详细介绍一下它的使用方式。详细的介绍可以参考官方文档 [GitHubPages](https://pages.github.com/) 。

## 有什么限制？



1 GitHubPages 为每个工程提供的空间大小上限为 1GB，来搭建个人 Blog 网站绰绰有余。

2 每月访问 GitHubPages 的带宽上限为 100GB。

3 GitHubPages 编译的频率低于每小时10次 ，完全满足个人  Blog 静态网页的要求。

## 如何使用？

#### 找到 GitHubPages

GitHubPages 入口按照下面的步骤可以找到：

1 点击工程设置：

![GitHubPages](http://p3gaf3kiq.bkt.clouddn.com/GitPages0.png)

---

2 下滑到 GitHub Pages，可以看到其超链接：

![GitHubPages](http://p3gaf3kiq.bkt.clouddn.com/GitPages.png)

---

3 下滑到底部，可以看到官方推荐搭建 Blog 的 [Jekyll框架](https://jekyllrb.com/docs/quickstart/) :



![GitHub官方推荐Blog框架](http://p3gaf3kiq.bkt.clouddn.com/GitBlog.png)

 Jekyll 框架文档为英文，所以英文不是障碍的友人可以选择，偷懒的我选择了易读的汉化 [hexo框架](https://hexo.io/zh-cn/docs/index.html) 。

#### 创建工程



相信开发者都拥有自己的 [github](https://github.com/) 账号。什么？没有？好吧，没有的也没关系，申请很简单。不要被全英文的网站所吓倒，反复几次过后你会发现——和申请QQ的套路没多大差别。

登录 gitHub 账号，新建工程：

![新建GitHub工程](http://p3gaf3kiq.bkt.clouddn.com/Git%E4%BB%93%E5%BA%93.png)

工程名称有严格的限制，具体命名要求可以在 [官网文档](https://help.github.com/articles/user-organization-and-project-pages/) 找到。

![命名要求](http://p3gaf3kiq.bkt.clouddn.com/Git%E4%BB%93%E5%BA%93%E5%90%8D.png)

#### 安装Hexo



安装步骤可以参照：[hexo安装](https://hexo.io/zh-cn/docs/index.html)

#### 选取使用的主题

[挑选主题](https://hexo.io/themes/) ，不同的主题，安装方式不同，具体安装方式可以在各主题的 github 中看到。我选择的是 [BlueLake](https://github.com/chaooo/hexo-theme-BlueLake) 。推荐排名靠前的主题样式，因为它们不仅意味着符合大众的审美，而且往往 github 上面的使用步骤写的全面详细。相信一句话：「群众的眼光是雪亮的」。

#### 为工程配置域名



首先需要购买域名。推荐在国内的几大服务商处购买，它们还附带有解析、备案等一系列服务。我在阿里云购买的 .top 域名，售价 ¥2 大洋。

购买成功后，添加解析地址。各服务商的解析方式都差不多，下面以阿里云的域名解析为例：

![解析域名](http://p3gaf3kiq.bkt.clouddn.com/%E8%A7%A3%E6%9E%90%E5%9F%9F%E5%90%8D.png)

添加 www 和不带 www 的两个解析地址。其中带 www 的域名解析到不带 www 的地址，不带 www 的域名解析到 username.github.io。这样可以让从两个地址的访问记录统一到我们的 github 上面的地址，有利于提高网站在 Google 和 Baidu 的排名。

配置项目。打开新建的 username.github.io 工程，在工程中新建文件，取名为 CNAME 。内容为自己要绑定的域名。

![CNAME命名](http://p3gaf3kiq.bkt.clouddn.com/%E6%B7%BB%E5%8A%A0CNAME0.png)

我填写的内容：

![CNAME命名](http://p3gaf3kiq.bkt.clouddn.com/%E6%B7%BB%E5%8A%A0CNAME.png)





一切顺利的话，输入购买的域名，就能看到自己的 Blog 网站啦。快给自己点个赞吧。

#### 发表新文章

依据 GitHub 搭建的 Blog 网站文章，实际是一个静态网页。该网页内容可以依据 MarkDown 创建。书写的 Blog 文件需要存放到正确的位置。该位置可以参照主题自带的 hello 文件。比如我选择主题的 hello.md 文件，存放在 根目录 `/source/_posts/` 下。因此我只要在该目录下，ctrl + d 复制 hello.md ，然后修改文件标题就可以开始写 Blog 了。

## 不可缺少的能力

一篇令人赏心悦目的文章，少不了标题、插图。所以需要掌握以下两种 Blog 写作技能：

1 [ MarkDown 语法](http://wowubuntu.com/markdown/#em) 。

2 图片存放到云上。

如果将配图放在我们本身网站中，有两个缺点：

​	2.1 会造成网页空间迅速增大（别忘了空间上限为1GB）; 

​	 2.2 引用和管理不方便，缺少配图管理工具。

如果把图片全部放到云上面，然后在文章中以外部链接的方式引用，就能轻松解决上述两个缺点。易用并且带有图片资源外链生成功能的厂家，推荐国内的七牛云 。温馨提示一下：七牛云认证时需要身份认证。

写好文字，配好图片，加上适当的排版美化，一篇热气腾腾、洋溢着成就感的文章就完成了。

然后使用 hexo 命令部署到服务器上：

```
hexo g -d
```

最后使用 Git 命令提交到远程仓库，大功告成！

不熟悉 hexo 命令的小伙伴，可以在终端使用 `hexo help` 命令获取对 hexo 命令参数的详细解释：

```
Commands:
  help     Get help on a command.
  init     Create a new Hexo folder.
  version  Display version information.

Global Options:
  --config  Specify config file instead of using _config.yml
  --cwd     Specify the CWD
  --debug   Display all verbose messages in the terminal
  --draft   Display draft posts
  --safe    Disable all plugins and scripts
  --silent  Hide output on console
```

这种学习方法对所有的终端命令都有效，包括 Git 在内。记住——这个武林绝招只传男，不传女。不然怎么能体现咱们程序猿们的一阵噼里啪啦的高深莫测呢？

步骤比较繁琐，但是顺利做完，我们对网站搭建会形成整体的认识。Blog 只是一个简单的网站，我们日常接触的企业网站比较复杂，需要不同节点专业人员的相互配合。比如，会有设计 UI 的 MM, 处理前端逻辑的程序猿，后台处理数据、提供服务的运维人员等，每一个步骤都有专业的人去处理。通过搭建 Blog 认识到这些，相信以后与别人有更默契的配合！