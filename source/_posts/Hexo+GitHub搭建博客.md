---
title: "Hexo+GitHub搭建博客"
comments: true
mathjax: true
share: true
toc: true
categories:
  - Hexo
tags:
  - Hexo
  - GitHub
---
----------

- **转载请注明作者和出处：**[https://adolphmaster.github.io](https://adolphmaster.github.io/)
- **文章地址：**[https://adolphmaster.github.io/2019/07/07/Hexo+GitHub搭建博客/](https://adolphmaster.github.io/2019/07/07/Hexo+GitHub搭建博客/)
- **编&emsp;&emsp;者：adolphMaster**

----------
[TOC]

# Hexo+GitHub搭建博客

> 在参照众多大神在网络上的文章之后，自己终于弄出个东西来了，对于我这种爱折腾的人来说，将这各过程写下来，将来绝对用得到，如果还能帮助哪位同道中人，那实在是意外之喜，值得浮一大白！

## ① 前期准备

> 前期准备就不介绍了，这个随便搜，不会有出错的

* GitHub账号以及账号名.github.io的项目

  > 例如，我的就是[adolphmaster.github.io](https://github.com/adolphmaster/adolphmaster.github.io)，这个也是将来我们访问页面的url，一定是账号名，选择Public，勾上初始化README文件选项，借用某位大神的图片，如下：

  ![借用某位大神的图片](https://img-blog.csdn.net/20160415123510901)

* 安装Git

* 安装node.js

## ②绑定GitHub

首先，我们需要给github添加SSH key，分两个步骤：生成SSH key和添加key到Github Pagesa.

生成SSH key：

```shell
打开Git Bash,在命令行中输入，输入完第一次输入文件名，之后几次等待输入可以直接按回车：
ssh-keygen -t rsa -C "youremail@example.com"
```
> 其中这里双引号中填写的就是自己的邮箱地址，回车之后需要你输入文件名称已经密码，借用某位大神的图片：

![借用某位大神的图片](https://img-blog.csdn.net/20160413195524856?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

经过以上的操作之后，在用户目录里会自动生成一个.ssh文件夹，下面会生成两个文件：ssh_key和ssh_key.pub，这两个分别是SSH key的私钥（不可泄露出去）和公钥（可以放心告诉任何人）。

```shell
    我们可以用vim命令来查看公钥文件内容,借用某位大神的图片：
    vim ssh_key.pub
```

![借用某位大神的图片](https://img-blog.csdn.net/20160413204824019)
        

可以看到公钥的ssh key是刚刚设定的邮箱地址作为后缀的，复制这段key，然后准备执行下一步。

添加key到Github Pages：用我们最开始注册的GitHub账号登陆GitHub主页面，点击右上角账号管理中的Setting选项,借用某位大神的图片：

![借用某位大神的图片](https://img-blog.csdn.net/20160413205103837)

进入到设置栏之后，选中SSH and GPG keys选项，然后向SSH keys栏中添加一个新的SSH key，借用某位大神的图片：

![借用某位大神的图片](https://img-blog.csdn.net/20160413205418811)Title可以自己任意定义，把刚刚复制的ssh_key.pub中的key复制到此处填写key内容的空白处，点击添加，借用某位大神的图片：

![](https://img-blog.csdn.net/20160413205611485)

添加完成后，可以看到SSH keys栏中多出了一个key，至此我们就完成了SSH key的生成和添加，借用某位大神的图片：

![https://img-blog.csdn.net/20160413205554344](https://img-blog.csdn.net/20160413205554344)

接下来我们通过msysgit测试一下连接：
```shell
ssh -T git@github.com  
```

出现最后一句话或者类似成功的信息标志着SSH key添加成功，借用某位大神的图片:

![https://img-blog.csdn.net/20160413210533341](https://img-blog.csdn.net/20160413210533341)

> 这里报错的话，就回到 / 目录(跟目录，即cd / 回车)输入 ssh-add ssh_key，ssh_key为输入的密钥的文件名，  
>
> 如果还系统提示：could not open a connection to your authentication agent
>
> 则需要执行一下命令：ssh-agent bash  
>
> 再输入ssh-add ssh_key

```shell
中途可能要设置全局配置user.name 和user.email   （–-global有可能要去掉，因为我加上报错，去掉了就ok）
git config –-global user.name “adolphmaster”  //(“”的账号是刚才Github里面自己注册的账号) 
git config –-global user.email “adolphmaster@163.com” //(""的邮箱是你自己注册的邮箱)

```



## ③ 搭建Hexo

```shell
全局配置设置到淘宝源：
npm config set registry https://registry.npm.taobao.org
```

### 安装hexo插件

```shell
输入以下代码,借用某位大神图片：
  cd / #进入根目录，实际上是git安装的根目录 
  pwd /
  npm install hexo-cli -g
```

![借用某位大神图片](https://img-blog.csdn.net/20180515115328728?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTg3OTE3OA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

```shell
安装之后，输入以下代码：
cd / 
hexo init Hexo 
cd /Hexo 
npm instal 
hexo generate（可简写为hexo g ， 类似编译） 
hexo sever（可简写为hexo s， 类似运行）
这时访问http://localhost:4000，应该就能看到东西了

查看hexo插件的版本
hexo -V
大于hexo 3.0的上传到github的方法： 
安装部署到github插件依赖
npm install –save hexo-deployer-git
```

添加上传信息，借用某大神图片：

![](https://img-blog.csdn.net/20180515151502825)

![](https://img-blog.csdn.net/2018051512195954)

```shell
deploy: 
type: git 
repo: https://github.com/adolphmaster/adolphmaster.github.io  //（改成自己的） 
branch: master
```

再将gitbash部署hexo到github

```shell
hexo deploy
```

### 设置自己博客的功能(Next主题设置)

#### [开始使用next主题](http://theme-next.iissnan.com/getting-started.html)

> * 下载主题
>
> * 启用主题
>
> * 选择Scheme
>
> * 设置语言
> * 设置菜单
> * ······





* [参考：Github+Jekyll —— 创建个人免费博客（三）Git学习](https://blog.csdn.net/linshuhe1/article/details/51146184)

* [参考：如何建立linux ssh信任的方法与常见问题](https://zhidao.baidu.com/question/712206549106448205.html)

* [参考：2018.5月使用Github+Hexo搭建自己的博客](https://blog.csdn.net/weixin_39879178/article/details/80319392)