---
title: Blog搭建碰壁记
description: 顺便夹带一些搭建网站的小回忆
date: 2026-10-04 15:47:25+0800
categories: 
    - 折腾
tags: 
    - Blog
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---
最近逐渐开始接触实际生产环境和许多先前在日常玩乐中接触不到的内容，也开始遇到越来越多需要靠自己研究而不是照搬现有教程/文章的经历，于是搭建一个简单的blog的想法慢慢地萌生了，刚好趁着国庆假期有一些闲暇时间，就找了个机会搭了这么个小站出来，现在其实也还在慢慢优化调整，不过已经能够工作了。刚好，就在这里记录一下自己搭建遇到的各种各样问题，留存以便后面可能需要的迁移/调整操作（？）。

## 追忆：最初的最初

其实印象里很早就尝试过Blog/个人站搭建，在孩童时期最早开始接触到的可以称得上"编程"的内容也是HTML/CSS/JavaScript，说来惭愧，只是简单摸了摸勉强算是入了个门就跑去玩别的各式各样的内容了。  
印象里的玩乐其实分了几个阶段：  

### 第一阶段：本地搭着玩

照着远古教材和自己的远古Windows XP电脑配置了半个小时的`IIS5.1`，然后成功点了一个index.html，然后...就没有然后了，这玩意就被弃置了:)

### 第二阶段：初试内网穿透

再然后嘛，就是喜闻乐见的——网课时代！于是重新开始折腾，那段时间玩了特别多特别多乱七八糟的东西，包括但不限于Linux启蒙，第一次摸ARM开发板(Orange Pi Zero)，开始对网络协议和网络层级有认识......这一大堆后面慢慢在这个站里补踩坑记录（逃）。  

也是那段时间接触到了某神秘蓝色软件（不是Telegram），并跟着网上翻到的各类教程最终摸到了[这么一个项目](https://github.com/open-dingtalk/pierced)（我都没想到还能找到Github链接）。那个时候钉钉提供的这个内网穿透开发工具是直接拉HTTP协议的，通过一个frpc魔改版（ding.exe）和极其简单的配置文件（ding.cfg）配置二级域名，配好二级域名后在cmd里启动程序，观察输出日志有无报错提示，若有即为二级域名已被占用，需要更换。  

印象里玩这套工具持续了相当长一段时间，甚至借此给一台仅有GPRS/GSM通讯、无USB和WLAN功能的诺基亚手机传入了一个小游戏（[J2ME](https://en.wikipedia.org/wiki/Java_Platform,_Micro_Edition)，时代的眼泪ww），但是很可惜，经过这么多年的变迁，当时的内容已经完全找不到了，也没能留下什么图片/视频记录。

### 第三阶段：静态网页托管

依然是网课时代...不得不说网课时代真的为我提供了很好的机会进入这个世界（笑），从Bilibili上看到了[青柠起始页](https://intro.limestart.cn/)的介绍视频，于是开始尝试使用，后续青柠起始页并入[热铁盒软件](https://www.retiehe.com/)的账号体系，于是顺势注册了一个热铁盒账号。某天无意浏览的时候发现他们提供了网页托管服务，于是跃跃欲试建了一个小站，随手写了一些很粗糙、特别丑的页面，印象里花了不到半天的时间，后面由于几经更换上游域名，也忘记这件事了。  

但是很神奇，刚才写这篇Blog的时候，回去尝试登录了一下账号，发现那个简陋到爆的网站还在那里：[一言-BillZH](https://baiyang223.rth1.xyz/)。  

点进这个旧网站的时候，看着这一大坨丑到爆的画面，我的第一反应是：当时为什么没用AI？  
然后反应过来——*那个时候，我们还没有LLM。*

## 初识：github.io还是Cloudflare？

回到正题。这次想要真正搭建一个Blog的想法其实从3月就有相关计划了，但是由于各种各样的原因（主要是懒）就没有做起来。最初的想法是利用家里的光猫改桥接+软路由最小化配置DDNS via IPv6实现（当时甚至已经找好了[dynv6](https://dynv6.com/)，想好了建站计划），最后放弃是因为...改桥接之后网络测速有明显限速，排除了硬件问题和基础配置问题，查询相关资料得知**广东地区部分移动家用宽带存在改桥接后上游限速**行为([帖子原文](https://www.right.com.cn/forum/thread-8374526-1-1.html))，也可能是软路由层面出现了一些其他未预料的问题，尝试解决了一段时间，无果，于是只好作罢。  

其实前一两年的时间里也尝试过了解这方面的各种方案，包括但不限于Cloudflare转发/托管域名，亦或现在正在使用的GitHub Pages，但是一直没有真正开始做这类项目。  
这次下定决心拉起来，其实主要是因为github.io方向的方案确实很简便，而且Hugo-Stack主题还有相关的[一键配置模板](https://github.com/CaiJimmy/hugo-theme-stack-starter)，基本可以说是轮椅级别的入门方式了，那还说啥了，创建，配置，启动！  

至于cloudflare，个人想法是留待后续配置真正意义上的个人站/购买域名之后再尝试？前路漫漫嘛...

## 开始折腾：其实真的很轮椅

最开始做了很多无用功，想了想还是得先在这里写一下：

- 如果使用Stack主题的配置模板，**不需要**本地部署Hugo-Extended，配置完成后可以直接VSCode打开codespace进行远程GitHub Actions操作；
- 如果想用`[username].github.io`的GitHub Pages，利用模板就需要删库重建，不能直接fork现有配置；
- Codespace的初始化可能存在问题，在构建时会报错，我通过修改`.devcontainer/devcontainer.json`中的`features`，删除`dart-sass`行并重建容器解决，此问题可能无法复现，仅供参考。

整套流程其实很快捷，首先访问这个[一键配置模板](https://github.com/CaiJimmy/hugo-theme-stack-starter)，然后跟着里面的`README.md`一步一步完成就行，注意事项嘛...`↑抬头见喜↑`。  

补充一点，个人不太喜欢网页端Codespace配置，因为跑一个网页容器对我的电脑来说压力还是比本地VSCode大一些（也可能是网络问题），总之我改用了本地VSCode方式。步骤如下：  

- 打开VSCode，使用`Ctrl+Shift+X`或者`点击左侧"扩展/Extensions"按钮`跳转到扩展页，搜索`GitHub Codespaces`并安装；
- 等待安装的时候检查自己的仓库配置，如果没有新建Codespace则需要按照教程完成新建，然后可以把浏览器容器挂后台让它自己慢慢跑，如果**遇到右下角进度条完成但是左侧还没有文件列表**的话，就需要先做以下操作，在本地VSCode中检查Creation log，检查**Codespace是否由于前面提到的`features`配置问题DOWN进recovery mode**，如是则需要调整配置后重建；
- 随后回到GitHub配置页，在原有Codespaces页面会新增一个`On current branch`列表，点击右侧展开菜单，选择`Open in Visual Studio Code`即可跳转，这样不需要额外进行配置和登录操作，个人比较喜欢。

基本上，只要跑完这套流程，在本地VSCode的Codespace界面/网页端VSCode看到文件目录，此时就应该能够通过`[username].github.io`看到一个很完备的Template界面，只需要接下来做进一步个性化即可。

## 个性化开始：初识Hugo配置文件

当打开托管链接`[username].github.io`看到那个Template之后，就可以开始在自己的VSCode里对着配置文件大刀阔斧地调整了。首先做以下几步必要的调整（针对个人Blog）：

### `config`部分

#### `config/_default/config.toml`

修改`baseurl`为实际站点网址，`locale`为`zh`（中文）或`en`（英语），`defaultContentLanguage`同理，具体语言支持看[**这里**](https://github.com/CaiJimmy/hugo-theme-stack/tree/master/i18n)，`hasCJKLanguage`视情况而定，剩下的看文内注释即可~  

#### `config/_default/menu.toml`

`[[Social]]`部分框架是左侧栏上的社交媒体按钮，可以视个人情况开关，直接删除或在对应框架元素前使用`#`注释掉。  

#### `config/_default/params.toml`

`[sidebar]`中的emoji项即是左侧栏头像旁的emoji，我的配置注释掉了这行，就可以隐藏这个emoji显示，也可以替换为其他的emoji，默认为`🍥`；  

`[footer]`的`since`为页脚的年份，`customText`是自定义文本，我的站点为`Modified by BillZH`；  

`[dateFormat]`为所有文章的日期显示格式，建议根据[Hugo官方文档-dateFormat](https://gohugo.io/functions/dateformat/)进行配置，同时配置可能会受到语言本地化影响；  

`[article]`中的`readingTime`我站关闭了，整体美观度会有提升；  

`[comments]`可以关闭评论功能，这对于某些纯归档站/像我这样懒得配评论功能的人来说很友好，将`enabled`置为`false`即可.  

其他配置可以参考[Stack官方文档-站点配置](https://stack.cai.im/zh/config/site#%E7%AB%99%E7%82%B9%E8%AE%BE%E7%BD%AE)部分完成，不再赘述。

### `content`部分

这里配置能够在主页看到的几个部分，分别为

- `主页` -> `content/_index.md`
- `归档` -> `content/page/archives/index.md`
- `搜索` -> `content/page/search/index.md`
- `友链` -> `content/page/links/index.md`

各文件中均有模板配置，其中

- `title`项即为在主页和标题中看到的文本，默认英文，可自行修改；
- `slug`项定义了该页面在最后静态页面中的最末层级名称，理论上可修改，个人未测试。

其他部分均不建议进行修改。  

### `assets`部分

`assets`部分分为`img`和`scss`两部分，`img`中有`avatar.png`和`favicon.png`两个文件，分别对应左侧栏的头像文件和网站的icon，此处需要注意的是网站icon使用了`png`格式，**并非常见`favicon.ico`类型**。  
`scss`则是自定义scss文件的预留，可以暂时闲置。

### 还需要其他修改？

请参照Stack官方文档的[修改主题](https://stack.cai.im/zh/guide/modify-theme#hugo-%E6%A8%A1%E5%9D%97-hugo-module)部分介绍，一键Template适用于其中`Hugo模块`部分内容，不再赘述。  
修改完成后，可以在`VSCode`的`终端/Terminal`窗口运行`hugo server`进行实时预览，默认网页应该位于`http://localhost:1313/`，直接访问即可。`hugo server`服务属于热更新，打开状态下进行任何页面修改都会直接更新，如果页面没有更新，手动刷新一下即可。

## 搞定了基础配置？开始写帖子吧！

`content/post`目录下目前应该可以看到几个不同的文件夹，分别是默认模板下的几个示例帖子，可以参考这几个帖子开始写自己的帖子了！  
需要注意的是，默认情况下建议使用`content/post/[postname]/index.md`路径进行配置，在`index.md`中需要使用以下模板进行帖子定义：

```Markdown
---
title: [帖子标题]
description: [帖子副标题]
slug: [希望显示在链接栏的名称，默认为标题/文件名]
date: 2026-10-04 13:33:25+0800 # 帖子写作时间
categories: [分类]
tags: [标签]
weight: 1       # 帖子排序权重
---
```

随后即可使用正常Markdown语法在该配置下进行帖子正文书写。  
Hugo支持的Markdown语法还算齐全，由于我也是Markdown小白就不在这里班门弄斧了（继续逃），可以参见[官方文档](https://hugo.opendocs.io/content-management/formats/)。

## 完成配置并编译

完成所有内容之后，可以先通过`hugo server`进行预览，确认没有什么问题之后就可以直接提交。  
在`终端/Terminal`窗口运行以下内容即可：

```shell
git add .
git commit -m "[commit description, remember to change]"
git push
```

随后，GitHub Actions将会自动编译更改并更新，稍等片刻，访问`[用户名].github.io`即可浏览修改后的网站。

## 后记

这是我真正意义上的第一个blog网站，这次blog撰写也是我第一次真正意义上的撰写Markdown语法文档，说实话收获颇丰，也越来越意识到自己还是一个小菜鸡。  
其实也学习到了很多内容，比如...Markdown语法？Hugo配置？顺带看了点Go语言？  
也在写这篇文档的时候开始体会到编写blog的某些乐趣，以及追忆、重拾旧站时一些略奇异的心理体验。  
总之，这就是我的第一个blog了，希望你们能喜欢~

Written by BillZH  
October 4, 2026.
