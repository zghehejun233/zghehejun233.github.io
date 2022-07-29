---
title: java课程设计实验报告
description: 实验报告啊实验报告
categories: 学习
abbrlink: 38741
index_img: /post_img/231.png
banner_img: /post_img/231.png
---

# Java课程设计实验报告

## 系统总体要求

### 实验目的

锻炼学生使用高级程序设计语言进行面向对象的分析、设计和应用开发能力，结合JavaIO流技术、Spring相关框架、数据库技术、网络技术与Web前端开发技术等实现一个综合性的应用框架。

### 硬件环境

- PC：Ryzen7 5800H，16G
- Mac：M1 Silicon
- 阿里ECS
- 阿里云RDS MySQL
- 阿里云Redis

### 软件环境

- 操作系统：Windows10 Professional，Windows11，Ubuntu 18.04，MacOS Monterey
- 开发工具：IDEA，VIsual Studio Code，OpenJDK，WebStorm，npm，nrm，Maven，[Android Studio，Flutter SDK]
- 数据服务：MySQL，SQLite，Redis
- 数据设计：Navicat，DataGrip，Another Redis Desktop Manager
- 版本控制：Git
- 后端框架：Spring，Spring Boot，Spring Data JPA
- Web服务：Nginx

## 系统总体要求

### 系统总功能要求

本次设计要求利用Java实现一个学生信息管理平台（PC版，应用于校内网有线网络访问，暂不开发移动端）。主要功能为

1. 学生基本信息、联系方式、入学前信息、家庭信息、社会关系等基本信息的管理。
2. 学习信息管理，包括课程基本信息，课程中心（教材、课件、参考资料等）选课信息、考勤信息、作业信息、成绩信息等。
3. 学生社会实践、学科竞赛、科技成果、培训讲座、创新项目、校外实习等创新实践信息管理。
4. 学生荣誉信息管理，包括获得的各种称号奖励等。
5. 学生体育活动、外出旅游、文艺演出、聚会、等日常活动管理。
6. 学生外出请假信息和生活学习消费等日志信息管理。
7. 学生个人信息的统计汇入统计数据库。
8. 学生各种信息的查询统计、综合绩分的计算（可自行设计公式）和学生个人画像、个人简历的生成打印。

（所谓信息管理就是信息的CRUD——创建添加，读取查询，更新修改，删除）

### 开发平台介绍

#### IDEA

#### Visual Studio Code

### 开发进度表

### 小组成员分工表

> 以下按照姓名首字母排序

| 姓名   | 工作内容                                                                                                                               | 成绩比重 |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| 郭苏睿 | 编写选课功能</br>实现各个科目的成绩计算、绩点计算和排名业务</br>设计系统架构，提供实现思路，规范编码风格                               | 1.0      |
| 何硕   | 编写日常信息和部分选课信息模块，实现增删改查功能</br>维护版本库，编写开发文档和版本修改记录</br>实现简历功能                           | 1.0      |
| 胡钊   | 编写学生基本信息和课程信息模块，实现增删改查功能</br>设计接口，编写开发文档</br>优化编码风格，添加部分异常的捕获                       | 1.0      |
| 吕俊安 | 调整业务细节，优化算法提高运算速度降低资源占用</br>编写单元测试、集成测试，排查系统漏洞和逻辑缺陷</br>测试系统性能。添加部分异常的捕获 | 1.0      |

## 需求分析

### 需求简述

对于山东大学来讲，现有在校教职工数量众多，其中学生的学习、生活会产生大量信息，对于学生方和校方都存在学生信息管理系统的迫切需求。

#### 价值评估

该需求有较大的现实意义，能够有效简化教师、学生获取相关信息的效率，同时可以提供大量数据供后期分析，帮助学校改善提高教学质量，更好服务学生；协助同学们更清晰的了解自己学习和生活状况。

从技术角度来讲，本需求实现难度尚可，在前后端分离的条件下基本符合现代主流Web开发模式。且其子需求的实现均属于常见功能，并无太多需要集中研究的开发问题。

综合评估，本需求的价值满足产品上线条件。

### 作品说明

- 作品定位：面向所有山东大学师生
- 作品综述

| 项目     | 内容                                                                                    |
| -------- | --------------------------------------------------------------------------------------- |
| 作品名称 | 学生信息管理系统                                                                        |
| 作品定位 | 提高师生在校学习生活便利性                                                              |
| 作品特色 | 1. 内容覆盖全面<br>2.系统运行稳定性良好<br>3.具有较高的工作效率和性能<br>4.可拓展性良好 |
| 目标人群 | 山东大学全体师生                                                                        |

### 需求描述

#### 功能性需求

1. 作品设计的内容应当覆盖学生日常生活的方方面面，充分反映学习生活
2. 部分功能对教师和学生两类用户进行分离
3. 作品可以提供所有信息的增删改查
4. 提供检索和快速筛选的功能，方便快速找到目标条目
5. 作品基于部分数据可以描绘学生的画像
6. 提供对系统运行状况的监控，对数据空间告急等情况及时警告提示

#### 非功能性需求

1. 作品应当有良好的UI，并提供多端入口，包括但不限于Web、桌面客户端、Android和iOS等
2. 作品对数据有分析统计的能力
3. 作品对部分频繁读取数据提供缓存缓解服务器运算和数据库读写压力

#### 功能权限

1. 系统提供对学生和教师的权限分离
2. 系统保留对权限的延伸能力

#### 数据维护需求

1. 系统保证关联数据的正确删除，避免残留数据
2. 维护数据表关系

### 需求视图

#### 功能流程图

此处为登录页

![image-20220514161222178](https://tva1.sinaimg.cn/large/e6c9d24ely1h2802p95bij21kg0u0wfd.jpg)

这里展示对于学生新的增删改查，首先是入口页面，提供了滑动浏览的能力；一般展示模块摘要、检索功能和数据三个卡片

![image-20220514161303192](https://tva1.sinaimg.cn/large/e6c9d24ely1h2803dbi0qj21kq0u0af2.jpg)

检索功能支持分类型搜索，可以通过下拉菜单选择，有模糊匹配能力

![image-20220514161427104](https://tva1.sinaimg.cn/large/e6c9d24ely1h2804tn8koj20v408274q.jpg)

对于超出长度的数据，可以通过翻页快速浏览；部分操作按钮被收纳在单元格内

![image-20220514161530381](https://tva1.sinaimg.cn/large/e6c9d24ely1h2805xjlv9j21f70u044e.jpg)

点击添加即可进入添加页面，部分元素提供了下拉选择的能力；通过左上角返回可以回到原界面

![image-20220514161648297](https://tva1.sinaimg.cn/large/e6c9d24ely1h28079ss9lj21gv0u0gnv.jpg)

以下三个按钮分别对应编辑、删除和查看详情操作

![image-20220514161733438](https://tva1.sinaimg.cn/large/e6c9d24ely1h28082953aj207e02ma9x.jpg)

部分模块提供二级链接，点击蓝色字体即可跳到子页面

![image-20220514161932513](https://tva1.sinaimg.cn/large/e6c9d24ely1h280a4dqhcj21ok0u0n23.jpg)

在学生管理页面点击学生姓名，应当跳转到个人简历页面

![image-20220514162219306](https://tva1.sinaimg.cn/large/e6c9d24ely1h280d0rlq3j21h20u0taq.jpg)

![image-20220514162236504](https://tva1.sinaimg.cn/large/e6c9d24ely1h280dbhh10j21h40u0myv.jpg)

点击按钮获得pdf版本的简历文件

![image-20220514162353023](https://tva1.sinaimg.cn/large/e6c9d24ely1h280en5efij2154044dft.jpg)

## 系统设计

### 系统概要设计

![aedas](https://tva1.sinaimg.cn/large/e6c9d24ely1h280g16iskj21yw0u0aha.jpg)

#### 总体架构

本系统架构基本基于MVC，在数据访问层进行进一步分离

以下给出系统架构图

![8CCDD3D95FDD4B60736922F30ABF5952](https://tva1.sinaimg.cn/large/e6c9d24ely1h285qzql70j20o20r7dhw.jpg)

其中，

1. Web层(C)：位于`controller`包下，负责对http请求的分发和`@Validation`校验异常的捕获及处理
2. 服务层(C)：由于本系统初版直接进行了响应数据的处理，本系统此处并未将本层设计为接口，而是使用普通类的形式；主要负责对请求体的解包，包装成实体类对象参与传递，以及提供服务实现层状态的维护。
3. 服务实现层(C)，本层用于业务的实现，严格杜绝对上层的访问操作，仅提供本层和对数据访问层的权限。
4. 数据访问层(M)：本次用于维护实体关系和封装对数据库表的直接操作

本系统总体架构具有良好的鲁棒性，符合高内聚低耦合的要求

Web层与其下的服务层、服务实现层有一一对应关系，Web层仅负责请求的解析、远程方法的调用、异常捕获以及请求体和参数的传递；在服务层，主要将请求体封装为合适的PO或者DTO传递给服务实现层并维护服务实现层对象的状态；服务实现层主要用于实现对应实体增删改查业务，部分类参与对非实体类对象的计算和维护；数据访问层实现了对所有数据库操作的封装，避免对数据库的直接访问操作。

在实际业务过程中，类的分类被进一步细化。

本系统参考阿里巴巴开发手册，规定以下集中：

- POJO: 位于`models`包下，具有现实世界对应关系的实体类，一定有上述四层结构
- VO：使用较少，未定义类文件，在服务层和服务实现层直接组合，强制要求服务层和服务实现层命名包含`VO`
- DTO：位于`dto`包下，用于数据流转，本系统内主要负责包装成绩计算相关的数据，便于数据流转，降低系统耦合性
- BO：仅包含对简历信息的封装，具有实际业务意义

#### 工作流程

本报告将系统的工作划分为如下几个阶段

1. 接受http请求。
2. 处理数据，封装对象。
3. 操作数据库。
4. 后台定时工作。
5. 生成简历和个人画像。

#### 功能模块划分

##### 四个基本模块

学生基本信息模块用于记录学生的基本信息，包括性别、年龄、学院、年级等等。
配备了基本的增删改查能力，查询可以使用两种模式选择；
点击每个学生的姓名可以跳转到该学生的个人简历页面；
个人简历将会根据该学生的信息生成两个图表便于展示。

学生课程信息模块用于记录学生与课程相关的信息，比如选课、作业完成情况等等。
配备了基本的增删改查能力，查询可以使用两种模式选择。

教研活动模块用于记录学生与各种教学活动，包含课内课外的相关的信息。
配备了基本的增删改查能力，查询可以使用两种模式选择。

日常信息模块用于记录学生的日常活动，如支出、消费等等。
配备了基本的增删改查能力，查询可以使用两种模式选择。

##### 成绩计算和排名模块

基于Redis和Spring Boot定时事务，主动计算成绩。

本作品将会定时计算所有同学的成绩并进行排名，学生在查询时只需查找对应的成绩即可，能够有效降低服务器的读写压力，保护数据安全。

考虑到AOP设计理念，此处业务架构示例图如下

![7C72482DAA62F63FB194123660FD6841](https://tva1.sinaimg.cn/large/e6c9d24ely1h285qox87bj218p0ptdjp.jpg)

##### 简历信息模块

利用`echarts.js`绘制动态图表，生动展示学生的形象。

展示学生的各项基本信息。

### 系统详细设计

#### 包结构

```
main
|-- java.org.fatchmansoft.teach
|   |-- java
|   |   |-- config
|   |   |   |-- ...
|   |   |-- controllers
|   |   |   |-- ...
|   |   |-- dto
|   |   |   |-- ...
|   |   |-- models
|   |   |   |-- ...
|   |   |-- payload
|   |   |   |-- ...
|   |   |-- repository
|   |   |   |-- ...
|   |   |-- security
|   |   |   |-- ...
|   |   |-- service
|   |   |   |-- ...
|   |   |-- sqlite
|   |   |   |-- ...
|   |   |-- util
|   |   |   |-- ...
|   |   |-- RunJApplet
|   |   |-- SpringBootSecurityJwtApplication
|   |   |-- SystemApplicationListener
|   |-- resources
|-- test
|   |-- java
|   |   |--- models
|   |   |--- redis
```

其中，`controllers`用于存放Web控制器进行请求分发

```
|-- acdemic
|   |-- ...
|-- acdemic_activity
|   |-- ...
|-- daily
|   |-- ...
|-- student_basic
|   |-- ...
|-- system
|   |-- ...
|-- IntroduceController
```

`dto`用于存放DTO对象及其相关的工具类

```
|-- AverageScoreDTO
|-- ChartInformationDTO
|-- CourseRankDTO
|-- COurseRankComparator
|-- CourseRankDTOSerializator
|-- TotalRankDTO
|-- TotalRankDTOComparator
|-- TotalRankDTOSerializator
|-- TotalScoreDTO
```

`models`包下包含所有的实体类，此处不再斤西瓜展开

`service`包包含业务逻辑部分

```
|-- academic
|   |-- ...
|-- acdemic_activity
|   |-- ...
|-- daily
|   |-- ...
|-- student_basic
|   |-- EducationExperienceImpl
|   |-- EducationExperienceService
|   |-- FamilyImpl
|   |-- FamilyService
|   |-- SocialRelationImpl
|   |-- SocialRelationService
|   |-- StudentImpl
|   |-- StudentService
|-- vo_service
|   |-- AcademicActivityVOService
|   |-- AcademicActivityVOImpl
|   |-- DailyVOService
|   |-- DailyVOImpl
|   |-- StudentAcademicService
|   |-- StudentAcademicImpl
|-- GlobalScoreService
|-- IntroduceService
|-- IntroduceServiceImpl
|-- SystemService
|-- TestService
```

#### 实体关系展示

以下展示几个模块的类图

![67F51931BEF301D17FD04FF14071DBC7](https://tva1.sinaimg.cn/large/e6c9d24ely1h283rpvm2nj20rd0tywiq.jpg)

![155A68AF6CDF1DC525CF93A92405278F](https://tva1.sinaimg.cn/large/e6c9d24ely1h283s3f9lhj20sd0k7dkf.jpg)

![D6CF655E21EA2156082FFF28674E49A1](https://tva1.sinaimg.cn/large/e6c9d24ely1h283rz61rgj20rh0qate2.jpg)

![60CCCAF20310A1044A3AE73C4DC6DACC](https://tva1.sinaimg.cn/large/e6c9d24ely1h283sae77wj20tz0k842q.jpg)

![EDB199DD7186AEFE1F69FC175625AFF3](https://tva1.sinaimg.cn/large/e6c9d24ely1h283se56mzj21030rp0z8.jpg)

#### 工作流程展示

此处给出一种典型的工作模式

![BFE9333D5A663FA8FA65F81115C95C82](https://tva1.sinaimg.cn/large/e6c9d24ely1h283ren9xaj20u00xj0z4.jpg)

## 系统实现

### 单一对象的建立和维护

单一对象的建立和维护需求实现起来最为简单。

MVC架构最大的历史意义在于将单体应用实现了垂直分层，这使得层与层之间的耦合度降低，且有效提高了服务层的复用性，这为Spring框架的AOP思想奠定坚实基础。

基于课堂上的框架，本组对本作品进行了进一步分包以明确类职责。

其中值得一提的是控制层，即C层。在MVC提出后，应用的可维护性、可拓展性得到极大提高，但开发者也逐渐发现MVC往往会带来C层的臃肿。针对这个问题，前端开发领域提出了MVP(Model-View-Presenter)模式，后来又衍生出MVVM(Model-VIew-ViewModel)模式以解决这个现象；针对本作品，本组参考常规的业务实现与架构方法，结合项目本身情况报告后，使用服务层与服务实现层来降低耦合、提高可维护性。

本组的方案基本参考了Spring Boot应用的架构方式，即Service接口+ServiceImpl类实现的思路。但在此基础上，本组将服务(Service)层使用类实现，并提供一些逻辑来缓解服务实现层的压力。其任务有以下两点

1. 解包请求体，封装实体类。

   由于上层控制器只进行分发，服务层接收到的唯一参数认识请求体，因此，本组在此处对请求体进行解析并建立对应的POJO或DTO进行接下来的传递。

   这种方式，一可以使得程序更加安全健壮：使用请求体或Map来传值是危险的，因为下级无法了解上级打包了多少内容，极易出现空指针或错误取值；二有效降低耦合性、提高复用性：在服务之间出现调用关系时，只要OOP构造足够合理完善，服务实现曾能覆盖对象需要进行的操作，可以只在服务层之间进行相互调用，避免了穿透到服务实现层甚至数据操作层。

2. 维护服务实现层状态。

    由于对多方对象操作，特别是建立和查询时，需要多方对象持有一个一方对象的引用，或者说句柄，所以本组在多方的服务实现层维护一个一方的主键（在多对多情况下持有多个多方的主键们）来作为这个句柄。

    因此，本组将服务实现层的维护权移交给上层。由对应的服务层提供句柄的初始化操作。

以下以对`Student`类的操作为例进行说明。

#### 实体类的建立和数据操作层封装

以下为`Student`类的主要内容

> 如非特殊说明，以下所有代码应用均不包含导入部分

```java
@Entity
@Table(name = "student", uniqueConstraints = {
        @UniqueConstraint(columnNames = {"student_id", "student_num"})
})
@NoArgsConstructor
@Getter
@Setter
@AllArgsConstructor
public class Student {
    @Id
    @Column(name = "student_id")
    private Integer studentId;
    @Column(name = "student_num")
    @NotBlank(message = "学号不能为空！")
    private String studentNum;
    // 此处省略一部分代码
    @Column(name = "email")
    @Email
    private String email;

    @OneToMany(mappedBy = "student", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private Set<Family> families;
    // 此处省略一部分代码
    @OneToMany(mappedBy = "student", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private Set<Achievement> achievements;

    @Override
    public boolean equals(Object o) {
                // 省略部分代码
        return studentId != null && Objects.equals(studentId, student.studentId);
    }

    @Override
    public int hashCode() {
        return getClass().hashCode();
    }

    @Override
    public String toString() {
        return "Student{" +
                "studentId=" + studentId +
                // 省略部分代码
                ", email='" + email + '\'' +
                '}';
    }
}
```

> 此处省略内容与一对多、多对多相关，将在下面进一步展示。

实体类的编写，有以下几点值得一提

- 使用`Lombok`。众所周知，实体类的编写有大量Setter与Getter，使用`Lombok`注解可以极大减少代码量，提高代码可读性
- `override`三个基本方法。对实体类来讲，`hashCode()`，`equals()`和`toString`都是非常重要的方法。其中`equals()`基于`hasCoode()`。
  
  > 值得一提的是，对于直接连接的多对多关系并没有包含到`toString()`方法里。这是由于在多方A对多方B调用时，由于B也持有一个A的集合，就会带来递归调用进而导致stack overflow。

- 使用注解进行校验。该类使用了`@NotBlank`、`@Email`和`@Min`等注解，可以帮助实现参数的校验。
- 对每个参数使用`@Column`注解。使用该注解与数据库表字段的映射关系，可以在必要时手动进行数据库的迁移，同时配合IDEA强大的辅助功能可以实时查看JPA能否保证正确映射。
- 指定`uniqueconstraints`。使用`@UniqueConstraints`注解进行约束。

在此基础上，我们已经建立了一个内容丰富、结构良好的实体类。我们在此基础上封装他的数据操作层。

以下为`StudentRepository`的内容

```java
@Repository
public interface StudentRepository extends JpaRepository<Student, Integer> {
    /**
     * 获取最大id
     *
     * @return 最大id
     */
    @Query(value = "select max(studentId) from Student  ")
    Integer getMaxId();

    /**
     * 根据学号或姓名查询对象
     * 
     * @param numName 学号或者姓名
     * @return 对象数组
     */
    @Query(value = "from Student where ?1='' or studentNum like %?1% or studentName like %?1% ")
    List<Student> findStudentListByNumName(String numName);

}
```

在这里，本组做的工作有

- 使用javadoc形式注释。javadoc形式的注释覆盖了本作品中大部分的服务层和数据操作层方法，其最大的特点是方便，能够在调用时提示需要的参数、参数简介和返回值的简介。
- 使用`@Query`注解。尽管JPA具有一个强大的根据方法名实现功能的机制，在一些情况下指定SQL语句会有更好的效果。本作品暂不考虑对搜索的优化，所以其他多数地方均使用命名方式声明方法。

#### Web层对请求分发

让我们将目光转向控制器，此处以添加为例

```java
@CrossOrigin(origins = "*", maxAge = 3600)
@RestController
@RequestMapping("/api/teach")
public class StudentController {
    @Resource
    private StudentService studentService;

    @PostMapping("/studentInit")
    @PreAuthorize("hasRole('ADMIN')")
    public DataResponse studentInit(@Valid @RequestBody DataRequest dataRequest) {
        SystemApplicationListener.logger.info("studentInitStart");
        List<Object> result = studentService.getAllStudent(dataRequest);
        SystemApplicationListener.logger.info("studentInitEnd");
        return CommonMethod.getReturnData(result);
    }

    @PostMapping("/studentEditSubmit")
    @PreAuthorize("hasRole('ADMIN')")
    public DataResponse studentEditSubmit(@Valid @RequestBody DataRequest dataRequest) {
        // 捕获校验错误异常
        try {
            Integer result = studentService.saveStudent(dataRequest);
            return CommonMethod.getReturnData(result);
        } catch (ValidationException validationException) {
            String temp = validationException.getLocalizedMessage();
            // 通过拼接字符串返回更易读的错误信息
            return CommonMethod.getReturnMessage("400", temp.substring(temp.substring(0, temp.indexOf(":")).length() + 2));
        }
    }
    //  此处省略部分代码
}
```

上面展示的代码，主要作用是通过类和方法的两次分发对http请求进行映射，调用对应的方法，并捕获一些异常。

如上面所说，Web层最重要的任务是进行请求分发，在这一原则下每个`controller`文件在100行左右，具有良好的可读性，可以快速定位到分发时出现的问题；使用`@PreAuthorize`注解进行权限控制；使用`@Valid`注解进行参数校验，不满足实体类定义的字段将会抛出对应的异常并携带message信息返回前端。

值得一题的是，本项目大部分地方使用`@Resource`注解注入资源，主要有两个考虑

1. `@Autowired`不被建议进行`field injection`。最近几个版本Spring官方都在建议使用构造方法或`setter`的方式注入资源，而不是直接对属性注入1⃣️提高安全性，本项目懒得使用其他注入方式。
2. `@Resource`注解默认`byName`注入，`@Autowired`则是`byType`注入，有时需要指定`name`时要配合`@Qualifier`注解，略微麻烦一些，`@Resource`注解啧默认通过反射机制使用`byName`自动注入

经过分发后，我们的请求体内数据将来到下一层，服务层。

#### 服务层解包封装对象

服务层的实现方式给有区别，此处逐一给出展示

此处注入的只有对应服务实现层对象

```java
@Service
public class StudentService {
    @Resource
    private StudentImpl student;
// 略去
}
```

首先,展示用于页面初始化以及选择时调用的两个方法

```java

    /**
     * 获取所有学生的信息
     *
     * @param dataRequest 接受请求内容
     * @return 学生数组
     */
    public List<T> getAllStudent(DataRequest dataRequest) {
        return student.queryStudentMapList("");
    }
    // 省略部分代码
    /**
     * 传回某个学生的详细信息
     *
     * @param dataRequest 接受请求数据
     * @return 某个学生
     */
    public Map<String, Object> getStudentDetail(DataRequest dataRequest) {
        Integer studentId = dataRequest.getInteger("id");
        return student.queryStudentDetail(studentId);
    }
```

此处调用的是服务实现层的同一个方法，只是传入参数不同。在此处分离的考虑主要是本作品设计时对服务层是完全自上而下的，本组希望服务层与Web层有良好的合作关系，因此进行了分离；除此之外，这种设计可以避免取出请求体内容时出现空指针，一定程度上提高了安全性；这里javadoc形式的注解为其它类调用方法提供了一定帮助，并且在返回值时通过容器搭配泛型的方式带来良好的可复用性。

除此以外，可以看到第二个方法的第一行进行在请求体中取出内容的操作，者与上文所说服务层的定位是相同的——解析请求数据。服务层承担对请求体内容的解析工作，并对解析到的内容进行处理和包装后传递给下一层。当然，在上面的代码中并没有很显然的应用，下面我们以添加新学生的方法进一步观察一下。

```java
    /**
     * 持久化学生信息
     *
     * @param dataRequest 接受请求内容
     * @return 返回建立的学生id
     */
    public Integer saveStudent(DataRequest dataRequest){
        Map<String,Object> form = dataRequest.getMap("form");
        Student studentData = new Student();
        studentData.setStudentId(CommonMethod.getInteger(form,"id"));
        studentData.setStudentNum(CommonMethod.getString(form,"studentNum"));
        // 省略部分代码
        studentData.setEmail(CommonMethod.getString(form,"email"));
        return student.insertStudent(studentData);
    }
```

本例中，服务层首先取出请求体中的一个Map，之后建立一个空对象逐个取出Map中的内容。这种方式会导致代码量的增加，但好处在于可以保证后面的操作都是针对对象进行的，而对象的类对所有方法和类都是公开透明的，针对对象的操作最多最多取出一个`null`，但至少不会`NullPointerException`，具有更好的安全性和可读性，同时可以实现更好的业务抽象。

最后再给出一个简单的示例

```java
    /**
     * 删除学生信息
     *
     * @param dataRequest 请求内容
     */
    public void deleteStudent(DataRequest dataRequest){
        Integer id = dataRequest.getInteger("id");
        student.deleteStudent(id);
    }
```

从上面的几个例子来看，这种方式还有一个好处————便于修改维护。举个例子，如果要取出的字段由`id`变更为`studentId`，且存在较多的服务之间调用，在服务层进行取出操作可以仅修改一次就能实现修改的需求。

总体来讲，服务层进行的是一系列预处理，将面向http的请求体数据解包、打包为面向对象的对象，其代价是更多的代码量，换来的是更好的可移植性、可维护性和安全性。考虑到本项目的规模和需求，本组采用这种方式进行程序的设计。接下来，对象将在服务实现层执行具体逻辑。

#### 服务实现层实现增删改查逻辑

此处首先展示用于查询的方法

```java
    public List<Object> queryStudentMapList(String numName) {
        List<Object> result = new ArrayList<>();
        List<Student> studentList = studentRepository.findStudentListByNumName(numName);
        if (studentList == null || studentList.size() == 0) {
            return result;
        }
        Student student;
        Map<String, Object> tempMap;
        for (Student value : studentList) {
            student = value;
            tempMap = new HashMap<>();
            tempMap.put("id", student.getStudentId());
            tempMap.put("studentNum", student.getStudentNum());
            // 省略部分代码
            tempMap.put("age", student.getAge());
            tempMap.put("phoneNumber", student.getPhoneNumber());
            // 省略部分代码
            result.add(tempMap);
        }
        return result;
    }
```

在设计本方法时主要考虑两点：

1. 功能具有复用需求。上层对该方法的调用有三种情况，分别是查询所有、根据一个字段查询以及组合字段查询。
   
   > 此处所谓组合字段查询，是指前端可以通过`v-model`绑定一个或多个`input`和`select`形式的约束，此时需要在服务层对约束进行组合拼接在调用查询的方法。
   
    通过方法的封装，可以根据传入参数的内容调用数据操作层的同一个方法，减少代码的冗余。
2. 功能具有良好的独立性。在抽离成方法时，首先要考虑的如何进行参数和返回值的抽象，对于本功能来讲，其参数只需要一个字符串即可，返回值使用`List`作为容器进行装载，如果需要进一步处理可以在调用方法里进行处理，具有非常良好的抽象能力，属于是老天爷赏饭吃，不吃不行。

另外，如上面所示，本项目大部分使用了增强型的`for`循环，即使用`for (Class value : classObjectContainer)`的形式遍历容器内的对象，这样可以在语法层面省去手动声明对象引用变量和执行目标对象的过程，同时带来更好的可读性。

上面的代码实现的是对常用数据操作的一种封装，在服务实现层还有一类重要的操作：根据某些字段获取特定对象，本项目使用这种方式实现

```java
    private Student getStudent(Integer studentId) {
        Student student = null;
        Optional<Student> op;
        if (studentId != null) {
            op = studentRepository.findById(studentId);
            if (op.isPresent()) {
                student = op.get();
            }
        }
        return student;
    }
```

因为表中的数据通过主键进行唯一标识，该方法以及下面出现的一些方法作用和目的很清晰，就是通过`id`获取对应的对象。

本方法在接受`id`之后，首先是建立一个对象引用变量，并尝试进行查找；查找失败的情况下会返回空指针，这可以轻易的在调用方进行捕获。进一步查询时调用服务实现层继承的JPA的`CrudRepository`接口实现的`findById`方法即可轻松实现需求。但此处并没有使用泛型进行进一步抽象，主要是希望强调服务的隔离，同时保留一定自主性给出拓展空间。

以上方法可以实现多数与查询有关的需求，下面讨论添加的实现

```java
    public Integer insertStudent(@Valid Student studentData) {
        Student student = getStudent(studentData.getStudentId());
        Integer maxStudentId = null;
        if (student == null) {
            student = new Student();
            maxStudentId = studentRepository.getMaxId();
            if (maxStudentId == null) {
                maxStudentId = 1;
            } else {
                maxStudentId += 1;
            }
            student.setStudentId(maxStudentId);
        }

        student.setStudentNum(studentData.getStudentNum());
        student.setStudentName(studentData.getStudentName());
        // 省略部分代码
        studentRepository.save(student);
        return maxStudentId;
    }
```

此处的方法所接受的就是服务层封装后的对象，其内部同时转载两个同类对象，一个就是调用方传入的元数据，另一方是即将持久化的目标数据，这一方式可以提供一定自由修改的空间，将会在下面进一步介绍。除此以外，本方法的核心是对`maxId`字段的查询，其用处主要在于实现手动的主键自增，这是本项目早期使用SQLite的需求，理论上切换到MySQL后可以避免其使用。

可以看到确定对象的状态后，只需要调用其数据操作层的`save()`方法即可保存，这也是继承的`CrudRepository`所提供的能力，算是典型的ORM框架能力，将数据库表记录的添加抽象为对象的`save()`方法。

相似的，我们可以看一看对象——或者说记录——的删除操作：

```java
    public void deleteStudent(Integer studentId) {
        Student student = getStudent(studentId);
        if (student != null) {
            studentRepository.delete(student);
        }
    }
```

可以看到，在查询对象之后只需要调用`delete()`方法即可。

至此为止，单一对象的各种操作基本实现。

### 一对多关系维护时的差异

这一类需求在设计时，主要在于如何添加某个一方的多方。在这种情况下，核心在于为多方对象确定其链接的一方。对于CRUD来讲，主要的改动在于添加，我们需要让多方建立时持有一个一方的句柄，其次是删除时需要妥善处理级联方式，在某个多方被删除时需要考虑是否保留一方又或者相反情况

#### 添加多方状态的维护

此处以`EducationExxperience`为例来展示，首先需要注意实体类的生命

```java
// 省略部分代码
public class EducationExperience {
    // 省略部分代码
    @ManyToOne()
    @JoinColumn(name = "student_id")
    private Student student;
    // 省略部分代码
}
```
此处我们将`EducationExperience`类称为多方类，注意到他持有一个一方对象，通过这种组合的方式实现逻辑层面与一方的关联，也就是说当我们持有一个多方对象时，可以通过访问他的`.getStudent()`方法获得他的一方对象。

除此以外，这样的字段还需要有两个注解。其一是`@ManyToOne`，顾名思义用于指明对于多方类来讲存在多对一的关系；重点在于`@JoinColumn`注解，可以说它指定了连接方式。

首先我们需要知道，JPA对一对多、多对多关系在数据库表层面是通过外键实现的，在一对多的情况下就涉及到一个问题：这样的外键应该存在哪个类中。通常来讲，由于多方只需要持有一个一方对象，我们通常会将这个外键交给多方，也就是“由多方维护关系”，其在数据库表上的表现就是会有一个`student_id`字段记录它所连接的一方对象的主键，这样我们就可以实现二者在数据库层面上的连接。当然简单来讲，`@ManyToOne`其实就是用来指明外键的字段。

接下来，我们来看看一方

```java
    @OneToMany(mappedBy = "student",cascade =CascadeType.ALL,fetch = FetchType.LAZY)
    private Set<EducationExperience> educationExperiences;
```

如前面所说，一方需要持有一个多方的容器，此处使用集合实现。其重点在于`@OneToMany`注解，`mappedBy`用于放弃维护关系，这与多方类使用`@JoinCOlumn`是对应的：一方选择维护关系，另一方就要放弃。`cascade`用于声明级联，`fetch`忘了

通过这样的改动，就可以建立一个实体类和多个实体类之间的一对多关系。

#### 前期准备

此处本组的处理首先在服务实现层添加一个字段

```java
    /**
     * 保存相关studentId
     */
    private Integer studentId;
```

如注解所说。其作用就相当于所谓的“句柄”，使用这样一个主键保存其一方，随时可以拿来取用。至于这个id如何使用，首先要看下面的跳转

```java
    String educationExperienceParas = "model=educationExperience&studentId=" + student.getStudentId();
    Set<EducationExperience> educationExperiences = student.getEducationExperiences();
    tempMap.put("educationExperience", "共有" + educationExperiences.size() + "条教育经历");
    tempMap.put("educationExperienceParas", educationExperienceParas);
```

该方法利用前端提供的`link`类型，在由一方页面跳转到多方时携带一个一方的id保存在请求体内

```java
    /**
     * 获取所有
     *
     * @param dataRequest 请求内容
     * @return List
     */
    public List<Object> getAllEducationExperience(DataRequest dataRequest) {
        // 暂存studentId
        educationExperience.setStudentId(dataRequest.getInteger("studentId"));
        return educationExperience.queryEducationExperienceMapList();
    }
```

在多方的服务层，使用这样一行指令将id取出并set，即可在之后对多方的操作时保持这样一个联系

#### 修改多方添加逻辑

```java
    public Integer insertEducationExperience(EducationExperience educationExperienceData) {
        EducationExperience educationExperience = getEducationExperience(educationExperienceData.getEducationExperienceId());
        Integer maxEducationExperienceId = null;
        if (educationExperience == null) {
        // 省略部分代码
        educationExperience.setDescription(educationExperienceData.getDescription());

        Student relatedStudent;
        Optional<Student> opStudent = studentRepository.findById(studentId);
        if (opStudent.isPresent()) {
            relatedStudent = opStudent.get();
            educationExperience.setStudent(relatedStudent);
        }
        educationExperienceRepository.save(educationExperience);
        return maxEducationExperienceId;
    }
```

基于前面所说的准备，我们只需要额外使用上面几个语句查找`studentId`所指向的对象，并将其赋予`educationExperience`即可，在调用`save()`方法后即可保存关联的关系。

#### 修改多方删除逻辑

```java
    public void dropEducationExperience(Integer educationExperienceId) {
        EducationExperience educationExperience = getEducationExperience(educationExperienceId);
        Student relatedStudent;
        Optional<Student> opStudent = studentRepository.findById(studentId);
        if (opStudent.isPresent()) {
            relatedStudent = opStudent.get();
            relatedStudent.getEducationExperiences().remove(educationExperience);
        }
        educationExperienceRepository.delete(educationExperience);
    }
```

在删除时，我们所要删除的不只是多方对象本身，还需要删除“关系”。

也就是说尽管我们可以直接调用`delete()`方法删除，但一方所持有的集合仍然会持有这个被删除的对象，这会导致我们在获取一方持有的集合时出现空指针的问题。因此，在删除之前需要先删除关系，即调用`remove()`方法在集合内除去该对象，断开二者的联系，之后即可放心删除对象了。

### 多对多关系的实现

多对多关系的维护要相对复杂一些。

> 首先要明确一点，哪怕是JPA提供的`@ManyToMany`注解，在实际执行时也会建立一个名为`class_a_class_b`形式的中间表。

总的来说，多对多关系可以解释为多对一对多关系，也就是说对与两个具有多对多关系的对象，我们可以使用一个中间对象来描述二者关系，这个中间对象不具有实际意义，仅仅是一个桥梁。

我们可以拿Map来类比，众所周知Map存储的时k-v数据，我们可以通过key取出对应的value，这可以作为一种一对一关系，也可以说是映射的形式；我们还可以让几个key具有相同的value，这似乎就有些多对一的意思了；在此基础上，我们进一步延伸，可以使用两个Map A和B，使用keyA得到valueA，再将valueA作为keyB即可得到valueB，这种方式所实现的就与多对多比较相似。

下面以选课功能的实现为例来展开介绍。

#### 定义多对多关系

首先我们考虑，每个学生都会选择多个课程，那么不妨定义

```java
    @OneToMany(mappedBy = "student",cascade = CascadeType.ALL,fetch = FetchType.EAGER)
    private Set<CourseSelection> courseSelections;
```

同样，每门课程都会用多个学生选择，如下所示

```java
    @OneToMany(mappedBy = "course", cascade = CascadeType.ALL, fetch = FetchType.EAGER)
    private Set<CourseSelection> courseSelections;
```

可以看到，二者都持有一个`CourseSelection`类（下称中间类）的集合，这个类的作用就是连接二者实现多对多，我们可以看一下他的定义

```java
@Entity
@Table(name = "course_selection",uniqueConstraints = {@UniqueConstraint(columnNames = "course_selection_id")})
// 省略部分代码
public class CourseSelection {
    @Id
    @Column(name = "course_selection_id")
    private Integer courseSelectionId;
    @Column(name = "type")
    private  String type;
    @ManyToOne
    @JoinColumn(name = "course_id")
    private Course course;
    @ManyToOne
    @JoinColumn(name = "student_id")
    private Student student;
    // 省略部分代码
}
```

如上面所示，中间类主要负责持有两个对象并维护关系，也就是说他于其中一个类构成一对多关系，也与另一个类构成一对多关系。那么无论从哪个类进行操作，都可以通过`object.getCourseSlection().getAnotherObject()`这样的链式调用获取另一个对象，自然也就实现了多对多关系的维护。

在前面我们有提到，使用`@ManyToMany`注解同样可实现类似的效果，本组主要考虑以下两点而没有使用该注解

1. 编程人员会失去控制权。使用注解会将关系的维护完全移交给Spring Data JPA，导致编程人员无法确定其详细的调用逻辑，留下潜在的风险。
2. 缺少必要性，增加依赖性。由于这样的功能可以轻松实现，盲目使用注解会增加对框架的依赖，不利于后期开发或技术栈的迁移。
3. 具有拓展空间。如上面的代码，中间还可以顺便用来表明二者的关系，将中间类进行暴露可以留出更多操作空间，比如表明二者的连接性质。

#### 完善添加逻辑

就像刚才我们存了一个id，这里可以再存一个

```java
    public List<Object> getAllCourseSelection(DataRequest dataRequest) {
        try {
            courseSelection.setCourseId(dataRequest.getInteger("courseId"));
        } catch (NullPointerException nullPointerException) {
            SystemApplicationListener.logger.info("courseId设置失败");
        }
        try {
            courseSelection.setStudentId(dataRequest.getInteger("studentId"));
        } catch (NullPointerException nullPointerException) {
            SystemApplicationListener.logger.info("courseId设置失败");
        }
        return courseSelection.getCourseSelectionMapList();
    }
```

```java
    public Integer saveCourseSelection(CourseSelection courseSelectionData,
                                       Integer courseIdData, Integer studentIdData) {
        // 省略部分代码                                   
        Student student = null;
        Optional<Student> optionalStudent = studentRepository.findById(studentIdData);
        if (optionalStudent.isPresent()) {
            student = optionalStudent.get();
            courseSelection.setStudent(student);
        }
        Course course = null;
        Optional<Course> optionalCourse = courseRepository.findById(courseIdData);
        if (optionalCourse.isPresent()) {
            course = optionalCourse.get();
            courseSelection.setCourse(course);
        }
        courseSelection.setCourse(course);
        courseSelection.setStudent(student);
        courseSelectionRepository.save(courseSelection);
        return maxCourseSelectionId;
    }
```

上面的处理其实都是相似的，这里的重点在于用户通过其中一方开始操作，该如何选择要添加的另一个对象。本作品在几次迭代后，通过查询的方式获取满足条件的数据返回前端，前端生成一个下拉选项菜单进行选择，这部分逻辑被定义在有关初始化的方法里

```java
    if (courseSelection != null) {
        resultMap.put("id", courseSelection.getCourseSelectionId());
        // 省略部分代码
        resultMap.put("courseIdList", courseIdList);
    } else {
        List<Object> studentIdList = new ArrayList<>();
        if (studentId != null) {
            Student student;
            Optional<Student> optionalStudent = studentRepository.findById(studentId);
            if (optionalStudent.isPresent()) {
                student = optionalStudent.get();
                Map map = new HashMap<>();
                map.put("label", student.getStudentName());
                map.put("value", student.getStudentId());
                studentIdList.add(map);
                resultMap.put("studentId", "");
                resultMap.put("studentIdList", studentIdList);
            }
        } else {
            List<Student> studentList = studentRepository.findAll();
            Map map;
            for (Student value : studentList) {
                map = new HashMap<>();
                map.put("label", value.getStudentName());
                map.put("value", value.getStudentId());
                studentIdList.add(map);
            }
            resultMap.put("studentId", "");
            resultMap.put("studentIdList", studentIdList);
        }
        List<Object> courseIdList = new ArrayList<>();
        if (courseId != null) {
            Course course;
            Optional<Course> optionalCourse = courseRepository.findById(courseId);
            // 省略部分代码
            resultMap.put("courseId", "");
            resultMap.put("courseIdList", courseIdList);
        }
    }
```

可以看到，由于两个id初始化都被置为`null`，因此可以通过分支语句进行情况分类；接下来获取另一个类的所有对象填充到`List`中，并将其返回对应的字段即可实现选择的功能。这种处理具有良好的交互性，而且前端可以直接返回两个对象的id，不需要对后台逻辑进行过于复杂的修改。

#### 完善删除和其他逻辑

对于删除功能的修改同样是类比即可，并不复杂

```java
    public void deleteCourseSelection(Integer courseSelectionId) {
        CourseSelection courseSelection;
        Optional<CourseSelection> op;
        if (courseSelectionId != null) {
            op = courseSelectionRepository.findById(courseSelectionId);
            if (op.isPresent()) {
                courseSelection = op.get();
                Course relatedCourse;
                Optional<Course> opCourse = courseRepository.findById(courseSelection.getCourse().getCourseId());
                if (opCourse.isPresent()) {
                    relatedCourse = opCourse.get();
                    relatedCourse.getCourseSelections().remove(courseSelection);
                }
                Student relatedStudent;
                Optional<Student> opStudent = studentRepository.findById(courseSelection.getStudent().getStudentId());
                if (opStudent.isPresent()) {
                    relatedStudent = opStudent.get();
                    relatedStudent.getCourseSelections().remove(courseSelection);
                }
                courseSelectionRepository.delete(courseSelection);
            }
        }
    }
```

### 绩点计算与排名

对于一个学生管理系统，成绩、绩点的计算以及排名都是很有必要的功能。

#### 实现方式及思路

本项目考虑到绩点的计算需要大量磁盘IO遍历数据，当受到大量请求时显然会给服务器带来很大的压力。基于这个考虑，本作品使用缓存的方式，定时计算成绩，在接受到请求后使用数据与缓存数据对撞取出满足条件的信息即可。

这种实现具有一定难度，首先我们需要引入Redis这个常用的内存数据来作为缓存；其次，本项目考虑将每个课程的成绩排名列表、总成绩的成绩排名列表进行缓存；除此以外，本作品设计了几个DTO用来包装数据，比如某个DTO中包含平均、GPA等等。

接下来进行展示

#### Redis的基本配置与序列化的准备

首先是对Redis的简单配置

```
spring.redis.database=0
spring.redis.host=*****
spring.redis.port=6379
spring.redis.password=****
```

除此以外，本组将所有对象进行序列化后存储。因此这里还需要提供一个序列化、反序列化的工具类，这样的类时依附于`DTO`类，可以通过一些分隔符对字段进行分隔后保存。此处给出一个示例

```java
public class TotalRankSerializator {
    public static String serializeTotalRank(TotalRankDTO totalRankDTO) {
        String result = totalRankDTO.getAverageScore() + ":";
        // 省略部分代码
        result = result + totalRankDTO.getSameScoreNum();
        return result;
    }

    public static TotalRankDTO deserializeTotalRank(String str) {
        TotalRankDTO totalRankDTO = new TotalRankDTO();
        String stringDelimiter = ":";
        String[] temp = str.split(stringDelimiter);
        // 省略部分代码
        totalRankDTO.setSameScoreNum(Integer.parseInt(temp[3]));
        return totalRankDTO;
    }
}
```

除此以外，我们还需要给每个`DTO`类定义一个`Comparator`用于`ArrayList`的`sort()`方法使用。它需要继承`Comparator<T>`并`override`继承的`comparator`方法以定义比较逻辑，比如说

```java
public class TotalScoreComparator implements Comparator<TotalScoreDTO> {
    @Override
    public int compare(TotalScoreDTO o1, TotalScoreDTO o2) {
        return o2.getAverageScore().compareTo(o1.getAverageScore());
    }
}
```

总的来说，本项目设计的`DTO`类基本都需要一个序列化、反序列化工具类和`Comparator`以实现业务需求。

#### 成绩、排名获取方式

首先考虑对于每一门课程的成绩

实现逻辑比较简单，首先我们遍历所有的课程，然后对某个课程进行操作

对于这样一个课程，我们取出他所持有的所有成绩的集合，建立若干个`DTO`对象对成绩进行二次封装；在此基础上得到一个列表，调用`ArrayList`的`sort()`方法，根据自定义比较器进行一次排序即可得到该课程下自高至低的所有成绩的列表。在此基础上，我们继续进行一次遍历，给该列表的每个对象赋予排名信息等，即可得到该门课程完整的所有成绩的信息。在此之后，我们对列表中的所有元素进行序列化，然后即可作为list存入Redis。

以下展示某个课程列表的实现方法

```java
    /**
     * 用来获取某门课程的所有学生的成绩并进行排序
     *
     * @param course 课程
     * @return CourseRankDTO的列表，包含排名和百分比
     */
    public List<CourseRankDTO>  getCourseRankList(Course course) {
        List<Score> scoreList = new ArrayList<>(course.getScores());
        List<CourseRankDTO> courseRankDTOList = new ArrayList<>();
        for (Score value : scoreList) {
            courseRankDTOList.add(new CourseRankDTO(0, 0.0, value.getScore(), 0));
        }
        courseRankDTOList.sort(new CourseRankComparator()); // 排序
        int sameScoreNum = 1;
        int size = courseRankDTOList.size();
        for (int i = 0; i < size; i++) { // 遍历这一门课程下的所有成绩记录，从而得到该门课程的排名
            courseRankDTOList.get(i).setRank(i + 1);
            if ((i > 1) && courseRankDTOList.get(i).getScore().equals(courseRankDTOList.get(i - 1).getScore())) {
                sameScoreNum += 1;
            } else {
                sameScoreNum = 1;
            }
            courseRankDTOList.get(i).setSameScoreNum(i);
            courseRankDTOList.get(i).setPercent((courseRankDTOList.get(i).getRank() + 1 - sameScoreNum + 1) / (double) size);
        }
        List<String> serializedCourseRankDTO = new ArrayList<>(); // 序列化
        for (CourseRankDTO value : courseRankDTOList) {
            serializedCourseRankDTO.add(CourseRankDTOSerializator.serializeCourseRankDTO(value));
        }
        try {
            globalScoreRepository.drop("course:" + (course.getCourseId() - 1));
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
        globalScoreRepository.leftPushStringList("course:" + (course.getCourseId() - 1), serializedCourseRankDTO);
        try {
            globalScoreRepository.drop("courseTime:" + (course.getCourseId() - 1));
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
        globalScoreRepository.setString("courseTime:" + (course.getCourseId() - 1), DateUtil.now().toString());
        return courseRankDTOList;
    }
```

在此基础上，我们只需要进行一次所有课程的遍历即可将所有课程的信息获得。我们可以使用`findAll()`方法获得所有的对象，然后对列表中的所有元素执行上面定义的方法，比如

```java
    List<Course> courseList = courseRepository.findAll();
    for (Course value : courseList) {
        if (value.getScores() != null && value.getScores().size() != 0) {
            score.getCourseRankList(value);
        }
    }
```

基于上面的信息，我们可以进一步获取每个学生的成绩。但是我们还需要一个获得某个学生所有成绩的方法。

我们可以先获取某个学生的所有成绩，基于这个成绩的分数和课程，在对应的课程所有成绩内取出这个分数所对应的信息，对该学生所有课程进行遍历后即可计算该学生的平均绩点等信息。以下展示获取某个学生的成绩的方法

```java
    /**
     * 获取指定学生所有课程的排名
     *
     * @param courseScoresDTOList 学生的成绩DTO列表
     * @return 更新后的成绩DTO列表
     */
    public List<CourseScoresDTO> getRankForCoursesForStudent(List<CourseScoresDTO> courseScoresDTOList) {
        for (CourseScoresDTO courseScoresDTO : courseScoresDTOList) {
            Optional<Course> op = courseRepository.findById(courseScoresDTO.getCourseId());
            if (op.isPresent()) {
                Course course = op.get();
                List<CourseRankDTO> courseRankDTOList = new ArrayList<>();
                try {
                    List<String> tempList = globalScoreRepository.getAllRange(String.valueOf(course.getCourseId() - 1));
                    for (String value : tempList) {
                        courseRankDTOList.add(CourseRankDTOSerializator.deserializeCourseRankDTO(value));
                    }
                } catch (Exception e) {
                    SystemApplicationListener.logger.warn("取出缓存失败！");
                    SystemApplicationListener.logger.warn(String.valueOf(e));
                }
                CourseRankDTO courseRankDTO = score.getCourseRank(courseRankDTOList, courseScoresDTO.getScore());
                SystemApplicationListener.logger.info("打印学生的排名信息");
                SystemApplicationListener.logger.info(courseRankDTO.toString());
                courseScoresDTO.setCourseRankDTO(courseRankDTO);
            }
        }
        return courseScoresDTOList;
    }
```

在此基础上，我们还可以提供一个方法进行学生的遍历，并对该集合每个元素调用上面的方法，比如

```java
    /**
     * 获取所有学生的总成绩
     *
     * @return 学生总成绩的列表
     */
    public List<TotalScoreDTO> getScoresForAllStudents() {
        List<TotalScoreDTO> totalScoreDTOList = new ArrayList<>();
        List<Student> studentList = studentRepository.findAll();
        for (Student value : studentList) {
            List<CourseScoresDTO> scoresDTOList = getScoresForStudent(value);
            TotalScoreDTO totalScoreDTO = new TotalScoreDTO();
            if (scoresDTOList != null && scoresDTOList.size() != 0) {
                AverageScoreDTO averageScoreDTO = getAverageScoreForCoursesForStudent(getRankForCoursesForStudent(scoresDTOList));
                totalScoreDTO.setAverageScore(averageScoreDTO.getAverageScoreForAll());
            } else {
                totalScoreDTO.setAverageGPA(0.0);
                totalScoreDTO.setAverageScore(0.0);
            }
            totalScoreDTOList.add(totalScoreDTO);
        }
        return totalScoreDTOList;
    }
```

值得注意的是，上面得到的信息同样是不含有排名的。因此所以我们接下来要做的就是对所有成绩进行排名，在进行排序后即可对每个元素进一步补充数据，最终得到完整的一个列表，对该列表进行序列化的处理后放入Redis缓存备用。可以看出，其实这与计算某门课程的成绩并无太大区别，只是有更多的遍历循环逐个进行计算

```java

    /**
     * 获得所有学生的排名
     *
     * @param totalScoreDTOList 学生总成绩的列表
     * @return 加入排名信息后的学生总成绩的列表
     */
    public List<TotalScoreDTO> getRanksForAllStudents(List<TotalScoreDTO> totalScoreDTOList) {
        totalScoreDTOList.sort(new TotalScoreComparator());
        int size = totalScoreDTOList.size();
        int sameScoreNum = 1;
        for (int i = 0; i < totalScoreDTOList.size(); i++) {
            TotalRankDTO totalRankDTO = new TotalRankDTO();
            totalRankDTO.setRank(i + 1);
            totalRankDTO.setPercent((i + 1) / (double) size);
            totalRankDTO.setAverageScore(totalScoreDTOList.get(i).getAverageScore());
            if (i > 0 && (totalScoreDTOList.get(i).getAverageScore().equals(totalScoreDTOList.get(i - 1).getAverageScore()))) {
                sameScoreNum += 1;
            } else {
                sameScoreNum = 1;
            }
            totalRankDTO.setSameScoreNum(sameScoreNum);
            totalScoreDTOList.get(i).setTotalRankDTO(totalRankDTO);
            SystemApplicationListener.logger.warn(totalScoreDTOList.get(i).toString());
        }
        try {
            globalScoreRepository.drop("totalRank");
            SystemApplicationListener.logger.info("清空原有全部排名");
        } catch (Exception e) {
            SystemApplicationListener.logger.info(e.toString());
        }
        List<String> totalRankDTOList = new ArrayList<>();
        for (TotalScoreDTO value : totalScoreDTOList) {
            totalRankDTOList.add(TotalRankSerializator.serializeTotalRank(value.getTotalRankDTO()));
        }
        globalScoreRepository.leftPushStringList("totalRank", totalRankDTOList);
        return totalScoreDTOList;
    }
```

当然，上面的一些方法并非是一环套一环耦合的。

本组建立一个`ScheduledService`，用于保存所有需要定时执行的事务。

首先要对每门课程进行计算，我们定义一个这个样子的方法，在服务启动后一段时间进行计算，顺便打印一下log，示例

```java
    /**
     * 系统启动一分钟后计算所有课程的成绩列表
     * 之后每三分钟刷新一次
     */
    @Scheduled(initialDelay = MicroSecondsPerMinute, fixedDelay = 3 * MicroSecondsPerMinute)
    public void refreshCourseRank() {
        SystemApplicationListener.logger.info("Begin refresh course rank>>>" + DateUtil.now());
        List<Course> courseList = courseRepository.findAll();
        for (Course value : courseList) {
            if (value.getScores() != null && value.getScores().size() != 0) {
                score.getCourseRankList(value);
            }
        }
        SystemApplicationListener.logger.info("Finish refresh course rank>>>" + DateUtil.now());
    }
```

这样我们就可以获得一个动态刷新的课程成绩缓存

> 值得一提的是，此处定时事务注解`@Scheduled`指定了`fixedDelay`属性，他的特点是在该方法执行结束后才开始计时，这样能够避免数据的冲突。

同样的道理，我们可以进一步定义一个定时事务去求解所有同学的总成绩排名

```java
    @Scheduled(initialDelay = 2 * MicroSecondsPerMinute, fixedDelay = 3 * MicroSecondsPerMinute)
    public void refreshTotalRank() {
        SystemApplicationListener.logger.info("Begin refresh total rank>>>" + DateUtil.now());
        List<Student> studentList = studentRepository.findAll();
        for (Student value : studentList) {
            SystemApplicationListener.logger.info(value.toString());
        }
        List<TotalScoreDTO > totalScoreDTOList = globalScoreService.getScoresForAllStudents();
        totalScoreDTOList = globalScoreService.getRanksForAllStudents(totalScoreDTOList);
        for (TotalScoreDTO value : totalScoreDTOList) {
            SystemApplicationListener.logger.info(value.toString());
        }
    }
```

可以看到，这个方法非常明显地体现了对前述几个方法的调用和整合，同时又保证了每个方法的独立性，有效降低方法之间的耦合度。因此，下面进行简历数据的处理的时候同样调用一部分方法，由此可以看出本作品功能之间具有较为良好的独立性和可复用性。

### 简历业务的实现

对于个人简历业务的处理，此处略过Web层的分析，首先在服务层调用服务实现层的方法获得学生对象，该对象将会在后面面反复使用，可以说他是整个子业务的核心与灵魂

```java
    /**
     * 获取学生对象
     *
     * @param studentId 学生Id
     * @return 返回对象
     */
    public Student getStudent(Integer studentId) {
        SystemApplicationListener.logger.warn("getStudent:" +studentId.toString());
        Student student = null;
        Optional<Student> op;
        op = studentRepository.findById(studentId);
        if (op.isPresent()) {
            student = op.get();
        }
        return student;
    }
```

在此之后，如前面所说，我们需要获得某个学生的成绩，因此这里还需要考虑一些方法。首先是如何获取指定科目的成绩。

由于缓存在Redis中，本质上讲使用一个Map存放数据，因此这里只需给出一个成绩，由于Map是基于一个红黑二叉树实现的，此处可以实现毫秒级的查询速度，代码大概是这个样子

```java
    /**
     * 基于课程的所有排名，根据成绩匹配其排名
     *
     * @param courseRankDTOList 包装后的成绩列表
     * @param score             需要查询的成绩
     * @return 返回对应的CourseRankDTO
     */
    public CourseRankDTO getCourseRank(List<CourseRankDTO> courseRankDTOList, Integer score) {
        for (CourseRankDTO value : courseRankDTOList) {
            if (score.equals(value.getScore())) {
                return value;
            }
        }
        return new CourseRankDTO();
    }
```

相应的，还需要一个方法取出该学生的总成绩和排名信息，其原理也是相似的

```java
    /**
     * 获取某个学生的排名信息
     *
     * @param score 学生的成绩
     * @return 排名信息DTO
     */
    public TotalRankDTO getStudentForStudent(Double score) {
        List<TotalRankDTO> totalRankDTOList = new ArrayList<>();
        List<String> serializedTotalRank = globalScoreRepository.getAllRange("totalRank");
        for (String str : serializedTotalRank) {
            totalRankDTOList.add(TotalRankSerializator.deserializeTotalRank(str));
        }
        for (TotalRankDTO value : totalRankDTOList) {
            if (value.getAverageScore().equals(score)) {
                return value;
            }
        }
        return new TotalRankDTO();
    }
```

此处需要补充一些对前端的介绍，基于已有的前端，我们对此进行了一些功能的添加。首先是对于基本信息的一些完善，比如

```html
<div
  class="item"
  style="
    display: flex;
    flex-direction: column;
    align-content: center;
    align-items: start;
  "
>
  <div>姓名： {{ myName }}</div>
  <div>性别： {{ sex }}</div>
  <div>年龄： {{ age }}</div>
  <div>学院专业： {{ overview }}</div>
  <div>学号： {{ studentNum }}</div>
  <div>联系方式： {{ contact }}</div>
</div>
```

针对每个人的成绩，我们使用一个雷达图进行展示。图像的绘制基于`vue-charts`组件，图表支持动画以及动态调整，能够十分形象的展示数据，前端部分主要由这几个语句构建

```html
<el-card class="box-card">
  <div
    style="
      display: flex;
      flex-direction: column;
      align-content: center;
      align-items: center;
    "
  >
    <div class="card-header;margin-bottom:36px">{{ myName }}的综合成绩分布</div>
    <Radar
      v-if="studyChartLoaded"
      :chart-options="studyChartOptions"
      :chart-data="studyChartData"
      :chartId="studyChartId"
      style="width: 400px"
    />
  </div>
</el-card>
```

后端需要提供两个列表，分别保存`label`和每个科目的成绩数据，其逻辑如下

```java
/**
     * 获取学生的所有成绩信息
     *
     * @param student             学生对象
     * @param courseScoresDTOList 学生的所有成绩列表
     * @return 图表数据DTO
     */
    public ChartInformationDTO getStudyChartInformation(Student student, List<CourseScoresDTO> courseScoresDTOList) {
        ChartInformationDTO chartInformationDTO = new ChartInformationDTO();
        List<String> studyChartLabels = new ArrayList<>();
        List<Object> studyChartDatasets = new ArrayList<>();
        Map<String, Object> datasetItem = new HashMap<>();
        List<Integer> datasetItemData = new ArrayList<>();
        for (CourseScoresDTO value : courseScoresDTOList) {
            studyChartLabels.add(value.getCourse());
            datasetItemData.add(value.getScore());
        }
        datasetItem.put("data", datasetItemData);
        // 掠过部分代码
        datasetItem.put("borderColor", "#79bbff");
        studyChartDatasets.add(datasetItem);
        chartInformationDTO.setLabels(studyChartLabels);
        chartInformationDTO.setDatasets(studyChartDatasets);
        return chartInformationDTO;
    }
```

同理，我们还可以的到另一个图表，这里不做赘述。

下一步，建立一个生成器来解析渲染其他内容，这样一个生成器每个单元由`title`和`content`两个字段组成，默认将会在同一行显示。`content`中的内容通常使用`StringBuilder`生成并使用`<div>`标签包裹、`</br>`标签表明换行，前端部分逻辑如下所示

```html
<div
  class="item"
  style="
    display: flex;
    flex-direction: column;
    align-content: start;
    align-items: start;
  "
>
  <el-row
    type="flex"
    style="margin-left: 12px; margin-right: 12px; width: 100%"
    :gutter="110"
    v-for="(item, i) in attachList"
    :key="i"
  >
    <div class="paragraph-header">{{ item.title }}</div>
    <div v-html="item.content"></div>
  </el-row>
</div>
```

后端信息的填充基本是下面的形式

```java
m = new HashMap<>();
m.put("title", "--------");
m.put("content", "");
attachList.add(m);
m = new HashMap<>();
m.put("title", "教学活动");
m.put("content", "");
attachList.add(m);
pdfInfo.add(m);

m = new HashMap<>();
m.put("title", "实践信息");
StringBuilder practiceInformation = new StringBuilder("<div>");
for (Practice value : student.getPractices()) {
    practiceInformation.append(value.toString());
    practiceInformation.append("</br>");
}
practiceInformation.append("</div>");
m.put("content", practiceInformation.toString());
attachList.add(m);
```

基于上面的内容，我们就可以得到一份图文并茂的简历页。

### 服务部署

#### Nginx配置

Nginx是一个高效稳定、使用广泛的Web和反向代理服务器，本项目使用它作为Web服务器，此处略过其安装过程，最终配置文件的主要部分为

```sh
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www;

	index index.html;

	server_name localhost;

	location / {
		root /var/www/hexo;
		index index.html index.htm;
		try_files $uri $uri/ =404;
	}

	location /blog {
		alias /var/www/hexo;
		add_header 'Access-Control-Allow-Origin' '*';
		index index.html index.htm;
	}

	location /java {
		alias /var/www/java_course;
		index index.html;
	}
}
```

域名下二级站点`/java`将只指向本作品的前端`index.html`文件启动服务，Nginx将持续监听80端口的请求。

使用以上配置即可实现对前端界面的访问。但是前端对后端的请求和访问是另一个新的问题，此处会有一个我们所谓的跨域问题。

#### 跨域问题的解决

首先需要在后端`controller`类头上声明`@CrossOrigin(orgin="*")`注解，前端直接请求服务器域名，并对Nginx加入以下配置

```sh
location /api/ {
		proxy_redirect off;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_pass http://127.0.0.1:9090;
		proxy_buffer_size 64k;
		proxy_buffers 32 32k;
		proxy_busy_buffers_size 128k;
	}
```

该配置将形如`~/api`的请求进行转发，代理到本机的`127.0.0.1:9090`端口，并将请求得到的结果返回给请求方。由此配置杰克完成前后端在一台服务器上的部署。

## 总结体会

### 郭苏睿

本次课设我学习到一般后端服务的架构思路以及Spring框架的一些思想，能够将分层思想应用到单体应用的设计中，得到耦合度低、可复用能力强的应用架构。掌握了MySQL和Redis的入门知识，进一步加深对SQLite数据库的认识。具备了从需求分析、应用设计和具体实现再到使用Maven编译jar包部署到服务器。Git的理解和使用更深了一步，逐渐掌握大型工程的管理和控制。了解了关于UML图的知识，在与他人交流、文件撰写时效率更高。

### 何硕

我在本次课设中学到了很多的东西，比如各种类表的绘制，数据库的使用；如何提高编程效率、设计算法的技巧；如何高效使用工具来寻找资源，用科学分类的方法管理文档，养成了良好的代码规范，形成了规范的代码意识。

在做课设时，写sql表时，刚开始非常不习惯，看表时很奇怪，但随着学习的深入我看懂了，并应用了到实践中了，我又多会了一门语言。  

### 胡钊

本次课设我学会了网络协作编程，对于类之间的关系有了更加深刻的认识，也明白了类的可见性在编程中的重要性。对于接口的认识更加深刻。在查找资料的过程中，学会了JavaScript的基本内容，熟练了yaml语言的基本语法，学会了数据库的互连与互通，通过对于数据库的学习，我也对基本的数据结构有了大致的理解，也学会了与之相关的方法。学会了通过git实现多人编程。提高了阅读代码的能力，也养成了编写注释的习惯。也学会了绘制简单的UML类图，对于I/O流，“多线程”“一对多““多对多”等概念的理解更加深刻。

### 吕俊安

本次课程设计是我第一次参与设计真正的编程项目。在本次课设中，我认识到了代码风格习惯规范的重要性，意识到了积极、规范撰写注释的必要性，也认识到了代码安全的重要性。在本次课设中，我体验了通过网络协作编程的过程，熟悉了应用程序软件架构模型和应用模式的结构，巩固了Java语言的语法结构，更加深刻地认识了类的可见性和静态等特性对程序项目结构的影响，学习了有关数据库的常用操作和yaml语言的基本语法。同时，在本次课设中，我对通过算法和数据结构优化程序时空复杂度有了新的认识，更加清晰地了解程序中为追求更好地用户体验而对程序某些细节所作的妥协，通过在设计时对哈希表、红黑树、链表、trie树、哈夫曼编码等数据结构的取舍，让我认识到了程序设计时所需要综合考虑的各种问题。除此之外，我对Java Spring、IO流和文件以及socket网络编程等技术也有了了解。
