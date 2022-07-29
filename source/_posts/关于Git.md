---
title: 关于Git
description: 手收集一些关于Git的入门知识和使用技巧，还有关于开源的东西
categories: 编程
tags:
  - Git
  - 写作
abbrlink: 30151
header: ''
banner_img: /post_img/76044364_p0_master1200.jpg
index_img: /post_img/76044364_p0_master1200.jpg
---

## Git简介

### Git是什么

### 为什么要有Git

### 我必须要用Git吗

### Git的安装与配置

## Github、Gitee和GitLab

## 使用Git

### 基本操作

### merge和rebase

### 冷门命令

#### stash[^3]

## 开源许可证

### 什么是开源许可证

世界上的开源许可证（Open Source License）大概有上百种，大致有GPL、BSD、MIT、Mozilla、Apache和LGPL等#

#### 简单分类

大致分为两大类：**宽松自由软件许可协议（“Permissive free software licence”）和著佐权许可证（“copyleft license”）**。

> Permissive free software licence 是一种对软件的使用、修改、传播等方式采用**最低限制的自由软件许可协议条款类型**。这种类型的软件许可协议将不保证原作品的派生作品会继续保持与原作品完全相同的相关限制条件，从而为原作品的自由使用、修改和传播等提供更大的空间。
>
> 而 Copyleft License 是在有限空间内的自由使用、修改和传播，且不得违背原作品的限制条款。如果一款软件使用 Copyleft 类型许可协议规定软件**不得用于商业目的，且不得闭源，**那么后续的衍生子软件也必须得遵循该条款。

**两者最大的差别在于**，在软件被修改并再发行时， Copyleft License 仍然强制要求公开源代码（衍生软件需要开源），而 Permissive free software licence 不要求公开源代码（衍生软件可以变为专有软件）。

> 其中，Apache、MIT、BSD 都是宽松许可证，GPL 是典型的强著佐权（copyleft ）许可证，LGPL、MPL 是弱著佐权（copyleft ）许可证。SSPL 则是近年来 MongoDB 创建的一个新许可证，存在较大争议，开放源代码促进会 OSI 甚至认为 SSPL 就不是开源许可协议。

此外，还有一类是 Creative Commons（CC）知识共享协议。严格意义上说该协议并不能说是真正的开源协议，它们大多是被使用于设计类的工程上。

> CC 协议种类繁多，每一种都授权特定的权利。大多数的比较严格的 CC 协议会声明 “署名权，非商业用途，禁止衍生” 条款，这意味着你可以自由的分享这个作品，但你不能改变它和对其收费，而且必须声明作品的归属。这个许可协议非常的有用，它可以让你的作品传播出去，但又可以对作品的使用保留部分或完全的控制。最少限制的 CC 协议类型当属 “署名” 协议，这意味着只要人们能维护你的名誉，他们对你的作品怎么使用都行。

![协议列表.webp](https://img1.www.pingcap.com/prod/_8670ba8cf1.webp)

#### 开源与开源许可证的历史

开源这个词最初其实是指开源软件（OSS）。开源软件是源代码可以任意获取的计算机软件，任何人都能查看、修改和分发他们认为合适的代码。

**在开源领域中，存在着两大阵营**：FSF（Free Software Foundation，自由软件基金会) 和 OSI（Open Source Initiative，开放源代码促进会），**他们对开源有着不同的理念**。

> FSF 是开源泰斗 RMS 创立的重要的开源软件基金会 (1985/10/04), FSF 创立之初主要是为了筹集资金来建设 GNU 的内核 Hurd 项目及工具链，虽然 GNU 项目本身没有完成，但是该过程中创造出的大量软件工具，日后成为了 GNU/Linux 的重要组成部分。为了**贯彻 RMS 对 “自由” 和 “开源” 的理解**，FSF 建立了开源领域的第一个 “copyleft” 属性的许可证 - GPL (GNU Public License) 。
>
> OSI 由开源界泰斗 Bruce Perens 和 Eric S. Raymond (ESR) 在 1998 年组建，目的是在原教旨主义开源 (最早的开源运动发起和推动者们) 与软件工业/商业之间激烈矛盾中，寻求**更平衡的体系和治理机制**。OSI 组织批准过的许可大概有 80 种，包括 Apache License v2、GPL v2、MIT/BSD 等。

FSF 与 OSI 是推广和维护开源秩序的非盈利组织，维护着 “开源” 的定义以及主要的开源软件协议递交、讨论与审核。只要条款被审核通过是符合开放源代码定义的，就可以称之为开放源码授权条款，采用开放源码条款散布授权的软件即是开放源码软件，若一份商业产品中包含有开放源码软件，其包装上可以标上开放源码促进会的证明标章，认识这个标章的消费者就可以知道产品中有使用到开放源码软件，进而因为开放源码软件特有的优点而购买产品。

![开源标识.webp](https://img1.www.pingcap.com/prod/_e1f8e1d3bd.webp)

### 常见开源许可证

#### Apache License

Apache License（Apache许可证），是Apache软件基金会发布的一个自由软件许可证。

Apache License 最初为 Apache http 服务器而撰写。此许可证最新版本为 “版本 2”，于 2004 年 1 月发布。**Apache 许可证鼓励代码共享和最终原作者的著作权，允许源代码修改和再发布**。

Apache Licence是著名的非盈利开源组织Apache采用的协议。该协议和BSD类似，同样鼓励代码共享和最终原作者的著作权，同样允许源代码修改和再发布。

> 例如，在一个使用 Apache 许可证的开源项目中，其下游 Fork 的企业不仅没有回馈上游开源项目，反而将衍生的代码更改为不受 OSI 认可的 SSPL Licence，另行宣布成为一个新的开源项目，误导了很多不明真相的人，以为又涌现出一个新的开源项目。但该行为其实已经对原开源项目的合法权益造成了侵害，也有背开源精神。

但是也需要遵循以下条件：

- 需要给**代码的用户**一份Apache Licence。
- 如果修改了代码，需要在被修改的文件中说明。
- 在**衍生的代码中（修改和有源代码衍生的代码中）需要带有原来代码中的协议，商标，专利声明和其他原来作者规定需要包含的说明**。
- 如果再发布的产品中包含一个Notice文件，则在Notice文件中需要带有Apache Licence。你可以再Notice中增加自己的许可，但是不可以表现为对Apache Licence构成更改。
- Apache Licence也是**对商业应用友好**的许可。使用者也可以再需要的时候修改代码来满足并作为开源或商业产品发布/销售。

它有这些好处

- 永久权利 一旦被授权，永久拥有。
- 全球范围的权利 在一个国家获得授权，适用于所有国家。假如你在美国，许可是从印度授权的，也没有问题。
- 授权免费 无版税， 前期、后期均无任何费用。
- 授权无排他性 任何人都可以获得授权
- 授权不可撤消 一旦获得授权，没有任何人可以取消。比如，你基于该产品代码开发了衍生产品，你不用担心会在某一天被禁止使用该代码

#### BSD

BSD是"Berkeley Software Distribution"的缩写，意思是"伯克利软件发行版"。

BSD开源协议是一个给于使用者很大自由的协议。可以**自由的使用，修改源代码，也可以将修改后的代码作为开源或者专有软件再发布**。

BSD代码鼓励代码共享，但需要尊重代码作者的著作权。BSD由于允许使用者修改和重新发布代码，也允许使用或在BSD代码上开发商业软件发布和销售，因此是对商业集成很友好的协议。而很多的**公司企业在选用开源产品的时候都首选BSD协议**，因为可以完全控制这些第三方的代码，在必要的时候可以修改或者二次开发。

当你发布使用了BSD协议的代码，或则以BSD协议代码为基础做二次开发自己的产品时，需要满足三个条件：

- 如果再发布的产品中包含源代码，则在源代码中必须带有原来代码中的BSD协议。
- 如果再发布的只是二进制类库/软件，则需要在类库/软件的文档和版权声明中包含原来代码中的BSD协议。
- **不可以用开源代码的作者/机构名字和原来产品的名字做市场推广**。

#### GPL

GPL （GNU General Public License） ：GNU通用公共许可协议。**Linux 采用了 GPL**。

GPL协议和BSD, Apache Licence等鼓励代码重用的许可很不一样。GPL的出发点是代码的开源/免费使用和引用/修改/衍生代码的开源/免费使用，但**不允许修改后和衍生的代码做为闭源的商业软件发布和销售**。这也就是为什么我们能用免费的各种linux，包括商业公司的linux和linux上各种各样的由个人，组织，以及商业软件公司开发的免费软件了

#### LGPL

LGPL是GPL的一个为主要为类库使用设计的开源协议。和GPL要求任何使用/修改/衍生之GPL类库的的软件必须采用GPL协议不同。LGPL允许商业软件通过类库引用(link)方式使用LGPL类库而不需要开源商业软件的代码。这使得采用LGPL协议的开源代码可以被商业软件作为类库引用并发布和销售。

但是如果修改LGPL协议的代码或者衍生，则所有修改的代码，涉及修改部分的额外代码和衍生的代码都必须采用LGPL协议。因此LGPL协议的开源代码很适合作为第三方类库被商业软件引用，但不适合希望以LGPL协议代码为基础，通过修改和衍生的方式做二次开发的商业软件采用。

GPL/LGPL都保障原作者的知识产权，避免有人利用开源代码复制并开发类似的产品。

#### MIT

MIT是和BSD一样宽范的许可协议,源自麻省理工学院（Massachusetts Institute of Technology, MIT），又称X11协议。

**作者只想保留版权,而无任何其他限制**。MIT与BSD类似，但是比BSD协议更加宽松，是**目前最少限制的协议**。

这个协议唯一的条件就是在修改后的代码或者发行包包含原作者的许可信息。适用商业软件。

使用MIT的软件项目有：jquery、Node.js。

有许多团体均采用 MIT 许可证。例如著名的 ssh 连接软件 PuTTY 与 X Window System (X11) 即为例子。Expat 、Mono 开发平台库、Ruby on Rails、 Lua 5.0 onwards 等等也都采用 MIT 授权条款。

### 如何选择开源许可证

一些思维导图

![img](https://pic1.zhimg.com/80/v2-bc54a5e176e1ff9d75dda56da5472366_1440w.jpg?source=1940ef5c)

> 从左到右越来越严格

![img](https://www.runoob.com/wp-content/uploads/2018/03/61590003177751b9d5bd.jpg)

![img](https://www.runoob.com/wp-content/uploads/2018/03/f1989e42b25bb73fead5cb1d09036e6f.png)

## 仓库规范

## 参考资料

[^1]: (https://www.runoob.com/w3cnote/open-source-license.html)
[^2]: (https://pingcap.com/zh/blog/introduction-of-open-source-license)
[^3]: [Git 不能只会 pull 和 push，试试这5条提高效率的命令吧！](https://mp.weixin.qq.com/s/vCcmCWhNsDdQXJQwT6AZOQ)
[^4]: [Commit message 和 Change log 编写指南 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
