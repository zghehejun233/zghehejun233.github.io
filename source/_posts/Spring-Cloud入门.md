---
title: Spring Cloud入门
description: 记录一下平时看到的关于SpringCloud的内容
categories: 开发
tags:
  - Java
  - Spring
  - Spring Cloud
abbrlink: 42360
banner_img: /post_img/29671098_p0.jpg
index_img: /post_img/29671098_p0.jpg
date: 2022-04-06 12:39:00
---

## 简述

### 分布式和微服务概述

> 参考资料
>
> <https://cloud.google.com/learn/what-is-microservices-architecture?hl=zh-cn>
>
> <https://www.zhihu.com/question/28253777>

不论是商业应用还是用户应用，在业务初期都很简单，我们通常会把它实现为单体结构的应用。但是，随着业务逐渐发展，产品思想会变得越来越复杂，单体结构的应用也会越来越复杂。这就会给应用带来如下的几个问题：

- 代码结构混乱：业务复杂，导致代码量很大，管理会越来越困难。同时，这也会给业务的快速迭代带来巨大挑战；
- 开发效率变低：开发人员同时开发一套代码，很难避免代码冲突。开发过程会伴随着不断解决冲突的过程，这会严重的影响开发效率；
- 排查解决问题成本高：线上业务发现 bug，修复 bug 的过程可能很简单。但是，由于只有一套代码，需要重新编译、打包、上线，成本很高。

由于单体结构的应用随着系统复杂度的增高，会暴露出各种各样的问题。近些年来，**微服务架构**逐渐取代了单体架构，且这种趋势将会越来越流行。

Spring Cloud是目前最常用的微服务开发框架，已经在企业级开发中大量的应用。

> 微服务架构（通常简称为微服务）是指开发应用所用的一种架构形式。通过微服务，可将大型应用分解成多个独立的组件，其中每个组件都有各自的责任领域。在处理一个用户请求时，基于微服务的应用可能会调用许多内部微服务来共同生成其响应。

[容器](https://cloud.google.com/containers?hl=zh-cn)是微服务架构的绝佳示例，因为它们可让您专注于开发服务，而无需担心依赖项。现代云原生应用通常使用容器构建为微服务。

通常，微服务可用于加快应用开发速度。使用 Java 构建的微服务架构非常常见，尤其是 Spring Boot 架构。比较微服务与面向服务的架构也很常见。它们具有相同的目标，即将单体式应用分解为更小的组件，但这些架构所用的具体方法素有不同。

Google Cloud给出了一些微服务的示例，如

- 网站迁移：托管在单体式平台上的复杂网站可以迁移到云端和基于容器的微服务平台。

- 媒体内容：通过使用微服务架构，图片和视频资源可以存储在可扩缩的对象存储系统中，并直接提供给网站或移动设备。

- 交易信息和帐单：付款处理和订单可分离开来，各自作为独立的服务单元，这样即便帐单服务无法正常工作，也能正常接收付款。

- 数据处理：微服务平台可以扩展对现有模块化数据处理服务的云端支持。

从概念理解，**[分布式服务架构](https://www.zhihu.com/search?q=分布式服务架构&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A551785648})强调的是服务化以及服务的分散化，微服务则更强调服务的专业化和精细分工**；从实践的角度来看，**微服务架构通常是分布式服务架构**，反之则未必成立。所以，**选择微服务通常意味着需要解决分布式架构的各种难题。**

这里同时给出对于几个相关名词的解释

| 技术                          | 实现方式                                                     | 作用                             |
| ----------------------------- | ------------------------------------------------------------ | -------------------------------- |
| 分布式                        | 不同模块部署在不同服务器上                                   | 分布式解决网站高并发带来的问题   |
| 集群                          | 相同服务部署在不同服务器上                                   | 通过负载均衡设备共同对外提供服务 |
| SOA(组装服务/ESB企业服务总线) | 业务系统分解为多个组件，让每个组件独立提供离散、自治、可复用的服务能力，通过服务的编排和组合来实现上层的业务流程 | 简化维护，降低整体风险，伸缩灵活 |
| 微服务                        | 各服务间隔离（分布式也是），自治（分布式要相互组合），具有单一职责、边界、异步通信和独立部署等特性 | 各服务可独立应用                 |

### 微服务相关技术

微服务架构的定义：微服务架构是一种应用架构类型，其中应用会开发为一系列服务。它提供了独立开发、部署和维护微服务架构图和服务的框架。

> 在微服务架构中，每个微服务都是独立的服务，旨在容纳一种应用特性并处理离散的任务。每个微服务都通过简单的接口与其他服务通信，以解决业务问题。

以下给出一个表格

| 微服务条目          | 落地技术                             | 作用 |
| ------------------- | ------------------------------------ | ---- |
| 服务开发            | SpringBoot、Spring和SpringMVC        |      |
| 服务配置与管理      | Archaius（Netflix），Diamond（阿里） |      |
| 服务注册与发现      | Eureka、Consul、Zookeeper            |      |
| 服务调用            | Rest、RPC、gRPC                      |      |
| 服务熔断器          | Hystrix、Envoy                       |      |
| 负载均衡            | Ribbon、Nginx                        |      |
| 服务接口调用        | Feign                                |      |
| 消息队列            | Kafaka、RabbitMQ、ActiveMQ           |      |
| 服务配置中心管理    | SpringCloudConfig、Chef              |      |
| 服务路由（API网关） | Zuul                                 |      |
| 服务监控            | Zabbix、Nagios、Metrics、Spectator   |      |
| 全链路追踪          | Zipkin、Brave、Dapper                |      |
| 服务部署            | Docker、OpenStack、Kuberetes         |      |
| 数据操作开发包      | SpringCloud Stream                   |      |
| 事件消息总线        | SpringCloudBus                       |      |

## SpringCloud简介

> 参考资料
>
> <https://blog.51cto.com/lovebetterworld/2853431>
>
> <https://blog.csdn.net/ThinkWon/article/details/103715146>

Spring Cloud是**一系列框架的有序集合**。

它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、智能路由、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。

Spring Cloud并没有重复制造轮子，它只是将各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过Spring Boot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包。

> Spring Cloud对于中小型互联网公司来说是一种福音，因为这类公司往往没有实力或者没有足够的资金投入去开发自己的分布式系统基础设施，使用Spring Cloud一站式解决方案能在从容应对业务发展的同时大大减少开发成本。同时，随着近几年微服务架构和Docker容器概念的火爆，也会让Spring Cloud在未来越来越“云”化的软件开发风格中立有一席之地，尤其是在五花八门的分布式解决方案中提供了标准化的、全站式的技术方案，意义可能会堪比当年Servlet规范的诞生，有效推进服务端软件系统技术水平的进步

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226143921760.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly90aGlua3dvbi5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

SpringCloud 和SpringBoot有密切的关系

- Spring Boot 是 Spring 的一套快速配置脚手架，可以基于Spring Boot 快速开发**单个微服务**，Spring Cloud是一个基于Spring Boot实现的云应用开发工具。Spring -> Spring Boot > Spring Cloud 这样的关系。
- Spring Boot可以离开Spring Cloud独立使用开发项目，但是Spring Cloud离不开Spring Boot，属于依赖的关系
- Spring Boot专注于快速、方便集成的单个个体微服务，Spring Cloud是关注全局的服务治理框架
- Spring Boot使用了默认大于配置的理念，很多集成方案已经帮你选择好了，能不配置就不配置，Spring Cloud很大的一部分是基于Spring Boot来实现

### SpringCloud版本和组件

Spring Cloud是一个由许多子项目组成的综合项目，各子项目有不同的发布节奏。

 为了管理Spring Cloud与各子项目的版本依赖关系，发布了一个清单，其中包括了某个Spring Cloud版本对应的子项目版本。

为了避免Spring Cloud版本号与子项目版本号混淆，Spring Cloud版本采用了名称而非版本号的命名，这些版本的名字采用了伦敦地铁站的名字，根据字母表的顺序来对应版本时间顺序，例如Angel是第一个版本，Brixton是第二个版本。

当Spring Cloud的发布内容积累到临界点或者一个重大BUG被解决后，会发布一个"service releases"版本，简称SRX版本，比如Greenwich.SR2就是Spring Cloud发布的Greenwich版本的第2个SRX版本。目前Spring Cloud的最新版本是Hoxton。

Spring Cloud的子项目，大致可分成两类，一类是对现有成熟框架"Spring Boot化"的封装和抽象，也是数量最多的项目；第二类是开发了一部分分布式系统的基础设施的实现，如Spring Cloud Stream扮演的就是kafka, ActiveMQ这样的角色。

### Spring Cloud Config

集中配置管理工具，分布式系统中统一的外部配置管理，默认使用Git来存储配置，可以支持客户端配置的刷新及加密、解密操作。

### Spring Cloud Netflix

Netflix OSS 开源组件集成，包括Eureka、Hystrix、Ribbon、Feign、Zuul等核心组件

- Eureka：服务治理组件，包括服务端的**注册中心**和客户端的**服务发现机制**；
- Ribbon：**负载均衡**的服务调用组件，具有多种负载均衡调用策略；
- Hystrix：**服务容错**组件，实现了断路器模式，为依赖服务的出错和延迟提供了容错能力；
- Feign：基于Ribbon和Hystrix的**声明式服务调用**组件；
- Zuul：**API网关组件**，对请求提供路由及过滤功能。

### Spring Cloud Bus

用于传播集群状态变化的消息总线，使用轻量级消息代理链接分布式系统中的节点，可以用来动态刷新集群中的服务配置。

### Spring Cloud Consul

基于Hashicorp Consul的服务治理组件。

### Spring Cloud Security

安全工具包，对Zuul代理中的负载均衡OAuth2客户端及登录认证进行支持

### Spring Cloud Sleuth

Spring Cloud应用程序的分布式请求链路跟踪，支持使用Zipkin、HTrace和基于日志（例如ELK）的跟踪。

### Spring Cloud Stream

轻量级事件驱动微服务框架，可以使用简单的声明式模型来发送及接收消息，主要实现为Apache Kafka及RabbitMQ。
