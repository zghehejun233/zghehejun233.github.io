---
title: Java知识点总结
categories: 编程
description: Java的深入学习笔记，更新应试笔记
tags:
  - Java
abbrlink: d842f132
date: 2021-12-20 21:48:16
---

## 特点

1. Java源程序和源文件中的字母都大小写敏感

2. Unicode编码每个Unicode码占用16bits(2bytes)

3. **数组也是对象**

4. 如果Java源文件中包含了多个类，那么用编译器javac编译完源文件后将生成多个扩展名为.class的文件。

5. 一个Java源文件中可以有多个类，但只能有一个类是public的

>   1.每个编译单元（文件）都只能有一个public类，这表示，每个编译单元都有**单一的公共接口**，用public类来表现。该接口可以按要求包含众多的支持包访问权限的类。如果在某个编译单元内有一个以上的public类，编译器就会给出错误信息。
>   2.public类的名称必须完全**与含有该编译单元的文件名相同**，包含大小写。如果不匹配，同样将得到编译错误。
>   3.虽然不是很常用，但编译单元内完全不带public类也是可能的。在这种情况下，可以随意对文件命名。

6. 类（如：System、Scanner、String），它们都是一种数据类型。
7. 在Java中，负责对字节代码解释执行的是JVM
8. Java有三种注释形式，其中/\*\*content/形式可以使用javadoc直接生成外部的注释文档
9. If this source code is contained in a file called SmallProg.java, what command should be used to compile it using the JDK?：**javac SmallProg**

### Java关键字

1. 两个关键字

   | 保留字 | 备注                                                         |
   | ------ | ------------------------------------------------------------ |
   | goto   | 指定跳转到标签，找到标签后，程序将处理从下一行开始的命令。   |
   | const  | 用于修改字段或局部变量的声明。它指定字段或局部变量的值是常数，不能被修改 |

2. 权限控制

   | 关键字    | 备注           |
   | --------- | -------------- |
   | public    |                |
   | protected |                |
   | private   | 不能用来声明类 |
   | default   |                |
   > https://stackoverflow.com/questions/2534733/java-protected-classes
   > https://www.codenong.com/3869556/


3. 定义与实例化

   | 关键字     | 备注                                               |
   | ---------- | -------------------------------------------------- |
   | class      | 包含方法体和具体实现，public类名要和文件名保持一致 |
   | interface  | 仅含有方法体，没有具体实现                         |
   | abstract   |                                                    |
   | implements | 对接interface实现方法体                            |
   | extends    |                                                    |
   | new        |                                                    |

4. 包

   | 关键字  | 备注 |
   | ------- | ---- |
   | import  |      |
   | package |      |

5. 数据类型

   | 关键字  | 备注                       |
   | ------- | -------------------------- |
   | byte    | 8bit                       |
   | char    | 16bit（Unicode）           |
   | boolean |                            |
   | short   | 16bit                      |
   | int     | 32bit                      |
   | float   | 32bit（注意声明时附加f/F） |
   | long    | 64bit                      |
   | double  | 64bit                      |
   | void    |                            |
   | null    |                            |
   | true    |                            |
   | false   |                            |

6. 流程控制

   | 关键字     |      |
   | ---------- | ---- |
   | if         |      |
   | else       |      |
   | while      |      |
   | for        |      |
   | switch     |      |
   | case       |      |
   | default    |      |
   | do         |      |
   | break      |      |
   | continue   |      |
   | return     |      |
   | instanceof |      |

7. 修饰符

   | 关键字       |                                                              |
   | ------------ | ------------------------------------------------------------ |
   | static       | 只有内部类可以使用static关键字修饰，调用直接使用类名.内部类类名进行调用。可以修饰成员变量为全局静态成员变量（class variable） |
   | final        | final修饰的类是不能被继承的 ，final修饰的方法是不能被子类重写。 |
   | super        | 调用父类的方法                                               |
   | this         | 从本质上讲，this是一个指向本对象的指针, 然而super是一个Java关键字 |
   | native       |                                                              |
   | stricfp      |                                                              |
   | synchronized |                                                              |
   | transient    |                                                              |
   | volatile     |                                                              |

8. 异常处理

   | 关键字  |                                  |
   | ------- | -------------------------------- |
   | catch   |                                  |
   | try     | 捕获异常                         |
   | finally |                                  |
   | throw   | 执行抛出异常的动作               |
   | throws  | 将异常抛给调用者，自己不进行管理 |

9. 其他

   | 关键字 | 备注 |
   | ------ | ---- |
   | enum   |      |
   | assert |      |

> https://blog.csdn.net/sdujava2011/article/details/71404165


## 数据类型和数组

1. 程序运行中不可以改变数组的大小。
1. Java允许创建不规则数组，即Java多维数组中各行的列数可以不同。

> https://blog.nowcoder.net/n/110dd0ea457949eab99ad0f0fe7477b5

3. boolean型数据的值只有true和false
4. Java语言对语法要求严格，局部变量只有在定义、赋初值后才能访问。**局部变量没有默认值**，所以局部变量被声明后，必须经过初始化，才可以使用

> https://www.runoob.com/java/java-variable-types.html

5. Java中，boolean基本类型的变量不能取值为0/1
6. 由低精度的数据类型向高精度的数据类型赋值时，是自动类型转换，其数值不变
7. After the declaration: char[] c = new char[100]; the value of c[50]：'\u0032'
8. **boolean类型不能为null**，且不能和其他基本数据类型互转
9. Java默认所有浮点型数据都是double，必须通过f/F强制声明float *（奢侈啊奢侈）*
10. 枚举变量必须要定义在类层次上，被认为是一个安全的类型

>枚举型变量是一种特殊的类，枚举型变量是对象变量。每个枚举值被保存为对应的整型数
>存在相关的几个方法，ordinal()返回与该枚举值关联的序数值，name()返回枚举值的名称

11. Java中数组时引用数据类型，而String是对象，所以对于数组只需要用**.length调用数据类型的length属性**，但String需要调用.length()方法

12. Java提供了包装器类（wrapperClass）进行基本数据类型的包装

13. Java没有unsigned标识符

14. Why do variables declared in a class have default values, but the variables declared inside methods, said to be "local variables", don't have default values in Java?

    >All **member variable have to load into heap** so they have to initialized with default values when an instance of class is created. In case of local variables, they don't get loaded into heap they are stored in stack until they are being used before java 7, so we need to explicitly initialize them. Now the "Java Hotspot Server Compiler" performs "escape analysis" and decides to allocate some variables on the stack instead of the heap.
    >
    >Variables declared in methods and in blocks are called local variables. Local variable are not initialized when they are created at method invocation. Therefore, a local variable must be initialized explicitly before being used. Otherwise the compiler will flag it as error when the containing method or block is executed.



## 运算符

1. 关于短路运算符
2. 注意自增运算符的前后置，但是利用这个特性写代码会被杀
3. 注意优先级上逻辑非>逻辑与>逻辑或
4. ==是Java的一个关系运算符，它的作用是判断两者是否相等，具体的作用方式是**直接判断值**是否相等。

>对于基本数据类型来说，由于基本数据类型变量存储的都是原始值，==在判断变量是否相等时也是**直接比较变量的值**，所以如果基本变量的原始值相同，那么这两个变量使用==判断就输出true
>对于引用数据类型，也可以使用”==“来判断，由于引用数据类型变量存储的是引用对象的地址，所以使用==来比较两个引用数据类型变量，实际上是在**比较这两个引用变量是否引用了同一个对象**

3. 对于private修饰符，其修饰的都是Class层次的内容，比如method和class parameter、instance parameter

### 转义序列

| 转义序列 | 意义   |
| -------- | ------ |
| \b       | 退格符 |
| \t       | 制表符 |
| \n       | 换行符 |
| \r       | 回车符 |
| \\'      |        |
| \\"      |        |
| \\       |        |


## 流程控制

## 类与对象

1. Java只支持类之间的单继承，但是可以使用接口来实现多继承
1. 声明对象引用变量是在stack存储一个地址，初始值为null。在stack中查找速度快。new关键字能够在heap中开辟对应的内存空间，并将地址交给某个对象引用变量。

> https://www.jianshu.com/p/39c6ecc1b184
> https://zhuanlan.zhihu.com/p/53846258

3. 特别的，Java对String特殊处理。

3. memory space for a **static variable** is created when the class is first created

3. static methods can't reference the instance variables

###  关于static关键字

   > 动态是指Java程序在JVM上运行时，JVM会根据程序的需要动态创建对象并存储对象(分配内存)，对象使命结束后，对象会被垃圾回收器销毁，即内存回收由JVM统一管理并分配给其他新创建的对象；静态是指Java程序还没有运行时，**JVM就会为加载的类分配空间存储被static关键字修饰的内容**；如静态成员变量，Java类加载到JVM中，JVM会把类以及类的静态成员变量存储在方法区，我们知道**方法区是线程共享且很少发生GC的区域**，所以被**static关键字修饰的内容都是全局共享**的，且只会为其分配一次存储空间。

   1. 修饰静态代码块 
   - 静态代码块是当Java类加载到JVM内存中而执行的代码块，由于类的加载在JVM运行期间只会发生一次，所以静态代码块也只会执行一次。
   - 静态代码块的主要作用是用来进行一些**复杂的初始化工作**，所以静态代码块跟随类存储在方法区的表现形式是静态代码块执行的结果存储在方法区，即初始化量存储在方法区并被线程共享。
	 2. 修饰成员变量
	 - 静态变量存储在类的信息中，且可以在线程间共享，那么它当然也属于该类的每个对象，因此可以通过对象访问静态变量，但编译器并不支持这么做，且会给出警告。
	 - 一个类的静态变量和该类的静态代码块的加载顺序。类会优先加载静态变量，然后加载静态代码块，但有多个静态变量和多个代码块时，会按照编写的顺序进行加载。
	 - 静态变量可以不用显式的初始化，JVM会默认给其相应的默认值。
	 - 静态变量既然是JVM内存中共享的且可以改变，那么对它的访问会引起线程安全问题。如果能确保静态变量不可变，那么可以用final关键字一起使用避免线程安全问题；否则需要采用同步的方式避免线程安全问题，如与volatile关键字一起使用等。
	 - static关键不能修饰局部变量，包括实例方法和静态方法，不然就会与static关键字的初衷-共享相违背。
	 3. 修饰静态方法
	 - main方法被Java规范定义成Java类的主入口。Java类的运行都由main方法开启（既然类的实例方法需要对象调用才能访问，而静态方法直接通过类名就能访问，那么在不考虑部署服务器的情况下，一个类是如何开始执行的呢？最大的可能就是通过“类名.静态方法”启动Java，而我定义那么多静态方法，JVM又是如何知道主入口呢？）
	 - static关键字本身的含义就是共享，而Java类加载到JVM内存的方法区，也是线程共享的，所以没必要用static关键字修饰普通类。
	 4. 问题
	 - 封装是Java类的三大特性之一，也是面向对象的主要特性。因为不需要通过对象，而直接通过类就能访问类的属性和方法，这有点破坏类的封装性；所以除了Utils类，代码中应该尽量少用static关键字修饰变量和方法。
   > https://zhuanlan.zhihu.com/p/73704288

- Java类的初始化顺序

  **静态变量 -> 静态初始化块** -> 变量 -> 初始化块 -> **构造方法**
  
  > https://blog.csdn.net/caomiao2006/article/details/51533382

### 抽象类
   - 并不是所有的类都是用来描绘对象的，如果一个类中没有包含足够的信息来描绘一个具体的对象，这样的类就是抽象类
   - 抽象类往往用来表征对问题领域进行分析、设计中得出的抽象概念，是对一系列看上去不同，但是本质上相同的具体概念的抽象
   > 比如，在一个图形编辑软件的分析设计过程中，就会发现问题领域存在着圆、三角形这样一些具体概念，它们是不同的，但是它们又都属于形状这样一个概念，形状这个概念在问题领域并不是直接存在的，它就是一个抽象概念。而正是因为抽象的概念在问题领域没有对应的具体概念，所以用以表征抽象概念的抽象类是不能够实例化的。

   - 比较
      1. 与具体类比较
      > 抽象类不能直接实例化，并且对抽象类使用 new 运算符会导致编译时错误。虽然一些变量和值在编译时的类型可以是抽象的，但是这样的变量和值必须或者为 null，或者含有对非抽象类的实例的引用（此非抽象类是从抽象类派生的）。
      允许（但不要求）抽象类包含抽象成员。
      抽象类不能被密封。
      
      2. 与接口比较
      > 抽象类表示该类中可能已经有一些方法的具体定义，但是接口就仅仅只能定义各个方法的界面（方法名，参数列表，返回类型），并不关心具体细节。
      接口是引用类型的，和抽象类的相似之处有三点：
      1. 不能实例化；
      2. 包含未实现的方法声明；
      3. 派生类必须实现未实现的方法，抽象类是抽象方法，接口则是所有成员（不仅是方法包括其他成员).

>  抽象类与接口紧密相关。然而接口又比抽象类更抽象，这主要体现在它们的差别上：
>
> 类可以实现无限个接口，但仅能从一个抽象（或任何其他类型）类继承，从抽象类派生的类仍可实现接口，从而得出接口是用来解决多重继承问题的。
>
> 抽象类当中可以存在非抽象的方法，可接口不能，且它里面的方法只是一个声明必须用public来修饰没有具体实现的方法。
>
> 抽象类中的成员变量可以被不同的修饰符来修饰，可接口中的成员变量默认的都是静态常量（static final）。

- 抽象类是对象的抽象，然而接口是一种行为规范。

### 继承

- 继承的方式

  ![java-extends-2020-12-08](https://tva1.sinaimg.cn/large/008i3skNly1gwp5rhpd7ej30id0ingmy.jpg)

  - 两种继承关键字

    1. Extends：在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。

    2. implements：使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。

```java
public interface A {
  public void eat();    
  public void sleep(); 
}  

public interface B {    
  public void show(); 
}  

public class C implements A,B { 
}
```

- 构造方法
  - 子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。
  - 如果父类的构造器**带有参数**，则必须在子类的构造器中**显式地通过 super 关键字调用父类的构造器并配以适当的参数列表**。
  - 如果父类构造器没有参数，则在子类的构造器中**不需要使用 super 关键字调用父类构造器，系统会自动调用父类的无参构造器**。

### 重载OverLoad

重载（Overload）是让类以统一的方式处理不同类型数据的一种手段，实质表现就是**多个具有不同的参数个数或者类型的同名函数**（返回值类型可随意，**不能以返回类型作为重载函数的区分标准**）同时存在于同一个类中，是一个类中多态性的一种表现（调用方法时通过传递不同参数个数和参数类型来决定具体使用哪个方法的多态性）

### 重写OverRide

重写（Override）是父类与子类之间的多态性，实质是**对父类的函数进行重新定义**，如果在子类中定义某方法与其父类有相同的名称和参数则该方法被重写，不过子类函数的访问修饰权限不能小于父类的；若子类中的方法与父类中的某一方法具有相同的方法名、返回类型和参数表，则新方法将覆盖原有的方法，如需父类中原有的方法则可使用 super 关键字。

## OOP

### (接口)Interface

1. 实现接口的类需要对接口中所有方法进行定义

### 多态

### 封装


## 多线程

1. Java是多线程的，它必须由Thread类或它的子类来创建

## 异常处理

## 递归



## 应试

### 计算机系统概述

- java编译过程：.java(raw code) -> .class(byte code,run on JVM) -> Runing
- 三种错误类型
  - 编译错误(Syntax error)
  - 运行错误(Run-time errror)
  - 逻辑错误(Logic error)
- JDK(Java Development Kit)是oracle提供的Java开发工具，运行Java程序只需要JRE(Java Running Environment)

### 数据与表达式

- 命名规则
- 保留关键字
- 省略赋值运算符和自增自减运算符
- 常用进制的写法
- 类型转换
- 运算符和优先级

### 使用类和对象



## 常用类库及方法表

### Scanner

- 属于Java API
- 有三种构造方法，分别用于IOStream、File&String Resource
- .next()和.nextLine()
- 读取输入数
- 迭代器
- 

>https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html

### String

### Random

### Math

- 所有方法都是静态方法

### NumberFormat

### DecimalFormat

### Integer（Wrapper）

>https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html
