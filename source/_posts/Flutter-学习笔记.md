---
TextButtontitle: Flutter学习笔记
description: Flutter的笔记，主要扒自官方站
categories: 开发
tags:
  - Flutter
  - Android
  - 设计模式
abbrlink: 43a46ea2
---

# 简介

## 参考资料

- Flutter实战

- Flutter Codelab

- Flutter核心技术与实战

  

## Dart语言

> Dart 在静态语法方面和 Java 非常相似，如类型定义、函数声明、泛型等，而在动态特性方面又和 JavaScript 很像，如函数式特性、异步支持等。

### 变量声明

1. 使用var声明变量。

   Dart 中 var 变量一旦赋值，类型便会确定，则不能再改变其类型。

   > Dart不管怎么说也是个强类型的语言，所以第一次使用后就被确定

2. 使用`dynamic`和`Object`

   与Java相似，`Object`是所有对象的基类，`dynamic`与`Object`声明的变量都可以赋值任意对象，且后期可以改变赋值的类型，这和 `var` 是不同的

   ```dart
   dynamic t;
   Object x;
   t = "hi world";
   x = 'Hello Object';
   //下面代码没有问题
   t = 1000;
   x = 1000;
   ```

   > `dynamic`与`Object`不同的是`dynamic`声明的对象编译器会提供所有可能的组合，而`Object`声明的对象只能使用 `Object` 的属性与方法, 否则编译器会报错

3. `final`和`const`

   `const` 变量是一个编译时常量（**编译时直接替换为常量值**），`final`变量在第一次使用时被初始化。

4. 空安全

   ```dart
   int i = 8; //默认为不可空，必须在定义时初始化。
   int? j; // 定义为可空类型，对于可空变量，我们在使用前必须判空。
   
   // 如果我们预期变量不能为空，但在定义时不能确定其初始值，则可以加上late关键字，
   // 表示会稍后初始化，但是在正式使用它之前必须得保证初始化过了，否则会报错
   late int k;
   k=9;
   ```

   如果一个变量我们定义为可空类型，在某些情况下即使我们给它赋值过了，但是预处理器仍然有可能识别不出，这时我们就要显式（通过在变量后面加一个”!“符号）告诉预处理器它已经不是null

   ```dart
   class Test{
     int? i;
     Function? fun;
     say(){
       if(i!=null) {
         print(i! * 8); //因为已经判过空，所以能走到这 i 必不为null，如果没有显式申明，则 IDE 会报错
       }
       if(fun!=null){
         fun!(); // 同上
       }
     }
   }
   
   // 这是个针对函数变量的语法糖
   fun?.call() // fun 不为空时则会被调用
   ```

  Dart同时提供了一些运算用于Null的处理，例如

  - `?.`：若为Null，则略过这一行
  - `??`：如果为Null，则返回右值，否则返回左值
  - `??=`：如果左边为Null，则给左值赋予右值

### 函数声明

> Dart是一种真正的面向对象的语言，所以**即使是函数也是对象**，并且有一个类型**Function**。这意味着函数可以赋值给变量或作为参数传递给其他函数，这是函数式编程的典型特征。

Dart函数声明如果没有显式声明返回值类型时会默认当做`dynamic`处理

```dart
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

函数可以被作为变量使用

```dart
var say = (str){
  print(str);
};
say("hi world");
```

可变参数的声明

```dart
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```

定义函数时，使用{param1, param2, …}，放在参数列表的最后面，用于指定命名参数

**不能同时使用可选的位置参数和可选的命名参数**

```dart
//设置[bold]和[hidden]标志
void enableFlags({bool bold, bool hidden}) {
    // ... 
}
```

### mixin(相当于对多继承的一种实现)

> Dart 是不支持多继承的，但是它支持 mixin，简单来讲 mixin 可以 “组合” 多个类

我们定义了几个 mixin，然后通过 with 关键字将它们组合成不同的类

```dart
class Person {
  say() {
    print('say');
  }
}

mixin Eat {
  eat() {
    print('eat');
  }
}

mixin Walk {
  walk() {
    print('walk');
  }
}

mixin Code {
  code() {
    print('key');
  }
}

class Dog with Eat, Walk{}
class Man extends Person with Eat, Walk, Code{}
```

### 异步

> Dart类库有非常多的返回`Future`或者`Stream`对象的函数。 这些函数被称为**异步函数**：它们只会在设置好一些耗时操作之后返回，比如像 IO操作，而不是等到这个操作完成。

#### Future

`Future`与JavaScript中的`Promise`非常相似，表示一个异步操作的最终完成（或失败）及其结果值的表示

`Future` 的所有API的返回值仍然是一个`Future`对象，所以可以很方便的进行链式调用

使用Future.delayed 创建了一个延时任务（实际场景会是一个真正的耗时任务，比如一次网络请求），即2秒后返回结果字符串"hi world!"，然后我们在then中接收异步结果并打印结果

```dart
Future.delayed(Duration(seconds: 2),(){
   return "hi world!";
}).then((data){
   print(data);
});
```

如果异步任务发生错误，我们可以在`catchError`中捕获错误

```dart
Future.delayed(Duration(seconds: 2),(){
   //return "hi world!";
   throw AssertionError("Error");  
}).then((data){
   //执行成功会走到这里  
   print("success");
}).catchError((e){
   //执行失败会走到这里  
   print(e);
});
```

有些时候，我们会遇到无论异步任务执行成功或失败都需要做一些事的场景，比如在网络请求前弹出加载对话框，在请求结束后关闭对话框。这种场景，有两种方法，第一种是分别在`then`或`catch`中关闭一下对话框，第二种就是使用`Future`的`whenComplete`回调

```dart
Future.delayed(Duration(seconds: 2),(){
   //return "hi world!";
   throw AssertionError("Error");
}).then((data){
   //执行成功会走到这里 
   print(data);
}).catchError((e){
   //执行失败会走到这里   
   print(e);
}).whenComplete((){
   //无论成功或失败都会走到这里
});
```

总的来说，使用`Future`执行一段异步调用的语句包含四个部分，一是`.delayed({})`，要执行的语句；二是`.then((data){})`执行成功要执行的语句；三是失败时执行的`.catchError((e){})`；四是总是执行的`.whenComplete((){})`

记得在执行时抛出`AssertionError("Error")`异常！

对于一组要执行的异步操作，我们使用`Future.wait`，它接受一个`Future`数组参数，只有数组中所有`Future`都执行成功后，才会触发`then`的成功回调，只要有一个`Future`执行失败，就会触发错误回调

```dart
Future.wait([
  // 2秒后返回结果  
  Future.delayed(Duration(seconds: 2), () {
    return "hello";
  }),
  // 4秒后返回结果  
  Future.delayed(Duration(seconds: 4), () {
    return " world";
  })
]).then((results){
  print(results[0]+results[1]);
}).catchError((e){
  print(e);
});
```

#### Async/Await

> Dart中的`async/await` 和JavaScript中的`async/await`功能和用法是一模一样的

#### 回调的整体解决思路

如果代码中有大量异步逻辑，并且出现大量异步任务依赖其它异步任务的结果时，必然会出现`Future.then`回调中套回调情况。因此我们可以将调用的结果缓存在本地文件系统，再统一进行调用

```dart
//先分别定义各个异步任务
Future<String> login(String userName, String pwd){
	...
    //用户登录
};
Future<String> getUserInfo(String id){
	...
    //获取用户信息 
};
Future saveUserInfo(String userInfo){
	...
	// 保存用户信息 
}; 

login("alice","******").then((id){
 //登录成功后通过，id获取用户信息    
 getUserInfo(id).then((userInfo){
    //获取用户信息后保存 
    saveUserInfo(userInfo).then((){
       //保存用户信息，接下来执行其它操作
        ...
    });
  });
})
```

这个问题被形象的称为**回调地狱（Callback Hell）**

`Dart`语言提供两种方案，第一个是`Future`。利用其始终返回一个`Future`对象的特性，我们可以进行如下格式的调用

```dart
login("alice","******").then((id){
  	return getUserInfo(id);
}).then((userInfo){
    return saveUserInfo(userInfo);
}).then((e){
   //执行接下来的操作 
}).catchError((e){
  //错误处理  
  print(e);
});
```

使用async/await也可以实现，例如

```dart
task() async {
   try{
    String id = await login("alice","******");
    String userInfo = await getUserInfo(id);
    await saveUserInfo(userInfo);
    //执行接下来的操作   
   } catch(e){
    //错误处理   
    print(e);   
   }  
}
```

#### Stream

`Stream` 也是用于接收异步事件数据，和 `Future` 不同的是，它可以接收多个异步操作的结果（成功或失败）。 

也就是说，在执行异步任务时，可以通过**多次触发成功或失败事件来传递结果数据或错误异常。**

 `Stream` 常用于会**多次读取数据的异步任务场景**，如网络内容下载、文件读写等

```dart
Stream.fromFutures([
  // 1秒后返回结果
  Future.delayed(Duration(seconds: 1), () {
    return "hello 1";
  }),
  // 抛出一个异常
  Future.delayed(Duration(seconds: 2),(){
    throw AssertionError("Error");
  }),
  // 3秒后返回结果
  Future.delayed(Duration(seconds: 3), () {
    return "hello 3";
  })
]).listen((data){
   print(data);
}, onError: (e){
   print(e.message);
},onDone: (){

});
```

### Dart和其他主流语言

## Widget简介

在 Flutter 中，Widget 采用由父到子、自顶向下的方式进行构建，父 Widget 控制着子 Widget 的显示样式，其样式配置由父 Widget 在构建时提供。

### StatelessWidget

![img](https://img.kancloud.cn/3e/c9/3ec97a9f584132c2bcdbca60fd2888cc_442x422.png)

> 第一个小例子是，我需要创建一个自定义的弹窗控件，把使用 App 过程中出现的一些错误信息提示给用户。这个组件的父 Widget，能够完全在子 Widget 初始化时将组件所需要的样式信息和错误提示信息传递给它，也就意味着父 Widget 通过初始化参数就能完全控制其展示效果。所以，我可以采用继承 StatelessWidget 的方式，来进行组件自定义。
>
> 第二个小例子是，我需要定义一个计数器按钮，用户每次点击按钮后，按钮颜色都会随之加深。可以看到，这个组件的父 Widget 只能控制子 Widget 初始的样式展示效果，而无法控制在交互过程中发生的颜色变化。所以，我无法通过继承 StatelessWidget 的方式来自定义组件。那么，这个时候就轮到 StatefulWidget 出场了。

### StatefulWidget

![img](https://img.kancloud.cn/8a/e7/8ae7bf36f618a999da8847cbb4da4bf6_762x502.png)

与 StatelessWidget 相对应的，有一些 Widget（比如 Image、Checkbox）的展示，除了父 Widget 初始化时传入的静态配置之外，还需要处理用户的交互（比如，用户点击按钮）或其内部数据的变化（比如，网络数据回包），并体现在 UI 上。



## Flutter简介

### 如何理解Flutter

Flutter可以被看作是一个UI框架，它的存在有效提高了跨平台开发的效率和UI的美观。

Flutter使用Dart语言开发，支持**空安全(Null Safety)**、单行函数之类的语法特性；能够实现很多业务逻辑的处理；可以调用原生平台的代码进行开发；大量的包也已经实现了如调用摄像头这样的操作。

### Flutter原理

Flutter框架示意图

![图1-1](https://book.flutterchina.club/assets/img/1-1.82c25693.png)

### Flutter项目的结构

#### 开发习惯

> 目前为止这些都是观察到的规律，并不一定是合适的

- 与Java不同，Dart一般不会按照类来组织文件，一个文件一般会包含一整个业务逻辑

- Dart语言不存在接口等概念，一般也不会考虑设计模式（据说设计模式主要是为了弥补Java的一些乱七八糟的小问题才被提出）。分包的依据主要考虑组件功能，例如:

  - widgets：用于存放自定义的组件
  - routes：存放导航页面，或者仅为一个用于注册命名路由的文件
  - models：存放实体类，一般只放一个文件
  - common/data：存放常量
  - l10n：国际化
  - pages
  - themes

  > 官方示例Gallery
  >
  > https://github.com/flutter/gallery/tree/master/lib
  >
  > 
  >
  > 组件化和平台化，该如何组织合理稳定的Flutter工程结构？——Flutter核心技术与实践
  >
  > https://www.kancloud.cn/alex_wsc/flutter_demo/1572034

### 基本元素

一个Flutter项目同样是从`main`方法开始执行的，然后调用`MyApp`方法开始build一个Widget树

```dart
void main() => runApp(const MyApp());
```

Flutter中，万物皆为Widget，甚至连居中这样的排版元素也是Widget，整个App也是一个MaterialApp

所有的Widget，不管是StatefulWidget还是StatelessWidget都有一个build方法构建，除此以外涉及到的还有Flutter中Widget的生命周期问题

![State生命周期方法](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/20a53f87642e44a2ae19d3dd42787005~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.image)

Flutter中采用的是和Vue、React类似的响应式布局，通过声明Widget、State双向绑定数据实现数据和UI的更新。当数据更新时，State状态改变，触发build方法，依次向下逐个触发build方法更新视图。

# 基本概念和一些原理

## Context

context是BuildContext的一个示例，它是对该组件再Widget树中位置的描述，提供了一些方法。

> 如果 StatefulWidget 的状态是希望暴露出的，应当在 StatefulWidget 中提供一个of 静态方法来获取其 State 对象，开发者便可直接通过该方法来获取；如果 State不希望暴露，则不提供of方法。

## 调试

1. `debugger()`语句采用一个可选`when`参数，我们可以指定该参数仅在特定条件为真时中断
2. `print()`功能将输出到系统控制台，我们可以使用`flutter logs`来查看它（基本上是一个包装`adb logcat`）
3. `debugPrint()`是一个封装print，它将输出限制在一个级别，避免被Android内核丢弃

## 异常

>  `debugPrint()`是一个封装print，它将输出限制在一个级别，避免被Android内核丢弃

# 基本组件和布局

## 文本和按钮

### Text

Text是最基本的一个组件，用来显示单一文本

Text组件由三部分组成，一是显示的内容，二是和显示格式有关的一系列参数，三是style参数，一般传入一个TextStyle对象控制字体格式

```dart
Text(
  '文本是视图系统中的常见控件，用来显示一段特定样式的字符串，就比如 Android 里的 TextView，或是 iOS 中的 UILabel。',
  textAlign: TextAlign.center,// 居中显示
  style: TextStyle(fontWeight: FontWeight.bold, fontSize: 20, color: Colors.red),//20 号红色粗体展示
);
```

### Text.rich和TextSpan

TextSpan主要用来解决切片显示的问题

```dart
TextStyle blackStyle = TextStyle(fontWeight: FontWeight.normal, fontSize: 20, color: Colors.black); // 黑色样式
 
TextStyle redStyle = TextStyle(fontWeight: FontWeight.bold, fontSize: 20, color: Colors.red); // 红色样式
 
Text.rich(
    TextSpan(
        children: <TextSpan>[
          TextSpan(text:'文本是视图系统中常见的控件，它用来显示一段特定样式的字符串，类似', style: redStyle), // 第 1 个片段，红色样式 
          TextSpan(text:'Android', style: blackStyle), // 第 1 个片段，黑色样式 
          TextSpan(text:'中的', style:redStyle), // 第 1 个片段，红色样式 
          TextSpan(text:'TextView', style: blackStyle) // 第 1 个片段，黑色样式 
        ]),
  textAlign: TextAlign.center,
);
```

### Button

Button有很多种，包括FloatingActionButton、ElevatedButton、RaisedButton和FlatButton等

一个Button组件主要包括两个属性，onPressed和child

```dart
FlatButton(
    color: Colors.yellow, // 设置背景色为黄色
    shape:BeveledRectangleBorder(borderRadius: BorderRadius.circular(20.0)), // 设置斜角矩形边框
    colorBrightness: Brightness.light, // 确保文字按钮为深色
    onPressed: () => print('FlatButton pressed'), 
    child: Row(children: <Widget>[Icon(Icons.add), Text("Add")],)
)；
```

除此之外，还有一个icon参数，能够方便的制作带图标的按钮

## 图片和图标

### Image

Image控件有三个主要方式，分别是加载Asset资源`Image.asset('path')`、加载file资源`Image.file(new File('path'))`和网络图片`Image.network('URL')`

除了可以根据图片的显示方式设置不同的图片源之外，图片的构造方法还提供了填充模式 fit、拉伸模式 centerSlice、重复模式 repeat 等属性，可以针对图片与目标区域的宽高比差异制定排版模式

### FadeInImage

FadeInImage 控件提供了图片占位的功能，并且支持在图片加载完成时淡入淡出的视觉效果。此外，由于 Image 支持 gif 格式，我们甚至还可以将一些炫酷的加载动画作为占位图。

```dart
FadeInImage.assetNetwork(
  placeholder: 'assets/loading.gif', //gif 占位
  image: 'https://xxx/xxx/xxx.jpg',
  fit: BoxFit.cover, // 图片拉伸模式
  width: 200,
  height: 200,
)
```

### CachedNetworkImage

ImageCache 使用 LRU（Least Recently Used，最近最少使用）算法进行缓存更新策略，并且默认最多存储 1000 张图片，最大缓存限制为 100MB，当限定的空间已存满数据时，把最久没有被访问到的图片清除。图片**缓存只会在运行期间生效，也就是只缓存在内存中**。

如果想要支持缓存到文件系统，可以使用第三方的[CachedNetworkImage](https://pub.dev/packages/cached_network_image/)控件。

CachedNetworkImage 的使用方法与 Image 类似，除了支持图片缓存外，还提供了比 FadeInImage 更为强大的加载过程占位与加载错误占位，可以支持比用图片占位更灵活的自定义控件占位。

```dart
CachedNetworkImage(
        imageUrl: "http://xxx/xxx/jpg",
        placeholder: (context, url) => CircularProgressIndicator(),
        errorWidget: (context, url, error) => Icon(Icons.error),
     )
```

## 对齐和定位

## 可滚动组件

### ListView

**ListView 提供了一个默认构造函数 ListView**，我们可以通过设置它的 children 参数，很方便地将所有的子 Widget 包含到 ListView 中。

ListTile 是 Flutter 提供的用于快速构建列表项元素的一个小组件单元，用于 1~3 行（leading、title、subtitle）展示文本、图标等视图元素的场景，通常与 ListView 配合使用。

**ListView 的另一个构造函数 ListView.builder，则适用于子 Widget 比较多的场景**。这个构造函数有两个关键参数：

- itemBuilder，是列表项的创建方法。当列表滚动到相应位置时，ListView 会调用该方法创建对应的子 Widget。
- itemCount，表示列表项的数量，如果为空，则表示 ListView 为无限列表。

```dart
ListView.builder(
    itemCount: 100, // 元素个数
    itemExtent: 50.0, // 列表项高度
    itemBuilder: (BuildContext context, int index) => ListTile(title: Text("title $index"), subtitle: Text("body $index"))
);
```

与 ListView.builder 抽离出了子 Widget 的构建方法类似，ListView.separated 抽离出了分割线的创建方法 separatorBuilder，以便根据 index 设置不同样式的分割线。

```dart
// 使用 ListView.separated 设置分割线
ListView.separated(
    itemCount: 100,
    separatorBuilder: (BuildContext context, int index) => index %2 ==0? Divider(color: Colors.green) : Divider(color: Colors.red),//index 为偶数，创建绿色分割线；index 为奇数，则创建红色分割线
    itemBuilder: (BuildContext context, int index) => ListTile(title: Text("title $index"), subtitle: Text("body $index"))// 创建子 Widget
)
```



### 滚动嵌套

 Flutter 中有一个专门的控件 CustomScrollView，用来处理多个需要自定义滚动效果的 Widget。在 CustomScrollView 中，**这些彼此独立的、可滚动的 Widget 被统称为 Sliver**。





## 线性布局——使用Row和Column

## 弹性布局——源于Web的Flex

## 流式布局——不太清楚

## 层叠布局——不了解

# 功能性组件

## 进度指示器

## 输入框、表单、单选开关和复选框

### TextFiled组件

`TextField`组件提供了一个输入框，示例

```dart
Column(
  children: <Widget>[
    TextField(
      autofocus: true,
      decoration: InputDecoration(
        labelText: "用户名",
        hintText: "用户名或邮箱",
        prefixIcon: Icon(Icons.person)
      ),
    ),
    TextField(
      decoration: InputDecoration(
        labelText: "密码",
        hintText: "您的登录密码",
        prefixIcon: Icon(Icons.lock)
      ),
      obscureText: true,
    ),
  ],
);
```

其具有的controller属性可以配置一个controller，用于文本的获取或控制光标位置、选择状态等。

controller可以用来直接获取输入内容，调用`.text()`方法即可。

可以对一个controller配置监听,当然，也可以通过`onChanged()`实现，例如

```dart
@override
void initState() {
  //监听输入改变  
  _unameController.addListener((){
    print(_unameController.text);
  });
}
```

`onChanged`是专门用于监听文本变化，而`controller`的功能却多一些，除了能监听文本变化外，它还可以设置默认值、选择文本，例如

```dart
_selectionController.text="hello world!";
_selectionController.selection=TextSelection(
    baseOffset: 2,
    extentOffset: _selectionController.text.length
);
```

文本输入时的焦点可以通过`FocusNode`和`FocusScopeNode`来控制，**默认情况下，焦点由`FocusScope`来管理**，它代表焦点控制范围，可以在这个范围内可以通过`FocusScopeNode`在输入框之间移动焦点、设置默认焦点等。

我们可以通过`FocusScope.of(context)` 来获取Widget树中默认的`FocusScopeNode`。

```dart
class FocusTestRoute extends StatefulWidget {
  @override
  _FocusTestRouteState createState() => _FocusTestRouteState();
}

class _FocusTestRouteState extends State<FocusTestRoute> {
  FocusNode focusNode1 = FocusNode();
  FocusNode focusNode2 = FocusNode();
  FocusScopeNode? focusScopeNode;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: EdgeInsets.all(16.0),
      child: Column(
        children: <Widget>[
          TextField(
            autofocus: true, 
            focusNode: focusNode1,//关联focusNode1
            decoration: InputDecoration(
                labelText: "input1"
            ),
          ),
          TextField(
            focusNode: focusNode2,//关联focusNode2
            decoration: InputDecoration(
                labelText: "input2"
            ),
          ),
          Builder(builder: (ctx) {
            return Column(
              children: <Widget>[
                ElevatedButton(
                  child: Text("移动焦点"),
                  onPressed: () {
                    //将焦点从第一个TextField移到第二个TextField
                    // 这是一种写法 FocusScope.of(context).requestFocus(focusNode2);
                    // 这是第二种写法
                    if(null == focusScopeNode){
                      focusScopeNode = FocusScope.of(context);
                    }
                    focusScopeNode.requestFocus(focusNode2);
                  },
                ),
                ElevatedButton(
                  child: Text("隐藏键盘"),
                  onPressed: () {
                    // 当所有编辑框都失去焦点时键盘就会收起  
                    focusNode1.unfocus();
                    focusNode2.unfocus();
                  },
                ),
              ],
            );
          },
          ),
        ],
      ),
    );
  }
```

同样的，我们可以为`FocusNode`创建一个监听

```dart
...
// 创建 focusNode   
FocusNode focusNode = FocusNode();
...
// focusNode绑定输入框   
TextField(focusNode: focusNode);
...
// 监听焦点变化    
focusNode.addListener((){
   print(focusNode.hasFocus);
});
```



### Form组件

Flutter提供了一个`Form` 组件，它可以对输入框进行分组，然后进行一些统一操作，如输入内容校验、输入框重置以及输入内容保存

`Form`的子孙元素必须是`FormField`类型，为了方便使用，Flutter 提供了一个`TextFormField`组件，它继承自`FormField`类，也是`TextField`的一个包装类，所以除了`FormField`定义的属性之外，它还包括`TextField`的属性

```dart
import 'package:flutter/material.dart';

class FormTestRoute extends StatefulWidget {
  @override
  _FormTestRouteState createState() => _FormTestRouteState();
}

class _FormTestRouteState extends State<FormTestRoute> {
  TextEditingController _unameController = TextEditingController();
  TextEditingController _pwdController = TextEditingController();
  GlobalKey _formKey = GlobalKey<FormState>();

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey, //设置globalKey，用于后面获取FormState
      autovalidateMode: AutovalidateMode.onUserInteraction,
      child: Column(
        children: <Widget>[
          TextFormField(
            autofocus: true,
            controller: _unameController,
            decoration: InputDecoration(
              labelText: "用户名",
              hintText: "用户名或邮箱",
              icon: Icon(Icons.person),
            ),
            // 校验用户名
            validator: (v) {
              return v!.trim().isNotEmpty ? null : "用户名不能为空";
            },
          ),
          TextFormField(
            controller: _pwdController,
            decoration: InputDecoration(
              labelText: "密码",
              hintText: "您的登录密码",
              icon: Icon(Icons.lock),
            ),
            obscureText: true,
            //校验密码
            validator: (v) {
              return v!.trim().length > 5 ? null : "密码不能少于6位";
            },
          ),
          // 登录按钮
          Padding(
            padding: const EdgeInsets.only(top: 28.0),
            child: Row(
              children: <Widget>[
                Expanded(
                  child: ElevatedButton(
                    child: Padding(
                      padding: const EdgeInsets.all(16.0),
                      child: Text("登录"),
                    ),
                    onPressed: () {
                      // 通过_formKey.currentState 获取FormState后，
                      // 调用validate()方法校验用户名密码是否合法，校验
                      // 通过后再提交数据。
                      if ((_formKey.currentState as FormState).validate()) {
                        //验证通过提交数据
                      }
                    },
                  ),
                ),
              ],
            ),
          )
        ],
      ),
    );
  }
}
```



### Switch组件

`Switch`组件提供了一个Material风格的单选开关。

他的状态由父组件进行管理

当`Switch`或`Checkbox`被点击时，会触发它们的`onChanged`回调，我们可以在此回调中处理选中状态改变逻辑

有一个`activeColor`属性，用于设置激活态的颜色

### CheckBox组件

`CheckBox`大部分属性与`Switch`相同。

`Checkbox`有一个属性`tristate` ，表示是否为**三态**，其默认值为`false` ，这时 Checkbox 有两种状态即“选中”和“不选中”，对应的 value 值为`true`和`false` ；如果`tristate`值为`true`时，value 的值会增加一个状态`null`

## 装饰相关的组件

## Scaffold组件

## 大小适配相关的组件

# 路由和状态管理

## 数据共享和跨组件状态共享

## 路由管理

路由管理主要涉及到Route和Navigator两个类，Route是对页面的抽象，主要使用MaterialPageRoute建立路由模板。

MaterialPageRoute 是一种路由模板，定义了路由创建及切换过渡动画的相关配置，可以针对不同平台，实现与平台页面切换动画风格一致的路由切换动画。

Navigator负责维护一个Route栈。

### 基本操作

使用`Navigator.push(context, NewRoute)`转到新page

使用`Navigator.pop()`移去栈顶的page

### 命名路由

要想通过名字来指定页面切换，我们必须先给应用程序 MaterialApp 提供一个页面名称映射规则，即路由表 routes，这样 Flutter 才知道名字与页面 Widget 的对应关系。

路由表实际上是一个 Map，其中 key 值对应页面名字，而 value 值则是一个 WidgetBuilder 回调函数，我们需要在这个函数中创建对应的页面。

```dart
MaterialApp(
    ...
    // 注册路由
    routes:{
      "second_page":(context)=>SecondPage(),
    },
);
// 使用名字打开页面
Navigator.pushNamed(context,"second_page");
```

对于一个潜在的空路由，我们考虑对用户进行友好的错误提示，比如跳转到一个统一的 NotFoundScreen 页面，也方便我们对这类错误进行统一收集、上报。因此，在注册路由表时，Flutter 提供了 UnknownRoute 属性，我们可以对未知的路由标识符进行统一的页面跳转处理。

```dart
MaterialApp(
    ...
    // 注册路由
    routes:{
      "second_page":(context)=>SecondPage(),
    },
    // 错误路由处理，统一返回 UnknownPage
    onUnknownRoute: (RouteSettings setting) => MaterialPageRoute(builder: (context) => UnknownPage()),
);
 
// 使用错误名字打开页面
Navigator.pushNamed(context,"unknown_page");
```



### 页面参数的传递

Flutter 提供了**路由参数**的机制，可以在打开路由时传递相关参数，在目标页面通过 RouteSettings 来获取页面参数

```dart
// 打开页面时传递字符串参数
Navigator.of(context).pushNamed("second_page", arguments: "Hey");
 
class SecondPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // 取出路由参数
    String msg = ModalRoute.of(context).settings.arguments as String;
    return Text(msg);
  }
}
```

Flutter 也提供了**返回参数**的机制。在 push 目标页面时，可以设置目标页面关闭时监听函数，以获取返回参数；而目标页面可以在关闭路由时传递相关参数。

```dart
class SecondPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: <Widget>[
          Text('Message from first screen: $msg'),
          RaisedButton(
            child: Text('back'),
            // 页面关闭时传递参数
            onPressed: ()=> Navigator.pop(context,"Hi")
          )
        ]
      ));
  }
}
 
class _FirstPageState extends State<FirstPage> {
  String _msg='';
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      body: Column(children: <Widget>[
        RaisedButton(
            child: Text('命名路由（参数 & 回调）'),
            // 打开页面，并监听页面关闭时传递的参数
            onPressed: ()=> Navigator.pushNamed(context, "third_page",arguments: "Hey").then((msg)=>setState(()=>_msg=msg)),
        ),
        Text('Message from Second screen: $_msg'),
 
      ],),
    );
  }
}
```

## 导航返回拦截

# 手势、通知和动画

## 手势的识别

## 通知

# 网络

## HTTP Client

## Dio

get方法示例

```dart
void getRequest() async {
  // 创建网络调用示例
  Dio dio = new Dio();
  
  // 设置 URI 及请求 user-agent 后发起请求
  var response = await dio.get("https://flutter.dev", options:Options(headers: {"user-agent" : "Custom-UA"}));
  
 // 打印请求结果
  if(response.statusCode == HttpStatus.ok) {
    print(response.data.toString());
  } else {
    print("Error: ${response.statusCode}");
  }
}
```

文件的上传下载

```dart
// 使用 FormData 表单构建待上传文件
FormData formData = FormData.from({
  "file1": UploadFileInfo(File("./file1.txt"), "file1.txt"),
  "file2": UploadFileInfo(File("./file2.txt"), "file1.txt"),
 
});
// 通过 post 方法发送至服务端
var responseY = await dio.post("https://xxx.com/upload", data: formData);
print(responseY.toString());
 
// 使用 download 方法下载文件
dio.download("https://xxx.com/file1", "xx1.zip");
 
// 增加下载进度回调函数
dio.download("https://xxx.com/file1", "xx2.zip", onReceiveProgress: (count, total) {
	//do something      
});
```

使用拦截器添加Token、User-Agent等参数

```dart
// 增加拦截器
dio.interceptors.add(InterceptorsWrapper(
    onRequest: (RequestOptions options){
      // 为每个请求头都增加 user-agent
      options.headers["user-agent"] = "Custom-UA";
      // 检查是否有 token，没有则直接报错
      if(options.headers['token'] == null) {
        return dio.reject("Error: 请先登录 ");
      } 
      // 检查缓存是否有数据
      if(options.uri == Uri.parse('http://xxx.com/file1')) {
        return dio.resolve(" 返回缓存数据 ");
      }
      // 放行请求
      return options;
    }
));
 
// 增加 try catch，防止请求报错
try {
  var response = await dio.get("https://xxx.com/xxx.zip");
  print(response.data.toString());
}catch(e) {
  print(e);
}
```



## JSON的解析

### Bean的编写

```dart
class User {
  final String name;
  final String email;

  User(this.name, this.email);

  User.fromJson(Map<String, dynamic> json)
      : name = json['name'],
        email = json['email'];

  Map<String, dynamic> toJson() =>
    <String, dynamic>{
      'name': name,
      'email': email,
    };
}
```

需要关注的有两个方法，`.fromJson`和`.toJson()`

### JsonSerializable自动生成Model

> `json_serializable package`是一个自动化的源代码生成器，可以在开发阶段为我们生成 JSON 序列化模板，这样一来，由于序列化代码不再由我们手写和维护，我们将运行时产生 JSON 序列化异常的风险降至最低

使用它需要调用如下两个开发依赖项

```yaml
dependencies:
  json_annotation: <最新版本>

dev_dependencies:
  build_runner: <最新版本>
  json_serializable: <最新版本>
```

Bean文件的声明

```dart
import 'package:json_annotation/json_annotation.dart';

// user.g.dart 将在我们运行生成命令后自动生成
part 'user.g.dart';

///这个标注是告诉生成器，这个类是需要生成Model类的
@JsonSerializable()

class User{
  User(this.name, this.email);

  String name;
  String email;
  //不同的类使用不同的mixin即可
  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);  
}
```

在配置好后，并不会得到对应的bean，一种方案是通过`flutter packages pub run build_runner watch`在项目根目录下运行来启动_watcher_。只需启动一次观察器，然后它就会在后台运行，这是安全的

### 自动化脚本









## 网络的封装

# 数据存储

## 文件存储

## Shared Preference

## 本地数据库

# 多平台适配

## PlatformChannel

## Windows

## Android

# 常用功能的实现

## 摄像头和相册的调用

## 主题系统

## 多语言

## 自动登录
