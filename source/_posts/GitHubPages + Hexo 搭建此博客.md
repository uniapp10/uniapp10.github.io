---
title: GithubPages + Hexo 搭建博客
date: 2018-02-05 21:22:00
tags: GithubPages
---

## GitHubPages是什么？

GitHubPages 是 GitHub 公司上传在 [github](https://github.com) 上的工程提供的概览网页，如果将上传的工程比作一本书，那么 GitHubPages 可以看做书本的封面。做封面的目的很明确，就是为了使工程更美观和易读。

比如，我把搭建改网站的主题 fork 到我在自己的 github 网站  [uniapp10/hexo-theme-BlueLake](https://github.com/uniapp10/hexo-theme-BlueLake) ，打开后你会看到如下效果：

![ProjectPages](http://p3gaf3kiq.bkt.clouddn.com/ProjectPages0.png)



展示眼前的是一堆代码，给人的第一感觉是抽象，继而迷茫。但是如果我给它加上 GitHubPages ，变成[uniapp10/hexo-theme-BlueLake](http://unicoinapp.top/hexo-theme-BlueLake/) ，打开后变成如下效果：



![ProjectPages](http://p3gaf3kiq.bkt.clouddn.com/ProjectPages.png)



是不是有种耳目一新，瞬间有种如浴春风的快感？因为我在副标题中明确指出了该工程是——一个简单的、能够在不同设备运行的 、基于 hexo 框架的主题。

作为封面仅仅是 GitHubPages 的一种使用场景，使用它还可以为工程封面指定自定义域名，更重要的是可以创建自己的静态  Blog 网站，而且统统免费，简直不能太好用。更详细的介绍可以在官方的 [GitHubPages](https://pages.github.com/) 中找到。

## 有什么限制？

1 GitHubPages 为每个工程提供的空间大小为 1GB，来搭建个人 Blog 网站绰绰有余。

2 每月访问 GitHubPages 的带宽上限为 100GB。

3 GitHubPages 编译的频率低于每小时10次，完全满足个人  Blog 静态网页的要求。

## 如何使用？

###### 找到 GitHubPages 

GitHubPages 入口从工程设置中可以找到：

![GitHubPages](http://p3gaf3kiq.bkt.clouddn.com/GitPages0.png)

---



![GitHubPages](http://p3gaf3kiq.bkt.clouddn.com/GitPages.png)

---

![GitHub官方推荐Blog框架](http://p3gaf3kiq.bkt.clouddn.com/GitBlog.png)

从 GitHubPages 底部可以看出，官网是推荐使用 [Jekyll框架] （https://jekyllrb.com/docs/quickstart/）来搭建个人Blog，但是 Jekyll 全部都是英文，所以英文不是障碍的友人可以选择，偷懒的我选择了易读的汉化 [hexo框架](https://hexo.io/zh-cn/docs/index.html) 。

相信开发者都拥有自己的 [github](https://github.com/) 账号，没有的也没关系，申请很简单。不要被全英文的网站所吓倒，反复几次过后你会发现——套路都一样。

登录自己的 gitHub 账号，新建工程：

![新建GitHub工程](http://p3gaf3kiq.bkt.clouddn.com/Git%E4%BB%93%E5%BA%93.png)

工程名称有严格的限制，具体命名要求可以在 [官网文档](https://help.github.com/articles/user-organization-and-project-pages/) 找到。

![命名要求](http://p3gaf3kiq.bkt.clouddn.com/Git%E4%BB%93%E5%BA%93%E5%90%8D.png)

###### 安装Hexo

安装步骤可以参照：[hexo安装](https://hexo.io/zh-cn/docs/index.html)

###### 选取使用的主题

[挑选主题](https://hexo.io/themes/) ，不同的主题，安装方式不同，我选择的是 [BlueLake](https://github.com/chaooo/hexo-theme-BlueLake) 。具体安装方式可以在各主题的 github 中看到。推荐排名靠前的主题样式，因为它们不仅意味着符合大众的审美，而且往往 github 上面的步骤写的够详细。相信一句话：「群众的眼光是雪亮的」。

###### 配置域名

首先在新建的 `username.github.io` 工程下新建名称为`CNAME`的文件，添加自己要绑定的域名，我填写的如下：

![CNAME命名](http://p3gaf3kiq.bkt.clouddn.com/%E6%B7%BB%E5%8A%A0CNAME0.png)

![CNAME命名](http://p3gaf3kiq.bkt.clouddn.com/%E6%B7%BB%E5%8A%A0CNAME.png)

域名可以在国内的服务商处购买，我在[阿里云](https://www.aliyun.com/)购买的`.top` 域名，售价 2¥ 大洋。各服务商解析方式都差不多，下面以阿里云上的域名解析为例：

![解析域名](http://p3gaf3kiq.bkt.clouddn.com/%E8%A7%A3%E6%9E%90%E5%9F%9F%E5%90%8D.png)

添加 www 和不带 www 的两个解析地址。其中带 www 的域名解析到不带 www 的地址，不带 www 的域名解析到 `username.github.io`。这样可以让从两个地址的访问记录统一到我们的 github 上面的地址，有利于提高网站在 Google 和 Baidu 的排名。

一切顺利的话，输入购买的域名，就能看到自己的 Blog 网站啦，快给自己点个赞吧。

###### 发表新文章

访问依据 GitHub 搭建的 Blog 网站文章，实际是一个静态网页。该网页可以依据 MarkDown 创建，资源文件创建的位置的形式我们可以参照主题下已经创建好的 hello 文件。比如我选择主题的 hello 文章，放在 `根目录/source/_posts/` 下，以 .md 结尾。因此我只要在改目录下，`ctrl + d` 复制 hello.md ，然后修改下标题就 OK 了。

###### 不可缺少的能力

一篇排版漂亮的文章，少不了标题、插图。所以要求我们需要掌握以下两种技能：

1 [ MarkDown 语法](http://wowubuntu.com/markdown/#em) 。

2 图片存放到云上。

如果将配图放在我们本身网站中，有两个缺点，一是会造成网页空间迅速增大，别忘了空间上限为1GB; 二是引用和管理很不方便，因为没有工具。所以我们可以把图片全部放到云上面，以外部链接的方式在文章中引用。

比较好用的并且带有外链生成功能的厂家，推荐[七牛云](https://portal.qiniu.com/) 。温馨提示：需要身份认证。

写好文字，配好图片，加上适当的排版美化，一篇热气腾腾、洋溢着成就感的文章就完成了。使用如下命令部署服务器上：

```
hexo g -d
```

然后使用 Git 命令提交到远程仓库。

不熟悉 hexo 命令的小伙伴，可以在终端使用 `hexo help` 能够获得如下对 hexo 命令参数的详细解释：

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

这种学习方法对所有的终端命令都有效，包括 Git 在内。记住——这个武林绝招只传男，不传女。不然怎么能体现咱们程序猿们的一阵噼里啪啦的高深莫测？

步骤比较繁琐，但是顺利做完，我们对网站搭建已经有了整体认识。Blog 只是一个简单的网站，我们日常的网站设计到页面的  UI 设计 MM, 处理逻辑的前端程序猿，后台的数据处理，提供各种服务等，每一个步骤都有专业的人去处理，需要大家共同完成，通过搭建 Blog 认识到这些，相信以后与别人的配合能更顺利！