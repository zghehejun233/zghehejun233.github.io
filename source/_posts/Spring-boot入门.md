---
title: Spring Boot入门
description: Springboot入门记录和Spring相关的东西
categories: 开发
tags:
  - Java
  - Spring
  - Spring Boot
  - 单元测试
  - 设计模式
abbrlink: 22597
banner_img: /post_img/spring_boot.jpg
index_img: /post_img/spring_boot.jpg
sticky: 100
date: 2022-04-05 12:39:00
---

<script src='https://gitee.com/guo-surui/fuck_course_design/widget_preview' async defer></script>
<div id="osc-gitee-widget-tag"></div>
<style>
.osc_pro_color {color: #4183c4 !important;}
.osc_panel_color {background-color: #ffffff !important;}
.osc_background_color {background-color: #ffffff !important;}
.osc_border_color {border-color: #e3e9ed !important;}
.osc_desc_color {color: #666666 !important;}
.osc_link_color * {color: #9b9b9b !important;}
</style>


# 前言

## 三层架构

### 基本层次

### PO、DTO、DAO等

### 各层设计原则

### 一些范例

## RESTfulAPI

> 参考资料
>
> https://www.runoob.com/w3cnote/restful-architecture.html

### 简述

REST全称是Representational State Transfer，中文意思是表述（编者注：通常译为表征）性状态转移。 

> 它首次出现在2000年Roy Fielding的博士论文中，Roy Fielding是HTTP规范的主要编写者之一。 
>
> 他在论文中提到："我这篇文章的写作目的，就是想在符合架构原理的前提下，理解和评估以网络为基础的应用软件的架构设计，得到一个功能强、性能好、适宜通信的架构。

REST指的是**一组架构约束条件和原则**。" 如果一个架构符合REST的约束条件和原则，我们就称它为RESTful架构。

REST本身并没有创造新的技术、组件或服务，而隐藏在RESTful背后的理念就是使用Web的现有特征和能力， 更好地使用现有Web标准中的一些准则和约束。

虽然REST本身受Web技术的影响很深， 但是理论上REST架构风格并不是绑定在HTTP上，只不过目前HTTP是唯一与REST相关的实例。 所以我们这里描述的REST也是通过HTTP实现的REST。

### 进一步解释

#### 资源与URI

> REST全称是表述性状态转移，那究竟指的是什么的表述? 其实指的就是资源。
>
> **任何事物，只要有被引用到的必要，它就是一个资源。**
>
> 资源可以是实体(例如手机号码)，也可以只是一个抽象概念(例如价值) 。

要让一个资源可以被识别，需要有个唯一标识，在Web中这个唯一标识就是URI(Uniform Resource Identifier)。

URI既可以看成是资源的地址，也可以看成是资源的名称。

> 如果某些信息没有使用URI来表示，那它就不能算是一个资源， 只能算是资源的一些信息而已。

URI的设计应该遵循可寻址性原则，具有自描述性，需要在形式上给人以直觉上的关联

### API的设计

## Spring家族

### Spring

### SpringBoot

### SSM架构

### SpringCloud

# Spring原理

## IOC容器

## AOP

# SpringBoot基本应用

## 创建一个项目

### 项目结构

一个全新的Springboot Web项目目录基本长成这个样子

```
|- java
  |- com.package.name
    |- SpringBootDemoApplication
  |- resources
    |- application.properties
|- test
  |- java
    |- com.package.name
      |- SpringBootDemoApplicationTest
|- pom.xml
```

可以参考如下形式构建项目结构

```
|- POJO
|- DAO
|- DTO
|- VO
|- service
|- service Implements
|- controller
|- config
|- utils
|- constants
```

其中一些分包和层次的解释

- POJO/PO：实体类，对于JPA项目可以使用models/domain，MyBatis项目可以使用pojo/entity
- DAO：数据访问层，对于JPA项目可以使用repository，MyBatis项目可以使用mapper
- DTO：数据传输对象，用于实现非侵入式的封装多个实体类之间的关系
- VO：显示层对象，通常是Web向模板渲染引擎层传输的对象。
- Service：数据服务接口层
- service implements：数据服务接口实现层，一般使用impl
- controller：前端控制器

对于Controller层，有一些约定

- 参数传递建议不要使用HashMap，建议使用数据模型定义
- 可以做参数校验、异常抛出等操作，但建议不要放太多业务逻辑，业务逻辑尽量放到Service层代码中去做

> 参考资料
>
> 分层资料
>
> https://blog.csdn.net/qq_35246620/article/details/77247427
>
> https://www.zhihu.com/question/39651928
>
> https://blog.csdn.net/qq_39615545/article/details/90172038
>
> https://zhuanlan.zhihu.com/p/115403195
>
> 命名规范
>
> https://blog.csdn.net/Luomingkui1109/article/details/78882468
>
> https://blog.csdn.net/qq_33404395/article/details/79877384?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-1.pc_relevant_aa&spm=1001.2101.3001.4242.2&utm_relevant_index=4
>
> https://blog.csdn.net/weixin_30474613/article/details/95303995?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2.pc_relevant_paycolumn_v3&utm_relevant_index=5

### 依赖分析

> 对于一个使用Maven配置的Springboot项目，依赖由`pom.xml`文件来描述。

```xml
# 版本号和编码
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    # 1------parent
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.6.4</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    # 2-----项目元数据
    # 这一部分就是在创建时的Project Metadata
    <groupId>com.surui</groupId>
    <artifactId>spring_boot_example</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>spring_boot_example</name>
    <description>spring_boot_example</description>
  
    <properties>
        <java.version>11</java.version>
    </properties>
    # 3-----具体依赖
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    # 4----构建配置
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```



以上主要分为四个部分

1. parent：继承spring-boot-starter-parent的依赖管理，控制版本与打包等内容

2. 项目元数据：创建时候输入的Project Metadata部分，也就是Maven项目的基本元素，包括：groupId、artifactId、version、name、description等
3. dependencies：项目具体依赖，这里包含了spring-boot-starter-web用于实现HTTP接口（该依赖中包含了Spring MVC）；spring-boot-starter-test用于编写单元测试的依赖包。更多功能模块的使用我们将在后面的教程中逐步展开。
4. build：构建配置部分。默认使用了spring-boot-maven-plugin，配合spring-boot-starter-parent就可以把Spring Boot应用打包成JAR来直接运行。

## 配置文件

> 参考资料
>
> https://blog.didispace.com/spring-boot-learning-21-1-3/

`src/main/resources`目录是Spring Boot的配置目录，所以我们要为应用创建配置个性化配置时，就是在该目录之下。Spring Boot的默认配置文件位置为： `src/main/resources/application.properties`。

关于Spring Boot应用的配置内容都可以集中在该文件中了，根据我们引入的不同Starter模块，可以在这里定义诸如：容器端口名、数据库链接信息、日志级别等各种配置信息。

> 比如，我们需要自定义web模块的服务端口号，可以在`application.properties`中添加`server.port=8888`来指定服务端口为8888，也可以通过`spring.application.name=hello`来指定应用名（该名字在Spring Cloud应用中会被注册为服务名）。

Spring Boot的配置文件除了可以使用传统的properties文件之外，还支持现在被广泛推荐使用的YAML文件。

### 多个环境分别配置

对于多环境的配置，各种项目构建工具或是框架的基本思路是一致的，通过配置多份不同环境的配置文件，再通过打包命令指定需要打包的内容之后进行区分打包，Spring Boot也不例外，或者说更加简单。

在Spring Boot中多环境配置文件名需要满足`application-{profile}.properties`的格式，其中`{profile}`对应你的环境标识，比如：

- `application-dev.properties`：开发环境
- `application-test.properties`：测试环境
- `application-prod.properties`：生产环境

至于哪个具体的配置文件会被加载，需要在`application.properties`文件中通过`spring.profiles.active`属性来设置，其值对应配置文件中的`{profile}`值。如：`spring.profiles.active=test`就会加载`application-test.properties`配置文件内容。

因此，多环境配置有这个思路

- `application.properties`中配置通用内容，并设置`spring.profiles.active=dev`，以开发环境为默认配置
- `application-{profile}.properties`中配置各个环境不同的内容
- 通过命令行方式去激活不同环境的配置

特别的，YAML可以在一个单个文件中通过使用`spring.profiles`属性来定义多个不同的环境配置。

例如下面的内容，在指定为test环境时，`server.port`将使用8882端口；而在prod环境，`server.port`将使用8883端口；如果没有指定环境，`server.port`将使用8881端口。

```yaml
server:
  port: 8881
---
spring:
  profiles: test
server:
  port: 8882
---
spring:
  profiles: prod
server:
  port: 8883
```



### 自定义参数和参数引用

在配置文件中添加**自定义参数**

```xml
book.name=SpringCloudInAction
book.author=ZhaiYongchao
```

自定义参数时还可以**引用参数**

```xml
book.name=SpringCloud
book.author=ZhaiYongchao
book.desc=${book.author}  is writing《${book.name}》
```

就可以直接使用`@Value`注解调用自定义参数

```java
@Component
public class Book {

    @Value("${book.name}")
    private String name;
    @Value("${book.author}")
    private String author;

    // 省略getter和setter
}
```

### 建立实体类

示例

```java
@Data
public class User {

    private Long id;
    private String name;
    private Integer age;

}
```

>  这里使用`@Data`注解可以实现在编译器自动添加set和get函数的效果。该注解是lombok提供的，只需要在`pom.xml`里引入即可

## 实现一个接口

### 可能使用到的注解

- `@Controller`：修饰class，用来创建处理http请求的对象 
- `@RestController`：Spring4之后加入的注解，原来在`@Controller`中返回json需要`@ResponseBody`来配合，如果直接用`@RestController`替代`@Controller`就不需要再配置`@ResponseBody`，默认返回json格式
- `@RequestMapping`：配置url映射。现在更多的也会直接用以Http Method直接关联的映射注解来定义，比如：`GetMapping`、`PostMapping`、`DeleteMapping`、`PutMapping`等

参数的绑定

- `@RequestParam`：接受页面中传递来的参数
- `@RequestBody`：用来绑定通过http请求中application/json类型上传的数据
- `@PathVariable`：用于获取url中的参数，需要在映射时使用花括号注明



### 编写Controller

首先在类声明外使用注解`@RequestMapping(value = "/users")`进行一次分发，将所有`.../users/...`都分发到这个controller下

使用`GetMapping`等注解实现具体请求

> 在这里没有对service层进行分离

```java
@RestController
@RequestMapping(value = "/users")     // 通过这里配置使下面的映射都在/users下
public class UserController {

    // 创建线程安全的Map，模拟users信息的存储
    static Map<Long, User> users = Collections.synchronizedMap(new HashMap<Long, User>());

    /**
     * 处理"/users/"的GET请求，用来获取用户列表
     *
     * @return
     */
    @GetMapping("/")
    public List<User> getUserList() {
        // 还可以通过@RequestParam从页面中传递参数来进行查询条件或者翻页信息的传递
        List<User> r = new ArrayList<User>(users.values());
        return r;
    }

    /**
     * 处理"/users/"的POST请求，用来创建User
     *
     * @param user
     * @return
     */
    @PostMapping("/")
    public String postUser(@RequestBody User user) {
        // @RequestBody注解用来绑定通过http请求中application/json类型上传的数据
        users.put(user.getId(), user);
        return "success";
    }

    /**
     * 处理"/users/{id}"的GET请求，用来获取url中id值的User信息
     *
     * @param id
     * @return
     */
    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        // url中的id可通过@PathVariable绑定到函数的参数中
        return users.get(id);
    }

    /**
     * 处理"/users/{id}"的PUT请求，用来更新User信息
     *
     * @param id
     * @param user
     * @return
     */
    @PutMapping("/{id}")
    public String putUser(@PathVariable Long id, @RequestBody User user) {
        User u = users.get(id);
        u.setName(user.getName());
        u.setAge(user.getAge());
        users.put(id, u);
        return "success";
    }

    /**
     * 处理"/users/{id}"的DELETE请求，用来删除User
     *
     * @param id
     * @return
     */
    @DeleteMapping("/{id}")
    public String deleteUser(@PathVariable Long id) {
        users.remove(id);
        return "success";
    }

}
```

# MyBatis

## 示例

- 引入MyBatis的Starter以及MySQL Connector依赖

  > 注意MyBatis的版本关系
  >
  > - `2.1.x`版本适用于：MyBatis 3.5+、Java 8+、Spring Boot 2.1+
  > - `2.0.x`版本适用于：MyBatis 3.5+、Java 8+、Spring Boot 2.0/2.1
  > - `1.3.x`版本适用于：MyBatis 3.4+、Java 6+、Spring Boot 1.5
  >
  > 其中，目前还在维护的是`2.1.x`版本和`1.3.x`版本

- 在`application.properties`中配置mysql的连接配置

- Mysql中创建一张用来测试的表

- 创建User表的映射对象User

- 创建User表的操作接口：UserMapper

  ```java
  @Mapper
  public interface UserMapper {
  
      @Select("SELECT * FROM USER WHERE NAME = #{name}")
      User findByName(@Param("name") String name);
  
      @Insert("INSERT INTO USER(NAME, AGE) VALUES(#{name}, #{age})")
      int insert(@Param("name") String name, @Param("age") Integer age);
  
  }
  ```

## 可能用到的注解

- `@Param：`@Param`中定义的`name`对应了SQL中的`#{name}`，`age`对应了SQL中的`#{age}`。
- `@Map`：通过`Map<String, Object>`对象来作为传递参数的容器

## 增删改查的实现

```java
public interface UserMapper {

    @Select("SELECT * FROM user WHERE name = #{name}")
    User findByName(@Param("name") String name);

    @Insert("INSERT INTO user(name, age) VALUES(#{name}, #{age})")
    int insert(@Param("name") String name, @Param("age") Integer age);

    @Update("UPDATE user SET age=#{age} WHERE name=#{name}")
    void update(User user);

    @Delete("DELETE FROM user WHERE id =#{id}")
    void delete(Long id);
}
```

### 查询

对于增、删、改操作相对变化较小。而对于“查”操作，我们往往需要进行多表关联，汇总计算等操作，那么对于查询的结果往往就不再是简单的实体对象了，往往需要返回一个与数据库实体不同的包装类，那么对于这类情况，就可以通过`@Results`和`@Result`注解来进行绑定，具体如下：

```java
@Results({
    @Result(property = "name", column = "name"),
    @Result(property = "age", column = "age")
})
@Select("SELECT name, age FROM user")
List<User> findAll();
```

在上面代码中，@Result中的property属性对应User对象中的成员名，column对应SELECT出的字段名。在该配置中故意没有查出id属性，只对User对应中的name和age对象做了映射配置

## 自动建表

> 参考资料
>
> https://github.com/zyf970617/mybatis-auto-create-table

## 跨表查询

> 参考资料
>
> https://blog.51cto.com/u_15305798/3130563



# Spring Jpa

## 基本的实体管理

### 唯一性约束

## 多表关联

> 参考资料
>
> https://glory.blog.csdn.net/article/details/79465859?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1.pc_relevant_paycolumn_v3&utm_relevant_index=1
>
> https://chuhang123.github.io/2017/10/09/Learning-JPA-OneToMany/
>
> https://www.jianshu.com/p/bf6b7b0da8d8
>
> http://wangzhenhua.rocks/zh-hans/java/jpa-one-to-many-many-to-one-best-practice

 我们在使用JPA的时候，会使用OneToMany表示对象之间的一对多的关系，ManyToOne表示多对一的关系。

多对一和一对多只是对象关系中的正面描述和反面描述，在JPA中不一样的定义方法会有不同的SQL生成，对性能会有比较大的影响。

> 比如我们举一个例子：一个学校会有很多的学生，很多学生都会在一个学校上学，那么我们应该会设计一个父对象School和一个子对象Student，School实体会和和Student之间有一对多的关联关系，Student实体和School实体有多对一的关联关系。

在JPA中对于上述的场景描述我们会有三个不同的做法：

1. 在父对象中使用`@OneToMany`建立和子对象的关系关系
2. 在父对象中使用`@OneToMany`和`@JoinColumn`来建立和子对象的关系
3. 建立双向关系，在父对象中使用`@OneToMany`，在子对象中使用`@ManyToOne`
4. 在子对象中使用`@ManyToOne`建立和父对象的联系

### 只在父对象中使用`@OneToMany`

- 只需要在父对象中声明即可，例如

  ```java
  public class School {
      @Id
      @GeneratedValue(strategy = GenerationType.SEQUENCE)
      private long id;
  
      private String name;
  
      @OneToMany(
              cascade = CascadeType.ALL,
              orphanRemoval = true
      )
      @JoinColumn(name = "school_id")
      private List<Student> students;
  
  }
  
  public class Student {
  
      @Id
      @GeneratedValue(strategy = GenerationType.SEQUENCE)
      private long id;
  
      private String name;
  }
  ```

- 这种方式实际上上建立了多对多的关系，也就是说Jpa会建立一张新的多对多表进行记录，SQL语句示例

  ```sql
  Hibernate: insert into School (name) values (?)
  Hibernate: insert into Student (name) values (?)
  Hibernate: insert into Student (name) values (?)
  Hibernate: insert into Student (name) values (?)
  Hibernate: insert into School_Student (School_id, students_id) values (?, ?)
  Hibernate: insert into School_Student (School_id, students_id) values (?, ?)
  Hibernate: insert into School_Student (School_id, students_id) values (?, ?)
  ```

### 在父对象中使用`@OneToMany`和`@JoinColumn`

- 示例

  ```java
  public class School {
      @Id
      @GeneratedValue(strategy = GenerationType.SEQUENCE)
      private long id;
  
      private String name;
  
      @OneToMany(
              cascade = CascadeType.ALL,
              orphanRemoval = true
      )
      @JoinColumn(name = "school_id")
      private List<Student> students;
  
  }
  ```

  

- 这里没有生成多对多的中间表，而是在student表中多了一个school_id的字段，要比上面生成的sql要精简了很多，但是问题是这里创建student的school_id的值是通过update语句更新进去的。因此这还不是一个最佳的sql语句。

### 父对象中使用`@OneToMany`，子对象使用`ManyToOne`

- 示例

  ```java
  public class School {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      @GenericGenerator(name = "native", strategy = "native")
      @Column(name = "id", updatable = false, nullable = false)
      private long id;
  
      private String name;
  
      @OneToMany(
              mappedBy = "school",
              cascade = CascadeType.ALL,
              orphanRemoval = true
      )
      private Set<Student> students;
  
  }
  
  public class Student {
  
      @Id
      @GeneratedValue(strategy = GenerationType.SEQUENCE)
      private long id;
  
      private String name;
  
      @ManyToOne
      @JoinColumn(name = "school_id")
      private School school;
  
  }
  ```

- 请注意，这里`@JoinColumn`在子对象中被使用，其注解的是一个父对象，但其作用还是相同的

- 这个结果是我们预期生成的，并没有额外的SQL产生。但是这里还存在的问题是在School中定义的OneToMany有导致内存泄漏的风险，因为我们没有办法控制它获取数据的数量，即使我们使用了懒加载，也有内存泄漏的问题。

### 子对象中使用`@ManyToOne`

- 这个就是一对多关系最完美的解决方案
- 可以实现的查询方式

### 使用`@ManyToOne`和`@OneToMany`实现双向一对多关系

> 本质上是双向一对多的关系，并不能叫做多对多

### 使用`@ManyToMany`实现多对多关系

1. `@ManyToMany 注解用于关系的发出端和接收端`
2. `同时关系的发出端和接收端--定义一个集合类型的接收端的字段属性；`
3. `关系的接收端，@ManyToMany(mappedBy='集合类型发出端实体的字段名称')；`

由于`@JoinTable`和`@JoinColumn`一般定义在拥有关系的这一端，而`@mappedBy`一定是定义在关系的被拥有方（the owned side），也就是跟定义`@JoinTable`和`@JoinColumn`互斥的一方，它的值指向拥有方中关于被拥有方的字段，可能是一个对象（`@OneToMany`），也可能是一个对象集合（`@ManyToMany`）。

## 一/多对多关系中的级联管理

> 参考资料
>
> https://wycode.cn/2018-04-19-many_to_many.html

实际业务中，我们通常会遇到以下情况：

1. 用户和用户的收货地址是一对多关系，当用户被删除时，这个用户的所有收货地址也应该**一并删除**。
2. 订单和订单中的商品也是一对多关系，但订单被删除时，订单所关联的商品肯定**不能被删除**。

此时只要配置正确的级联关系，就能达到想要的效果。

级联关系有

- CascadeType.REFRESH：级联刷新，当多个用户同时作操作一个实体，为了用户取到的数据是实时的，在用实体中的数据之前就可以调用一下refresh()方法
- CascadeType.REMOVE：级联删除，当调用remove()方法删除Order实体时会先级联删除OrderItem的相关数据
- CascadeType.MERGE：级联更新，当调用了Merge()方法，如果Order中的数据改变了会相应的更新OrderItem中的数据
- CascadeType.ALL：包含以上所有级联属性
- CascadeType.PERSIST：级联保存，当调用了Persist() 方法，会级联保存相应的数据

# 鉴权的实现

# 单元测试

## 简单的单元测试



# 日志

## 配置

- 启动日志：通过在`pom.xml`中引入了Lombok，然后使用`@Slf4j`声明引入Slf4j的`log`日志记录对象，之后就可以轻松的用它来日志了。而这个日志具体是如何写到控制台或者文件的，则有Spring Boot项目中引入了什么具体的日志框架决定，默认情况下就是Logback

- 开启DEBUG日志：在配置文件`application.properties`中配置`debug=true`

  > 这里开启的DEBUG日志，仅影响核心Logger，包含嵌入式容器、hibernate、spring等这些框架层面的会输出更多内容，但是你自己应用的日志并不会输出为DEBUG级别

- 多彩输出：

- 通过在`application.properties`中设置`spring.output.ansi.enabled`参数来支持，该参数有三个选项：

  - NEVER：禁用ANSI-colored输出
  - DETECT：会检查终端是否支持ANSI，是的话就采用彩色输出（默认项）
  - ALWAYS：总是使用ANSI-colored格式输出，若终端不支持的时候，会有很多干扰信息，不推荐使用

# 部署

## 启动Springboot项目

## 打包

## 在服务器上润起来
