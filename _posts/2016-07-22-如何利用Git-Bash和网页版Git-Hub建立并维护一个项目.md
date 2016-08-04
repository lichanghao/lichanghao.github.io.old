---
layout:     post
title:      "如何利用gitbash和网页版github建立并维护一个项目"
subtitle:   ""
date:       2016-07-22 11:10:00 +0300
author:     "lichanghao"
header-img: "img/post-sample-image.jpg"
header-mask: 0.3
catalog:    true
tags:
    - git
    - github
    - 基础
---

[github](https://en.wikipedia.org/wiki/GitHub)是一个开源代码库，Github使用git分布式版本控制系统。git最初用作Linux内核代码的管理。目前Github有140万的用户，其中不乏各种技术大牛。可以说，Github就是程序员业内的Facebook。你在这里可以轻易的找到优秀的开源代码，并不用花任何代价地Fork下来，并作出自己的改动，你还可以继续向开源代码的原作者发出Pullrequests，尝试把自己对开源项目作出的改变融合到主版本。总而言之，Github很好很强大。下面我作为一个初学者，向大家介绍一下Github的一些基本操作。（基于windows环境）

### 1.Github是什么
   Github其实是全球最大的同性交友网站。

<figure>
<img src="{{ site.github.url }}/img/Github1.PNG" />
<figcaption>图片源自网络</figcaption>
</figure>

   这只是个玩笑，别当真。其实在上面已经说过了，Github是一个基于git的开源代码库。说白了，这个网站提供代码托管服务，你可以把你的代码放到这个网站中托管，与此同时，如果你是免费用户，你就不得默认你的代码成为一个开源的项目。任何人都可以参与这个项目，只不过一般来说要创建不同的分支（branch）而已。
   
   
#### 最好先了解的几个概念


      0.git。git是一个分布式版本控制系统，用来进行项目版本管理。也就是说，用git可以轻松实现一个项目不同版本之前的回溯和更新。
      1.Repository（仓库）。一个仓库就是一个代码库。你可以自己随意创建仓库。它有点类似于文件夹。
      2.Fork。Fork的意思大概是，将他人的仓库拷贝一份到你的账户中。Fork十分常用。
      3.branch（分支）。一个项目，或者说一个仓库，可能会有多个分支。branch的概念和平行宇宙差不多，你Fork别人的代码以后，自然会创建一个新的branch。
      4.Pull requests。你将别人的Repository，Fork下来以后，可以任意做出自己的改动。如果你想为原作者的代码库做出自己的贡献，你就要向原作者发起Pull requests。如果原作者同意，你修改过的branch将会与原作者的branch合并。想想自己可能为一个巨型开源代码库做出贡献，是不是很酷。
  
 
### 2.注册Github账号

   [github官网](https://github.com/)。所幸的是github目前还没被拒于天朝网络长城之外，但是用大陆ip访问可能会有点慢。进入官网之后按提示一步一步来，很容易就可以注册一个属于自己的github账号，和注册微博或者论坛没什么区别。
   
   注意：最好绑定自己的一个常用邮箱，这样可以收到github发给你的各种通知，很有用。


### 3.我可以用我的账号做什么

1.托管自己的代码

2.fork他人的代码并打补丁，然后pull上去

3.和网站上的其他人交朋友（比如赞一下你喜欢的代码）

4.....
   
   还有一点要提的是，github提供了一个叫githubpages的服务，通过这个服务你可以在五分钟以内建立一个账号独有的网站。例如，我的github账号是[lichanghao](https://github.com/lichanghao)，那么我建立的网站域名就是[https://lichanghao.github.io/](https://lichanghao.github.io/)。通过github pages还有一个叫[jekyll](http://jekyll.bootcss.com/)的工具，就可以超级便捷地实现一个属于自己的个人博客。我的博客就是这么建起来的，现在我还在读jekyll的官方文档，日后研究一段时间我可能会再写一个建博客的教程。


### 4.如何创建一个Repository（仓库）


#### 4.1 在github官网上建立repo

   在网页中点击“New Repository”，跳转到下图所示的页面。
<figure>
<img src="{{ site.github.url }}/img/github2.jpg" />
<figcaption>创建repo</figcaption>
</figure>
   然后填写各种信息。最好勾选"Initialize this repository with a README"选项。填写完毕以后点击create。
<figure>
<img src="{{ site.github.url }}/img/github3.png" />
<figcaption>向repo中添加内容</figcaption>
</figure>
   点击create后跳转到上图所示页面。github给你提供了几种添加内容的方式，其中第二种和第三种需要用git bash，也就是命令行来完成。下面我介绍一下git bash的几个基础用法。
   
#### 4.2 利用git bash向一个空的repo中添加文件   

   首先要安装[git](http://code.google.com/p/msysgit/)，这个链接好像被墙了，有条件的同学可以翻墙下载，或者另行百度其他下载地址。我这里就不负责任的不把其他地址放在这里了，网上应该不难找。
   
   然后要配置git。git的远程代码是基于SSH的，SSH类似于HTTP，是一个网络协议，具体细节我也不太懂，感兴趣的同学可以自行谷歌。
   安装好git以后，右键一个文件夹，菜单中应该多出一个选项“Git Bash Here”。点击它，就打开了Git Bash的命令行窗口，同时路径设置在了该文件夹下。
<figure>
<img src="{{ site.github.url }}/img/github4.png" />
<figcaption>Git Bash 命令行窗口</figcaption>
</figure>
   接下来开始配置git，第一步：设置git的user name和email。在命令行窗口中输入如下代码
   
   
```html

$ git config --global user.name "此处填你的用户名"
$ git config --global user.email "此处填你的邮箱"

```
   
   第二步：生成SSH密钥。

```html
 
$ ssh-keygen -t rsa -C "填你刚才输入的邮箱"
 
```

   输入上述代码以后，窗口会提示你设置密码，如果不需要密码的话，连按三下回车就行了。
   
   
```html  
 
Your identification has been saved in /home/tekkub/.ssh/id_rsa.  
Your public key has been saved in /home/tekkub/.ssh/id_rsa.pub.  
The key fingerprint is:  
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    
```


   上述步骤成功以后命令行窗口会跳出以上的信息。在根目录下得到两个文件：id_rsa和id_rsa.pub。秘钥分两部分，公秘钥和私秘钥。
   
   第三步：添加私有秘钥到SSH。
   
   
```html   
 
$ ssh-add id_rsa
   
```
   
   
   第四步：在github上添加ssh密钥，这要添加的是“id_rsa.pub”里面的公钥。
   
   进入github登录自己的账号，在右上角头像旁边进入“setting”，点击“SSH and GPG keys”。
<figure>
<img src="{{ site.github.url }}/img/github5.png" />
<figcaption> </figcaption>
</figure>
   然后点击SSH右上角的“new SSH key”。
<figure>
<img src="{{ site.github.url }}/img/github6.png" />
<figcaption> </figcaption>
</figure>

   然后用记事本打开文件id_rsa.pub，把里面的所有信息复制到key下面的文本框中，点击“add SSH key”。

   第五步：测试成功与否
   
   
```html   
 
$ ssh git@github.com
   
```
 
 
   如果有成功信息，那么就完成了。
   
   
### 5.向Repository中添加代码

   用github网站，登录自己的账号，进入你想编辑的Repo中的某个目录，就直接可以编辑文件然后commit，很简单。

### 6.如何将托管在Github上的Repository克隆（clone）到本地

   
```html   
 
$ git clone git@github.com:username/reponame.git //username处是你的用户名，reponame处是你想要clone到本地的repo名字
   
```
成功后，repo就会被clone到你所在的根目录。


### 7.如何将本地的Repository上传到远程服务器


```html

$ git init   //初始化Repo。保证你所在的目录是Repo的根目录，如果不是，请用cd命令找到repo的根目录
$ git add .  //把所有文件变为add状态
$ git commit -m “此处填你的备注”  //把上述文件变为commit状态 
$ git push   //上传到远程服务器。如果你有本地的密码，会提示让你输入密码。

```
还有一个pull命令，跟push相反，是把远程服务器上的repo同步到本地。

```html

$ git pull   

```

到这里就结束了，由于我自己也是个初学者，肯定有许多技术细节我没介绍到，也有可能会有一些错误。自己写了才知道，一篇深入浅出的博客教程，可不是那么容易就能写出来的！如果你想学习更多有关git的知识，请参考下面的链接：

[廖雪峰git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)

[git常用命令](http://justcoding.iteye.com/blog/1830388)





